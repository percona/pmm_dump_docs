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
| dump-core            | Global |    Boolean |                                True | Export/import core metrics |
| dump-qan             | Global |    Boolean |                               False | Export/import QAN metrics |
| verbose              | Global |    Boolean |                               False | Enable verbose mode |
| allow-insecure-certs | Global |    Boolean |                               False | Accept any certificate presented by the server and any host name in that certificate |
| dump-path            | Global |     String | pmm-dump-{CURRENT_TIMESTAMP}.tar.gz | Path to the dump file
