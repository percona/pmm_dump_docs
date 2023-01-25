# Troubleshooting

## General Issues

### How to Bypass SSL Errors During PMM Dump Export and Import

PMM Server uses self-signed certificates by default unless you replaced them with your own proper certificates as described [here](https://www.percona.com/doc/percona-monitoring-and-management/2.x/how-to/secure.html).

By default PMM Dump expects that certificates for the HTTPS connection should be trusted and fails with error when connects to PMM:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='https://admin:admin@127.0.0.1' 
2021-10-08T13:19:29Z FTL Failed to compose meta error="failed to get PMM version: x509: cannot validate certificate for 127.0.0.1 because it doesn't contain any IP SANs"
```

If you want to continue using self-signed certificates you can run PMM Dump with the option `--allow-insecure-certs` that would allow the tool to continue even if the certificate is not trusted:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='https://admin:admin@127.0.0.1' --allow-insecure-certs
2021-10-08T13:25:45Z INF Exporting metrics…
...
```

## Export Issues

### How to Bypass Error "Failed to create ClickHouse source" when Exporting Query Analytics Data

When you try to export Query Analytics (QAN) data with PMM Dump it may fail with an error "Failed to create ClickHouse source".

PMM Server stores QAN data in the ClickHouse server that listens on port 9000. Unlike ports for HTTP and HTTPS connections that are published when you install a PMM Server, the ClickHouse port is only exposed by Docker and not published. This means that while you can connect to your PMM server using your machine hostname and IP address, port 9000 cannot be accessed this way.

Therefore, if you point `--pmm-url` option to the IP address of your machine or even localhost you would not be able to export QAN data:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='http://admin:admin@127.0.0.1' --dump-qan
2021-10-09T13:14:51Z FTL Failed to create ClickHouse source: dial tcp 127.0.0.1:9000: connect: connection refused
```

However, you can access ClickHouse if you use the IP that Docker assigns to your PMM Server. If you do not know this IP address, run the `docker inspect` command and search for the `IPAddress` value in the container `NetworkSettings`. Once you found the IP address that Docker assigned your PMM Server container you can use it to export QAN. See [Exporting Query Analytics Data](export_qan.md) for more details.

An alternative solution would be publishing port 9000 at the time when you create a PMM Server container but we do not recommend it, because doing so opens outside access to your raw queries and is not secure.

## Import Issues
