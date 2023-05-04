# Importing metrics

To import PMM metrics into local PMM instance, use the `pmm-dump import` command. By default, PMM Dump imports all performance metrics and **does not** import QAN data even if it exists in the dump file.

The following table lists all options applicable for the `import` command.

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
| dump-core            |    Boolean |                                True | Import core metrics? To disable, specify option `no-dump-core`
| dump-qan             |    Boolean |                               False | Import QAN metrics?
| verbose (-v)         |    Boolean |                               False | Enable verbose mode
| allow-insecure-certs |    Boolean |                               False | Accept any certificate presented by the server and any host name in that certificate
| dump-path (-d)       |     String | pmm-dump-{CURRENT_TIMESTAMP}.tar.gz | Path to the dump file
| workers              |    Integer |                 Number of CPU cores | The number of writing workers
