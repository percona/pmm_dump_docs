# Importing Query Analytics data

PMM Dump does not import Query Analytics (QAN) data even if it exists in the dump file unless the `--dump-qan` option is provided.

To import both performance metrics and QAN data, specify the `--dump-qan` option when running the tool:

``` {.bash data-prompt="$" }
$ pmm-dump import --pmm-url="http://admin:admin@172.17.0.2" --dump-qan --pass=****************
```

To import only QAN data and without importing performance metrics, also specify the option `--no-dump-core`:

``` {.bash data-prompt="$" }
$ pmm-dump import --pmm-url="http://admin:admin@172.17.0.2" \
> --dump-qan --no-dump-core --pass=****************
```