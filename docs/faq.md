# Frequently Asked Questions

## How Can I Collect All Data for All Metrics and Instances?

By default, `pmm-dump` collects all information, available in VictoriaMetrics for the last 4 hours. This includes all metrics for all monitored services. Therefore, to obtain such a dump file, you should only specify command `export` and connection options.

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='https://admin:admin@127.0.0.1'
```

## When I Use Option `instance` I Get Only Information for the Database. How Can I get Information for the Operating System Too?

You do not get OS information, because OS metrics are recorded by other instance name. To export both metrics for the database and Operating System, specify option `instance` as many times as needed.

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='http://admin:admin@127.0.0.1' \
> --instance='sveta_mysql_8025' \
> --instance='sveta_os'
```
