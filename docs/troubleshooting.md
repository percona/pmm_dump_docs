# Troubleshooting

## General issues

### How to bypass SSL errors during PMM Dump export and import

PMM Server uses self-signed certificates by default unless you replace them with your own proper certificates as described [here](https://docs.percona.com/percona-monitoring-and-management/3/admin/security/ssl_encryption.html).

By default, PMM Dump expects that certificates for the HTTPS connection should be trusted and fails with an error when connecting to PMM:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='https://admin:admin@127.0.0.1' 
2021-10-08T13:19:29Z FTL Failed to compose meta error="failed to get PMM version: x509: cannot validate certificate for 127.0.0.1 because it doesn't contain any IP SANs"
```

If you want to continue using self-signed certificates, you can run PMM Dump with the option `--allow-insecure-certs` which allows the tool to continue even if the certificate is not trusted:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='https://admin:admin@127.0.0.1' --allow-insecure-certs
2021-10-08T13:25:45Z INF Exporting metrics…
...
```

## Export issues

### How to bypass error "Failed to create ClickHouse source" when exporting Query Analytics Data

When you try to export Query Analytics (QAN) data with PMM Dump, it may fail with an error "Failed to create ClickHouse source".

PMM Server stores QAN data in the ClickHouse server that listens on port 9000. Unlike ports for HTTP and HTTPS connections that are published when you install a PMM Server, the ClickHouse port is only exposed by Docker and not published. This means that while you can connect to your PMM server using your machine hostname and IP address, port 9000 cannot be accessed this way.

Therefore, if you point the `--pmm-url` option to the IP address of your machine or even localhost, you will not be able to export QAN data:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='http://admin:admin@127.0.0.1' --dump-qan
2021-10-09T13:14:51Z FTL Failed to create ClickHouse source: dial tcp 127.0.0.1:9000: connect: connection refused
```

However, you can access ClickHouse if you use the IP that Docker assigns to your PMM Server. If you do not know this IP address, run the `docker inspect` command and search for the `IPAddress` value in the container `NetworkSettings`. Once you find the IP address that Docker assigned to your PMM Server container, you can use it to export QAN. See [Exporting Query Analytics Data](export_qan.md) for more details.

An alternative solution would be publishing port 9000 at the time when you create a PMM Server container, but we do not recommend it, because doing so opens outside access to your raw queries and is not secure.

## Import issues

### Import fails with the message `failed to write chunk: non-OK response from victoria metrics: 413`

The reason for this issue is that the value of `client_max_body_size` in the [NGINX](https://www.nginx.com/) configuration of the PMM server is smaller than the maximum chunk size in the dump file.

To resolve this issue, update the `client_max_body_size` parameter in the `/etc/nginx/conf.d/pmm.conf` under the `server` config and reload `nginx`.

1. Obtain the `Max Chunk Size` in the dump file:

``` {.bash data-prompt="$" }
pmm-dump show-meta -d pmm_dump_data.tar.gz 
Build: 
PMM Version: 2.29.0-19.2207180503.2c740d9.el7
Max Chunk Size: 24.8 MB (23.7 MiB)
```

2. Log in to the Docker `pmm-server` container:

``` {.bash data-prompt="$" }
docker exec -it pmm-server /bin/bash
```

3. Open the file `/etc/nginx/conf.d/pmm.conf` and update the `client_max_body_size` parameter:

``` {.bash data-prompt="$" }
vi /etc/nginx/conf.d/pmm.conf

    client_max_body_size 25m;
```

4. Restart the `nginx` service:

``` {.bash data-prompt="$" }
supervisorctl restart nginx
```

5. Retry the `pmm-dump import` command.

### Import fails with the message `error when processing native block: cannot unmarshal native block ... src is too short for reading string`

The reason for this error is incompatibility between VictoriaMetrics formats, introduced in version 1.82.1. See [SE-83](https://jira.percona.com/browse/SE-83) for more details.

To bypass this error, examine the dump file with the help of the [`verify-vm-native-data`](verify-vm-native-data.md) script:

``` {.bash data-prompt="$" }
p$ ./support-files/verify-vm-native-data pmm-dump-1651523184.tar.gz 
Trying to verify chunk with vmctl v1.82.1
2023/03/08 16:41:18 verifying block at path="/tmp/tmp.7h3rAq0Ay2/vm/1651518684-1651518984.bin"
cannot parse block at path="/tmp/tmp.7h3rAq0Ay2/vm/1651518684-1651518984.bin", blocksCount=0, err=error when processing native block: cannot unmarshal native block from 23 bytes: cannot read timestampsData: src is too short for reading string with size 937; len(src)=1
Dump data doesn't use VictoriaMetrics 1.82.1 native format

Trying to verify chunk with vmctl v1.77.2
2023/03/08 16:41:18 verifying block at path="/tmp/tmp.7h3rAq0Ay2/vm/1651518684-1651518984.bin"
2023/03/08 16:41:19 successfully verified block at path="/tmp/tmp.7h3rAq0Ay2/vm/1651518684-1651518984.bin", blockCount=20196
2023/03/08 16:41:19 Total time: 47.267605ms
Dump data uses VictoriaMetrics 1.77.2 native format
```

Depending on the result, import dumps that use VictoriaMetrics 1.77.2 into PMM 2.32 or lower. Import dumps that use VictoriaMetrics 1.82.1 into PMM 2.33 or higher.

To completely avoid this error, always export using JSON format (default starting from version 0.6.2).
