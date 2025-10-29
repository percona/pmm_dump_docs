# Frequently Asked Questions

## How can I collect all data for all metrics and instances?

By default, `pmm-dump` collects all information available in VictoriaMetrics for the last 4 hours. This includes all metrics for all monitored services. Therefore, to obtain such a dump file, you should only specify the `export` command and connection options.

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='https://admin:admin@127.0.0.1'
```

## When I use the `--instance` option, I get only information for the database. How can I get information for the operating system too?

You do not get OS information because OS metrics are recorded under a different instance name. To export both database and operating system metrics, specify the `--instance` option as many times as needed.

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='http://admin:admin@127.0.0.1' \
> --instance='sveta_mysql_8025' \
> --instance='sveta_os'
```
## How do I decrypt an encrypted dump file?

Usually you do not need to decrypt the dump file. `pmm-dump` will do this for you when importing data. However, you can decrypt the dump with `openssl` using the command below.

``` {.bash data-prompt="$" }
$ openssl enc -d -aes-256-ctr -pbkdf2 -in dump.tar.gz.enc -out dump.tar.gz
```