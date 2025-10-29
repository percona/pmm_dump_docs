# Exporting Query Analytics data

PMM Dump exports the most recent four hours of performance metrics and does not export Query Analytics (QAN) data unless the `--dump-qan` option is provided.

By default, PMM Dump reads QAN data from the ClickHouse database on port 9000. PMM does not publish this port by default; therefore, you can only export QAN data if you run PMM Dump on the same machine where the PMM server is running.

If you are using PMM 3 or newer, ClickHouse does not allow to connect outside of the container. If you are using PMM Dump, [bundled with PMM](https://docs.percona.com/percona-monitoring-and-management/3/troubleshoot/pmm_dump.html), this should not be a problem. If you are using PMM Dump externally, you need to adjust ClickHouse configuration in order to access QAN data.

## Prepare ClickHouse for accessing externally

### Allow connections outside of the Docker container

Uncomment entry `<listen_host>0.0.0.0</listen_host>` in the ClickHouse configuration file, then restart ClickHouse server:

``` {.bash data-prompt="$" }
$ docker exec pmm-server-3 sed -i 's#<!-- <listen_host>0.0.0.0</listen_host> -->#<listen_host>0.0.0.0</listen_host>#g' /etc/clickhouse-server/config.xml
$ docker exec pmm-server-3 supervisorctl restart clickhouse
clickhouse: stopped
clickhouse: started

```

### Identify which host IP is assigned to your PMM server in Docker:

``` {.bash data-prompt="$" }
$ sudo docker inspect pmm-server | grep IPAddress
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAddress": "172.17.0.2",
```

!!! note

    You can parse JSON with the `jq` command:

    ``` {.bash data-prompt="$" }
    $ docker inspect pmm-server | jq '.[0].NetworkSettings.IPAddress'
    "172.17.0.2"
    ```

    If you created a Docker network for PMM, use following parameters for the `jq` command:

    ``` {.bash data-prompt="$" }
    $ docker inspect pmm-server | jq '.[0].NetworkSettings.Networks."pmm-network".IPAddress'
    "172.17.0.2"
    ```

    Replace `pmm-network` with the name of your network.

## Dump QAN data

Specify the host IP that is assigned to your PMM server in Docker in the `--pmm-url` option. In our example, this is `172.17.0.2`.

To export both performance metrics and QAN data, specify the `--dump-qan` option when running the tool:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url="http://admin:admin@172.17.0.2" --dump-qan
```

To export only QAN data without exporting performance metrics, also specify the option `--no-dump-core`:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url="http://admin:admin@172.17.0.2" \
> --dump-qan --no-dump-core
```

!!! note

    If you publish port 9000 when create PMM Server container, you may access QAN using the same address as when connecting to PMM. However, this will create a risk of exposing your queries to an attacker in case if someone gains access to your PMM Server host.

    To publish port 9000, add option `--publish 9000:9000` to your `docker run` command.
