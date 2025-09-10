# PMM Dump Commands

PMM Dump supports the following commands.

## `help`

Prints help message and exits.

``` {.bash data-prompt="$" }
$ pmm-dump --help
usage: pmm-dump [<flags>] <command> [<args> ...]

Percona PMM Dump


Flags:
      --[no-]help              Show context-sensitive help (also try --help-long and --help-man). ($PMM_DUMP_HELP)
      --pmm-url=PMM-URL        PMM connection string ($PMM_URL)
      --pmm-host=PMM-HOST      PMM server host(with scheme) ($PMM_HOST)
      --pmm-port=PMM-PORT      PMM server port ($PMM_PORT)
      --pmm-user=PMM-USER      PMM credentials user ($PMM_USER)
      --pmm-token=PMM-TOKEN    PMM API token ($PMM_TOKEN)
      --pmm-cookie=PMM-COOKIE  PMM Auth cookie ($PMM_COOKIE)
      --pmm-pass=PMM-PASS      PMM credentials password ($PMM_PASS)
      --victoria-metrics-url=VICTORIA-METRICS-URL  
                               VictoriaMetrics connection string ($PMM_DUMP_VICTORIA_METRICS_URL)
      --click-house-url=CLICK-HOUSE-URL  
                               ClickHouse connection string ($PMM_DUMP_CLICK_HOUSE_URL)
      --[no-]dump-core         Specify to export/import core metrics ($PMM_DUMP_DUMP_CORE)
      --[no-]dump-qan          Specify to export/import QAN metrics ($PMM_DUMP_DUMP_QAN)
  -v, --[no-]verbose           Enable verbose mode ($PMM_DUMP_VERBOSE)
      --[no-]allow-insecure-certs  
                               Accept any certificate presented by the server and any host name in that certificate ($PMM_DUMP_ALLOW_INSECURE_CERTS)
  -d, --dump-path=DUMP-PATH    Path to dump file ($PMM_DUMP_DUMP_PATH)
      --workers=WORKERS        Set the number of reading workers ($PMM_DUMP_WORKERS)
      --[no-]vm-native-data    Use VictoriaMetrics' native export format. Reduces dump size, but can be incompatible between PMM versions ($PMM_DUMP_VM_NATIVE_DATA)
      --[no-]encryption        Enable encryption ($PMM_DUMP_ENCRYPTION)
      --pass=PASS              Password for encryption/decryption ($PMM_DUMP_PASS)
      --[no-]just-key          Disable logging and only leave key ($PMM_DUMP_JUST_KEY)
      --pass-filepath=PASS-FILEPATH  
                               Filepath to output encryption password ($PMM_DUMP_PASS_FILEPATH)

Commands:
help [<command>...]
    Show help.

export [<flags>]
    Export PMM Server metrics to dump file.By default only the 4 last hours are exported, but it can be configured via start-ts/end-ts options

import [<flags>]
    Import PMM Server metrics from dump file

show-meta [<flags>]
    Shows metadata from the specified dump file

version
    Shows tool version of the binary
```

To print usage information for the specific option use syntax `pmm-dump help [<command>]`.

