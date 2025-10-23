# Exporting metrics

To export PMM metrics, use the `pmm-dump export` command. By default, PMM Dump exports all performance metrics and **does not** export QAN data. PMM Dump supports multiple options that can be used to tune which data will be present in the resulting dump.

The following table lists all options applicable for the `export` command.

| Name                 | Value Type | Default                             | Description |
|----------------------|------------|-------------------------------------|-------------|
| allow-insecure-certs |    Boolean |                               False | Accept any certificate presented by the server and any host name in that certificate
| chunk-rows           |    Integer |                                1000 | Amount of rows to fit into a single chunk (QAN metrics). Affects time to export data and size of the resulting dump.
| chunk-time-range     |     String |                      5m (5 minutes) | Time range to be fit into a single chunk (core metrics). Example values: '45s' (45 seconds), '5m' (5 minutes), '1h' (1 hour). Affects time to export data and size of the resulting dump.
| click-house-url      |     String |                                None | ClickHouse connection string
| critical-load        |     String |              CPU=90,RAM=90,MYRAM=30 | Critical load threshold values. For the CPU value, it is overall regardless of cores count: 0-100%. When the value of `critical-load` is reached, `pmm-dump` stops executing.
| dashboard            |     String |                                None | Dashboard name to filter. Use multiple times to filter by multiple dashboards.
| dump-core            |    Boolean |                                True | Export core metrics? To disable, specify option `no-dump-core`
| dump-path (-d)       |     String | pmm-dump-{CURRENT_TIMESTAMP}.tar.gz | Path to the dump file
| dump-qan             |    Boolean |                               False | Export QAN metrics?
| encryption           |    Boolean |                                True | Enable encryption
| end-ts               |     String |                   Current timestamp | End date-time to filter exported metrics in RFC3339 format, e.g. 2023-01-03T15:04:05Z07:00
| export-services-info |    Boolean |                               False | Export overview info about all the services that are being monitored
| force-pass-filepath  |    Boolean |                               False | Overwrite the file where the encrypted password is stored
| help                 |    Boolean |                               False | Show context-sensitive help
| ignore-load          |    Boolean |                               False | Disable checking for load threshold values
| instance             |     String |                                None | Service name to filter instances. Use multiple times to filter by multiple instances.
| just-key             |    Boolean |                                True | Disable logging and print only generated encryption key
| max-load             |     String |              CPU=70,RAM=80,MYRAM=10 | Max load threshold values. For the CPU value, it is overall regardless of cores count: 0-100%. When the value of `max-load` is reached, `pmm-dump` stops executing and waits until resources are back to the specified values.
| pass                 |     String |                                None | Encryption password
| pass-filepath        |     String |                                None | File path where the generated password needs to be stored
| pmm-cookie           |     String |                                None | PMM Auth cookie
| pmm-host             |     String |                                None | PMM server host (with scheme), e.g. `--pmm-host=https://127.0.0.1`
| pmm-pass             |     String |                                None | PMM credentials password
| pmm-port             |    Integer |                                None | PMM server port
| pmm-token            |     String |                                None | PMM API token
| pmm-url              |     String |                                None | PMM connection string, e.g. `--pmm-url=https://admin:admin@127.0.0.1:443`
| pmm-user             |     String |                                None | PMM credentials user
| start-ts             |     String |         Current timestamp - 4 hours | Start date-time to filter exported metrics in RFC3339 format, e.g. 2023-01-02T15:04:05Z07:00
| stdout               |    Boolean |                               False | Redirect output to STDOUT
| ts-selector          |     String |                                None | Time series selector to pass to VictoriaMetrics. Allows you to write customized queries to retrieve core metrics.
| verbose (-v)         |    Boolean |                               False | Enable verbose mode
| victoria-metrics-url |     String |                                None | VictoriaMetrics connection string
| vm-native-data       |    Boolean |                               False | Use VictoriaMetrics' native export format. Reduces dump size, but can be incompatible between PMM versions
| where (-w)           |     String |                                None | WHERE statement to pass to ClickHouse. Allows you to write customized queries to retrieve QAN metrics.
| workers              |    Integer |                 Number of CPU cores | The number of reading workers

