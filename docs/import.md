# Importing metrics

To import PMM metrics into a local PMM instance, use the `pmm-dump import` command. By default, PMM Dump imports all performance metrics and **does not** import QAN data even if it exists in the dump file.

The following table lists all options applicable for the `import` command.

| Name                 | Value Type | Default                             | Description |
|----------------------|------------|-------------------------------------|-------------|
| allow-insecure-certs |    Boolean |                               False | Accept any certificate presented by the server and any host name in that certificate |
| click-house-url      |     String |                                None | ClickHouse connection string, for example `clickhouse://default:clickhouse@172.19.0.4:9000/pmm` or `tcp://default:clickhouse@172.19.0.4:9000/pmm` |
| dump-core            |    Boolean |                                True | Import core metrics? To disable, specify option `no-dump-core` |
| dump-path (-d)       |     String | pmm-dump-{CURRENT_TIMESTAMP}.tar.gz | Path to the dump file |
| dump-qan             |    Boolean |                               False | Import QAN metrics? |
| encryption           |    Boolean |                               False | Enable encryption
| help                 |    Boolean |                                None | Show context-sensitive help |
| pass                 |     String |                                None | Encryption password
| pmm-cookie           |     String |                                None | PMM Auth cookie
| pmm-host             |     String |                                None | PMM server host (with scheme), e.g. `--pmm-host=https://127.0.0.1` |
| pmm-pass             |     String |                                None | PMM credentials password |
| pmm-port             |    Integer |                                None | PMM server port |
| pmm-token            |     String |                                None | PMM API token
| pmm-url              |     String |                                None | PMM connection string, e.g. `--pmm-url=https://admin:admin@127.0.0.1:443` |
| pmm-user             |     String |                                None | PMM credentials user |
| verbose (-v)         |    Boolean |                               False | Enable verbose mode |
| victoria-metrics-url |     String |                                None | VictoriaMetrics connection string |
| vm-content-limit     |    Integer |                                   0 | Limit the chunk content size for VictoriaMetrics (in bytes). Doesn't work with native format. |
| vm-native-data       |    Boolean |                               False | Use VictoriaMetrics' native export format
| workers              |    Integer |                 Number of CPU cores | The number of writing workers
