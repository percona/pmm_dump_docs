# PMM Dump Options

The following table lists all command-line options applicable within pmm-dump.

| Name                 | Scope  | Value Type | Default                             | Description |
|----------------------|--------|------------|-------------------------------------|-------------|
| help                 | Global |        NaN |                                 NaN | Show content-sensitive help. |
| help-long            | Global |        NaN |                                 NaN |  |
| help-man             | Global |        NaN |                                 NaN |  |
| pmm-url              | Global |     String |                                 NaN | PMM connection string, e.g. `--pmm-url=https://admin:admin@127.0.0.1:443` |
| pmm-host             | Global |     String |                                 NaN | PMM server host (with scheme), e.g. `--pmm-host=htps://127.0.0.1` |
| pmm-port             | Global |    Integer |                                 NaN | PMM server port |
| pmm-user             | Global |     String |                                 NaN | PMM username |
| pmm-pass             | Global |     String |                                 NaN | PMM password |
| victoria-metrics-url | Global |     String |                                 NaN | VictoriaMetrics connection string |
| click-house-url      | Global |     String |                                 NaN | ClickHouse connection string |
| dump-core            | Global |    Boolean |                                True | Export/import core metrics. To disable, specify option `no-dump-core` |
| dump-qan             | Global |    Boolean |                               False | Export/import QAN metrics |
| verbose              | Global |    Boolean |                               False | Enable verbose mode |
| allow-insecure-certs | Global |    Boolean |                               False | Accept any certificate presented by the server and any host name in that certificate |
| dump-path            | Global |     String | pmm-dump-{CURRENT_TIMESTAMP}.tar.gz | Path to the dump file
| start-ts             | Export |     String |         Current timestamp - 4 hours | Start date-time to filter exported metrics in RFC3339 format, e.g. 2023-01-02T15:04:05Z07:00
| end-ts               | Export |     String |                   Current timestamp | End date-time to filter exported metrics in RFC3339 format, e.g. 2023-01-03T15:04:05Z07:00
| ts-selector          | Export |     String |                                 NaN | Time series selector to pass to VictoriaMetrics. Allows to write customized queries to retrieve core metrics.
| where (-w)           | Export |     String |                                 NaN | WHERE statement to pass to ClickHouse. Allows to write customized queries to retrieve QAN metrics.
| instance             | Export |     String |                                 NaN | Service name to filter instances. Use multiple times to filter by multiple instances.
| dashboard            | Export |     String |                                 NaN | Dashboard name to filter. Use multiple times to filter by multiple dashboards.
| chunk-time-range     | Export |     String |                      5m (5 minutes) | Time range to be fit into a single chunk (core metrics). Example values: '45s' (45 seconds), '5m' (5 minutes), '1h' (1 hour). Affects time to export data and size of the resulting dump.
| chunk-rows           | Export |    Integer |                                1000 | Amount of rows to fit into a single chunk (qan metrics). Affects time to export data and size of the resulting dump.
| ignore-load          | Export |    Boolean |                               False | Disable checking for load threshold values
| max-load             | Export |     String |              CPU=70,RAM=80,MYRAM=10 | Max load threshold values. For the CPU value is overall regardless cores count: 0-100%. When value of `max-load` is reached, `pmm-dump` stops executing and waits when resources are back to the specified values.
| critical-load        | Export |     String |              CPU=90,RAM=90,MYRAM=30 | Critical load threshold values. For the CPU value is overall regardless cores count: 0-100%. When value of `critical-load` is reached, `pmm-dump` stops executing.
| stdout               | Export |    Boolean |                               False | Redirect output to STDOUT
| workers              | Export / Import |    Integer |                 Number of CPU cores | The number of reading/writing workers
| export-services-info | Export |    Boolean |                               False | Export overview info about all the services, that are being monitored
| vm-native-data       | Export |    Boolean |                               False | Use VictoriaMetrics' native export format. Reduces dump size, but can be incompatible between PMM versions
| prettify             |   Meta |    Boolean |                                True | Print meta in human readable format. To revert value of this option, use syntax `no-prettify`
