# Exporting Query Analytics Data

PMM Dump exports the most recent four hours of performance metrics and does not export Query Analytics (QAN) data unless option `--dump-qan` is provided.

PMM Dump reads QAN data from the ClickHouse database by default on port 9000. PMM does not publish this port by default, therefore you can only export QAN data if you run PMM Dump on the same machine where the PMM server is running.

First, identify which host IP docker is assigned to your PMM server:

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

Then specify this address, in our case `172.17.0.2`, in the option `--pmm-url`.

To export both performance metrics and QAN data, specify the option `--dump-qan` when running the tool:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url="http://admin:admin@172.17.0.2" --dump-qan
```

If you want to export only QAN data and do not export performance metrics, also specify the option `--no-dump-core`:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url="http://admin:admin@172.17.0.2" \
> --dump-qan --no-dump-core
```

!!! warning

    PMM Dump connects to the local ClickHouse instance and may not work if run on a different server than one where PMM Server is installed.
