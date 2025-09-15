# Advanced filtering

PMM can store a lot of data and it could be impractical to export all this data. To resolve this issue, PMM Dump supports filtering options. Thus, to export a specific instance, use the `--instance` option. To export a particular dashboard, use the `--dashboard` option. To specify a custom time range for the exported data, use the options `--start-ts` and `--end-ts`. If you need even better control of the dump file content, use advanced filtering options such as `--ts-selector` and `--where`.

## Advanced filtering for performance metrics

PMM Dump can query VictoriaMetrics via the Prometheus export API accessible via `https://YOUR_PMM_URL/prometheus/api/v1/export/native`. This API supports the PromQL-based query language and you can use complex expressions to filter data. Use the option `--ts-selector='{PromQL_EXPRESSION}'` to query the VictoriaMetrics instance inside PMM.

For example, to export all data for two clusters: `cluster1` and `cluster2`, use the following command:

``` {.bash data-prompt="$" }
$ pmm-dump export \
> --pmm-url='http://admin:admin@127.0.0.1' \
> --ts-selector='{node_name= "<cluster1>|<cluster2>"}'
```

You will find more information on the MetricsQL query language in the [MetricsQL user reference manual](https://docs.victoriametrics.com/MetricsQL.html).

## Advanced filtering for Query Analytics (QAN) data

QAN stores its data in the ClickHouse database, in the table metrics. To query the metrics table in the ClickHouse database, specify the option `--where="YOUR_QUERY"`.

For example, to export only data for queries that start with `SELECT *`, use the following command:

``` {.bash data-prompt="$" }
$ pmm-dump export --dump-qan\
> --pmm-url='http://admin:admin@172.17.0.2' \
> --where="fingerprint LIKE ' SELECT * '"
```

You will find details on how to use the ClickHouse SQL dialect in the [user reference manual](https://clickhouse.com/docs/en/sql-reference/syntax/).