``` {.bash data-prompt="$" }
$ pmm-dump --help export
usage: pmm-dump export [<flags>]

Export PMM Server metrics to dump file.By default only the 4 last hours are exported, but it can be configured via start-ts/end-ts options


Flags:
      --[no-]help                Show context-sensitive help (also try --help-long and --help-man). ($PMM_DUMP_HELP)
      --pmm-url=PMM-URL          PMM connection string ($PMM_URL)
      --pmm-host=PMM-HOST        PMM server host(with scheme) ($PMM_HOST)
      --pmm-port=PMM-PORT        PMM server port ($PMM_PORT)
      --pmm-user=PMM-USER        PMM credentials user ($PMM_USER)
      --pmm-token=PMM-TOKEN      PMM API token ($PMM_TOKEN)
      --pmm-cookie=PMM-COOKIE    PMM Auth cookie ($PMM_COOKIE)
      --pmm-pass=PMM-PASS        PMM credentials password ($PMM_PASS)
      --victoria-metrics-url=VICTORIA-METRICS-URL  
                                 VictoriaMetrics connection string ($PMM_DUMP_VICTORIA_METRICS_URL)
      --click-house-url=CLICK-HOUSE-URL  
                                 ClickHouse connection string ($PMM_DUMP_CLICK_HOUSE_URL)
      --[no-]dump-core           Specify to export/import core metrics ($PMM_DUMP_DUMP_CORE)
      --[no-]dump-qan            Specify to export/import QAN metrics ($PMM_DUMP_DUMP_QAN)
  -v, --[no-]verbose             Enable verbose mode ($PMM_DUMP_VERBOSE)
      --[no-]allow-insecure-certs  
                                 Accept any certificate presented by the server and any host name in that certificate ($PMM_DUMP_ALLOW_INSECURE_CERTS)
  -d, --dump-path=DUMP-PATH      Path to dump file ($PMM_DUMP_DUMP_PATH)
      --workers=WORKERS          Set the number of reading workers ($PMM_DUMP_WORKERS)
      --[no-]vm-native-data      Use VictoriaMetrics' native export format. Reduces dump size, but can be incompatible between PMM versions ($PMM_DUMP_VM_NATIVE_DATA)
      --[no-]encryption          Enable encryption ($PMM_DUMP_ENCRYPTION)
      --pass=PASS                Password for encryption/decryption ($PMM_DUMP_PASS)
      --[no-]just-key            Disable logging and only leave key ($PMM_DUMP_JUST_KEY)
      --pass-filepath=PASS-FILEPATH  
                                 Filepath to output encryption password ($PMM_DUMP_PASS_FILEPATH)
      --start-ts=START-TS        Start date-time to filter exported metrics, ex. 2006-01-02T15:04:05Z07:00 ($PMM_DUMP_START_TS)
      --end-ts=END-TS            End date-time to filter exported metrics, ex. 2006-01-02T15:04:05Z07:00 ($PMM_DUMP_END_TS)
      --ts-selector=TS-SELECTOR  Time series selector to pass to VM ($PMM_DUMP_TS_SELECTOR)
  -w, --where=WHERE              ClickHouse only. WHERE statement ($PMM_DUMP_WHERE)
      --instance=INSTANCE ...    Name to filter instances by service names, node names, or instance names. Use multiple times to filter by multiple names ($PMM_DUMP_INSTANCE)
      --dashboard=DASHBOARD ...  Dashboard name to filter. Use multiple times to filter by multiple dashboards ($PMM_DUMP_DASHBOARD)
      --chunk-time-range=5m      Time range to be fit into a single chunk (core metrics). 5 minutes by default, example '45s', '5m', '1h' ($PMM_DUMP_CHUNK_TIME_RANGE)
      --chunk-rows=100000        Amount of rows to fit into a single chunk (qan metrics) ($PMM_DUMP_CHUNK_ROWS)
      --[no-]ignore-load         Disable checking for load threshold values ($PMM_DUMP_IGNORE_LOAD)
      --max-load="CPU=70,RAM=80,MYRAM=10"  
                                 Max load threshold values. For the CPU value is overall regardless cores count: 0-100% ($PMM_DUMP_MAX_LOAD)
      --critical-load="CPU=90,RAM=90,MYRAM=30"  
                                 Critical load threshold values. For the CPU value is overall regardless cores count: 0-100% ($PMM_DUMP_CRITICAL_LOAD)
      --[no-]stdout              Redirect output to STDOUT ($PMM_DUMP_STDOUT)
      --[no-]export-services-info  
                                 Export overview info about all the services, that are being monitored ($PMM_DUMP_EXPORT_SERVICES_INFO)
```

## `export`

Export PMM Server metrics to dump file. By default, the last 4 hours of all performance metrics, excluding QAN, are exported. But this behavior can be overridden with options.

For more details, see [Export](export.md).

## `import`

Imports PMM Server metrics from dump file.

For more details, see [Import](import.md).

## `show-meta`

Shows metadata from the specified dump file.

``` {.bash data-prompt="$" }
$ pmm-dump show-meta -d pmm-dump-1757934088.tar.gz.enc --pass=****************
Build: 1fc721f
PMM Version: 3.3.0
Max Chunk Size: 1.5 MB (1.4 MiB)
Arguments: export --pmm-url=https://127.0.0.1 --allow-insecure-certs=true
```

By default, `pmm-dump` prints meta information in human-readable format. If you need output in JSON format, use the option `--no-prettify`:

``` {.bash data-prompt="$" }
$ pmm-dump show-meta -d pmm-dump-1757934088.tar.gz.enc --pass=**************** --no-prettify
{
	"version": {
		"git-branch": "main",
		"git-commit": "1fc721f"
	},
	"pmm-server-version": "3.3.0",
	"max_chunk_size": 1480262,
	"pmm-server-timezone": null,
	"arguments": "export --pmm-url=https://127.0.0.1 --allow-insecure-certs=true",
	"vm-data-format": "json"
}
```

## `version`

Shows version number and GitHub commit hash.

``` {.bash data-prompt="$" }
$ pmm-dump version
Version: v0.7.1-ga, Build: d568d7d
```
