# PMM Dump Commands

PMM Dump supports following commands.

## `help`

Print help message and exit.

``` {.bash data-prompt="$" }
$ ./pmm-dump --help
usage: pmm-dump [<flags>] <command> [<args> ...]

Percona PMM Dump

Flags:
      --help                  Show context-sensitive help (also try --help-long and --help-man).
      --pmm-url=PMM-URL       PMM connection string
      --pmm-host=PMM-HOST     PMM server host(with scheme)
      --pmm-port=PMM-PORT     PMM server port
      --pmm-user=PMM-USER     PMM credentials user
      --pmm-pass=PMM-PASS     PMM credentials password
      --victoria-metrics-url=VICTORIA-METRICS-URL  
                              VictoriaMetrics connection string
      --click-house-url=CLICK-HOUSE-URL  
                              ClickHouse connection string
      --dump-core             Specify to export/import core metrics
      --dump-qan              Specify to export/import QAN metrics
  -v, --verbose               Enable verbose mode
      --allow-insecure-certs  Accept any certificate presented by the server and any host name in that certificate
  -d, --dump-path=DUMP-PATH   Path to dump file
      --workers=WORKERS       Set the number of reading workers

Commands:
  help [<command>...]
    Show help.

  export [<flags>]
    Export PMM Server metrics to dump file.By default only the 4 last hours are exported, but it can be configured via start-ts/end-ts options

  import
    Import PMM Server metrics from dump file

  show-meta [<flags>]
    Shows metadata from the specified dump file

  version
    Shows tool version of the binary
```

To print usage information for the specific option use syntax `pmm-dump help [<command>]`.

``` {.bash data-prompt="$" }
$ ./pmm-dump --help export
usage: pmm-dump export [<flags>]

Export PMM Server metrics to dump file.By default only the 4 last hours are exported, but it can be configured via start-ts/end-ts options

Flags:
      --help                     Show context-sensitive help (also try --help-long and --help-man).
      --pmm-url=PMM-URL          PMM connection string
      --pmm-host=PMM-HOST        PMM server host(with scheme)
      --pmm-port=PMM-PORT        PMM server port
      --pmm-user=PMM-USER        PMM credentials user
      --pmm-pass=PMM-PASS        PMM credentials password
      --victoria-metrics-url=VICTORIA-METRICS-URL  
                                 VictoriaMetrics connection string
      --click-house-url=CLICK-HOUSE-URL  
                                 ClickHouse connection string
      --dump-core                Specify to export/import core metrics
      --dump-qan                 Specify to export/import QAN metrics
  -v, --verbose                  Enable verbose mode
      --allow-insecure-certs     Accept any certificate presented by the server and any host name in that certificate
  -d, --dump-path=DUMP-PATH      Path to dump file
      --workers=WORKERS          Set the number of reading workers
      --start-ts=START-TS        Start date-time to filter exported metrics, ex. 2006-01-02T15:04:05Z07:00
      --end-ts=END-TS            End date-time to filter exported metrics, ex. 2006-01-02T15:04:05Z07:00
      --ts-selector=TS-SELECTOR  Time series selector to pass to VM
  -w, --where=WHERE              ClickHouse only. WHERE statement
      --instance=INSTANCE ...    Service name to filter instances. Use multiple times to filter by multiple instances
      --dashboard=DASHBOARD ...  Dashboard name to filter. Use multiple times to filter by multiple dashboards
      --chunk-time-range=5m      Time range to be fit into a single chunk (core metrics). 5 minutes by default, example '45s', '5m', '1h'
      --chunk-rows=1000          Amount of rows to fit into a single chunk (qan metrics)
      --ignore-load              Disable checking for load threshold values
      --max-load="CPU=70,RAM=80,MYRAM=10"  
                                 Max load threshold values. For the CPU value is overall regardless cores count: 0-100%
      --critical-load="CPU=90,RAM=90,MYRAM=30"  
                                 Critical load threshold values. For the CPU value is overall regardless cores count: 0-100%
      --stdout                   Redirect output to STDOUT
      --export-services-info     Export overview info about all the services, that are being monitored
      --vm-native-data           Use VictoriaMetrics' native export format. Reduces dump size, but can be incompatible between PMM versions
```

## `export`

Export PMM Server metrics to dump file. By default the 4 last hours of all performance metrics, excluding QAN, exported. But this behavior could be overwritten with options.

For more details see [Export](export.md).

## `import`

Import PMM Server metrics from dump file.

For more details see [Import](import.md).

## `show-meta`

Show metadata from the specified dump file.

``` {.bash data-prompt="$" }
$ ./pmm-dump show-meta -d pmm-dump-1678279503.tar.gz 
Build: 87cc678
PMM Version: 2.35.0-20.2302220742.5e80fd1.el7
Max Chunk Size: 2.7 MB (2.6 MiB)
Arguments: export --pmm-host=http://172.17.0.2 --pmm-user=*** --pmm-pass=*** --pmm-port=80 --ignore-load=true
```

By default, `pmm-dump` prints meta information in human-readable format. If you need output in JSON format, use option `--no-prettify`:

``` {.bash data-prompt="$" }
$ ./pmm-dump show-meta -d pmm-dump-1678279503.tar.gz --no-prettify  
{
	"version": {
		"git-branch": "dev/tests",
		"git-commit": "87cc678"
	},
	"pmm-server-version": "2.35.0-20.2302220742.5e80fd1.el7",
	"max_chunk_size": 2732148,
	"pmm-server-timezone": null,
	"arguments": "export --pmm-host=http://172.17.0.2 --pmm-user=*** --pmm-pass=*** --pmm-port=80 --ignore-load=true",
	"vm-data-format": "json"
}
```

## `version`

Show version number and GitHub commit hash.

``` {.bash data-prompt="$" }
$ ./pmm-dump version
Version: v2.35.0, Build: 87cc678
```
