# Exporting Metrics

To export PMM metrics, use `pmm-dump export` command. By default, PMM Dump exports all performance metrics and **does not** export QAN data. PMM Dump supports multiple options that could be used to tune which data will be present in the resuling dump.

The following table lists all options applicable for the `export` command.

| Name                 | Value Type | Default                             | Description |
|----------------------|------------|-------------------------------------|-------------|
| help                 |        NaN |                                 NaN | Show context-sensitive help
| pmm-url              |     String |                                 NaN | PMM connection string, e.g. `--pmm-url=https://admin:admin@127.0.0.1:443`
| pmm-host             |     String |                                 NaN | PMM server host(with scheme), e.g. `--pmm-host=htps://127.0.0.1`
| pmm-port             |    Integer |                                 NaN | PMM server port
| pmm-user             |     String |                                 NaN | PMM credentials user
| pmm-pass             |     String |                                 NaN | PMM credentials password
| victoria-metrics-url |     String |                                 NaN | VictoriaMetrics connection string
| click-house-url      |     String |                                 NaN | ClickHouse connection string
| dump-core            |    Boolean |                                True | Export core metrics? To disable, specify option `no-dump-core`
| dump-qan             |    Boolean |                               False | Export QAN metrics?
| verbose (-v)         |    Boolean |                               False | Enable verbose mode
| allow-insecure-certs |    Boolean |                               False | Accept any certificate presented by the server and any host name in that certificate
| dump-path (-d)       |     String | pmm-dump-{CURRENT_TIMESTAMP}.tar.gz | Path to the dump file
| start-ts             |     String |         Current timestamp - 4 hours | Start date-time to filter exported metrics in RFC3339 format, e.g. 2023-01-02T15:04:05Z07:00
| end-ts               |     String |                   Current timestamp | End date-time to filter exported metrics in RFC3339 format, e.g. 2023-01-03T15:04:05Z07:00
| ts-selector          |     String |                                 NaN | Time series selector to pass to VictoriaMetrics. Allows to write customized queries to retrieve core metrics.
| where (-w)           |     String |                                 NaN | WHERE statement to pass to ClickHouse. Allows to write customized queries to retrieve QAN metrics.
| instance             |     String |                                 NaN | Service name to filter instances. Use multiple times to filter by multiple instances.
| dashboard            |     String |                                 NaN | Dashboard name to filter. Use multiple times to filter by multiple dashboards.
| chunk-time-range     |     String |                      5m (5 minutes) | Time range to be fit into a single chunk (core metrics). Example values: '45s' (45 seconds), '5m' (5 minutes), '1h' (1 hour). Affects time to export data and size of the resulting dump.
| chunk-rows           |    Integer |                                1000 | Amount of rows to fit into a single chunk (qan metrics). Affects time to export data and size of the resulting dump.
| ignore-load          |    Boolean |                               False | Disable checking for load threshold values
| max-load             |     String |              CPU=70,RAM=80,MYRAM=10 | Max load threshold values. For the CPU value is overall regardless cores count: 0-100%. When value of `max-load` is reached, `pmm-dump` stops executing and waits when resources are back to the specified values.
| critical-load        |     String |              CPU=90,RAM=90,MYRAM=30 | Critical load threshold values. For the CPU value is overall regardless cores count: 0-100%. When value of `critical-load` is reached, `pmm-dump` stops executing.
| stdout               |    Boolean |                               False | Redirect output to STDOUT
| workers              |    Integer |                 Number of CPU cores | The number of reading workers
| export-services-info |    Boolean |                               False | Export overview info about all the services, that are being monitored

