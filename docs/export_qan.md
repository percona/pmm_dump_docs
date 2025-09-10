# Exporting Query Analytics data

PMM Dump exports the most recent four hours of performance metrics and does not export Query Analytics (QAN) data unless the `--dump-qan` option is provided.

By default, PMM Dump reads QAN data from the ClickHouse database on port 9000. PMM does not publish this port by default; therefore, you can only export QAN data if you run PMM Dump on the same machine where the PMM server is running.

First, identify which host IP is assigned to your PMM server in Docker:

``` {.bash data-prompt="$" }
$ sudo docker inspect pmm-server | grep IPAddress
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAddress": "172.17.0.2",
```

!!! note

    You can parse JSON with the `jq` command:

    ``` {.bash data-prompt="$" }
    $ docker inspect pmm2-server | jq '.[0].NetworkSettings.IPAddress'
    "172.17.0.2"
    ```

Then specify this address, in our case `172.17.0.2`, in the `--pmm-url` option.

To export both performance metrics and QAN data, specify the `--dump-qan` option when running the tool:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url="http://admin:admin@172.17.0.2" --dump-qan
```

To export only QAN data and without exporting performance metrics, also specify the option `--no-dump-core`:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url="http://admin:admin@172.17.0.2" \
> --dump-qan --no-dump-core
```

!!! warning

    PMM Dump connects to the local ClickHouse instance and may not work if run on a different server than the one where PMM Server is installed.
