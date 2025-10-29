# PMM Dump options

The following table lists all command-line options applicable within pmm-dump.

| Name                 | Scope  | Value Type | Default                             | Description |
|----------------------|--------|------------|-------------------------------------|-------------|
| allow-insecure-certs | Global |    Boolean |                                   False | Accept any certificate presented by the server and any host name in that certificate. |
| chunk-rows           | Export |    Integer |                                  100000 | Number of rows to fit into a single chunk (QAN metrics). Affects time to export data and size of the resulting dump. |
| chunk-time-range     | Export |     String |                          5m (5 minutes) | Time range to fit into a single chunk (core metrics). Example values: '45s' (45 seconds), '5m' (5 minutes), '1h' (1 hour). Affects time to export data and size of the resulting dump. |
| click-house-url      | Global |     String |                                    None | ClickHouse connection string, for example `clickhouse://default:clickhouse@172.19.0.4:9000/pmm` or `tcp://default:clickhouse@172.19.0.4:9000/pmm`. |
| critical-load        | Export |     String |                  CPU=90,RAM=90,MYRAM=30 | Critical load threshold values. For CPU, the value is overall regardless of cores count: 0-100%. When the value of `critical-load` is reached, `pmm-dump` stops executing. |
| dashboard            | Export |     String |                                    None | Dashboard name to filter. Use multiple times to filter by multiple dashboards. |
| dump-core            | Global |    Boolean |                                    True | Export/import core metrics. To disable, specify the option `no-dump-core`. |
| dump-path            | Global |     String | pmm-dump-{CURRENT_TIMESTAMP}.tar.gz.enc | Path to the dump file. |
| dump-qan             | Global |    Boolean |                                   False | Export/import QAN metrics. |
| encryption           | Global |    Boolean |                                    True | Enable encryption. |
| end-ts               | Export |     String |                       Current timestamp | End date-time to filter exported metrics in RFC3339 format, e.g. 2023-01-03T15:04:05Z07:00. |
| export-services-info | Export |    Boolean |                                   False | Export overview info about all the services that are being monitored. |
| force-pass-filepath  | Export |    Boolean |                                   False | Overwrite the file where the encrypted password is stored. |
| help                 | Global |    Boolean |                                    None | Show context-sensitive help. Output does not include command-specific options. |
| help-long            | Global |    Boolean |                                    None | Show context-sensitive help. Output includes command-specific options. |
| help-man             | Global |    Boolean |                                    None | Generates a man page for the help. |
| ignore-load          | Export |    Boolean |                                   False | Disable checking for load threshold values. |
| instance             | Export |     String |                                    None | Service name to filter instances. Use multiple times to filter by multiple names. |
| just-key             | Export |    Boolean |                                    True | Disable logging and only print the generated encryption key. |
| max-load             | Export |     String |                  CPU=70,RAM=80,MYRAM=10 | Max load threshold values. For CPU, the value is overall regardless of cores count: 0-100%. When the value of `max-load` is reached, `pmm-dump` stops executing and waits until resources are back to the specified values. |
| pass                 | Global |     String |                                    None | Encryption password. |
| pass-filepath        | Export |     String |                                    None | Filepath to output the generated encryption password. |
| pmm-cookie           | Global |     String |                                    None | PMM Auth cookie. |
| pmm-host             | Global |     String |                                    None | PMM server host (with scheme), e.g. `--pmm-host=https://127.0.0.1`. |
| pmm-pass             | Global |     String |                                    None | PMM password. |
| pmm-port             | Global |    Integer |                                    None | PMM server port. |
| pmm-token            | Global |     String |                                    None | PMM API token. |
| pmm-url              | Global |     String |                                    None | PMM connection string, e.g. `--pmm-url=https://admin:admin@127.0.0.1:443`. |
| pmm-user             | Global |     String |                                    None | PMM username. |
| prettify             |   Meta |    Boolean |                                    True | Print meta in human-readable format. To revert the value of this option, use the syntax `no-prettify`. |
| start-ts             | Export |     String |             Current timestamp - 4 hours | Start date-time to filter exported metrics in RFC3339 format, e.g. 2023-01-02T15:04:05Z07:00. |
| stdout               | Export |    Boolean |                                   False | Redirect output to STDOUT. |
| ts-selector          | Export |     String |                                    None | Time series selector to pass to VictoriaMetrics. Allows you to write customized queries to retrieve core metrics. |
| verbose              | Global |    Boolean |                                   False | Enable verbose mode. |
| victoria-metrics-url | Global |     String |                                    None | VictoriaMetrics connection string. |
| vm-content-limit     | Import |    Integer |                                       0 | Limit the chunk content size for VictoriaMetrics (in bytes). Doesn't work with native format. |
| vm-native-data       | Export |    Boolean |                                   False | Use VictoriaMetrics' native export format. Reduces dump size, but can be incompatible between PMM versions. |
| where (-w)           | Export |     String |                                    None | WHERE statement to pass to ClickHouse. Allows you to write customized queries to retrieve QAN metrics. |
| workers              | Export / Import |    Integer |            Number of CPU cores | The number of reading/writing workers.
