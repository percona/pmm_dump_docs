# Using PMM Dump

## Exporting data

PMM Dump exports collected metrics from a PMM instance into a tarball file. By default, the name of the resulting file is `pmm-dump-{UNIX_TIMESTAMP}.tar.gz.enc`.

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='https://*****:*****@127.0.0.1' --allow-insecure-certs --no-just-key
2025-09-16T13:04:50+03:00 INF Credential user was obtained from pmm-url
2025-09-16T13:04:50+03:00 INF Credential password was obtained from pmm-url
2025-09-16T13:04:50+03:00 INF Exporting metrics...
2025-09-16T13:04:50+03:00 INF Processing 1/49 chunk...
2025-09-16T13:04:50+03:00 INF start: 2025-09-16T06:04:50.011Z
2025-09-16T13:04:50+03:00 INF Processing 2/49 chunk...
2025-09-16T13:04:50+03:00 INF end: 2025-09-16T06:09:50.011Z
...
2025-09-16T13:04:50+03:00 INF Writing chunk to the dump... filename=1758016490-1758016790.bin source=vm
2025-09-16T13:04:50+03:00 INF Writing chunk to the dump... filename=1758016190-1758016490.bin source=vm
2025-09-16T13:04:50+03:00 INF Writing chunk to the dump... filename=1758017090-1758017390.bin source=vm
2025-09-16T13:04:50+03:00 INF Writing chunk to the dump... filename=1758016790-1758017090.bin source=vm
2025-09-16T13:04:50+03:00 INF Password: ****************
2025-09-16T13:04:50+03:00 INF Successfully exported!
$ ls pmm-dump-*
pmm-dump-1758017090.tar.gz.enc
```
This command exports all performance metrics collected in the last 4 hours and encrypts them with an auto-generated password.

!!! warning
    
    PMM Dump will not export QAN data unless the option `--dump-qan` is specified.

## Importing data

To import data, start a new PMM instance and run the `pmm-dump import` command:

``` {.bash data-prompt="$" }
$ pmm-dump import --pmm-url='https://admin:adminadmin@127.0.0.1' --allow-insecure-certs \
> --dump-path=pmm-dump-1758017090.tar.gz.enc --pass=****************
2025-09-16T13:06:47+03:00 INF Credential user was obtained from pmm-url
2025-09-16T13:06:47+03:00 INF Credential password was obtained from pmm-url
2025-09-16T13:06:47+03:00 INF Opening dump file... path=pmm-dump-1758017090.tar.gz.enc
2025-09-16T13:06:48+03:00 INF Importing metrics...
2025-09-16T13:06:48+03:00 INF Processing chunk 'vm/1758002690-1758002990.bin'...
2025-09-16T13:06:48+03:00 WRN Chunk 'vm/1758002690-1758002990.bin' is empty, skipping
2025-09-16T13:06:48+03:00 INF Processing chunk 'vm/1758002990-1758003290.bin'...
2025-09-16T13:06:48+03:00 WRN Chunk 'vm/1758002990-1758003290.bin' is empty, skipping
...
2025-09-16T13:06:48+03:00 INF Processing chunk 'vm/1758016790-1758017090.bin'...
2025-09-16T13:06:48+03:00 INF Successfully processed '1758016790-1758017090.bin'
2025-09-16T13:06:48+03:00 INF Successfully imported!

```

To access imported data, connect to PMM and navigate to the dashboard you want.

PMM Dump supports many custom options allowing you to define which data to export. For more details, consult [Export](export.md). For import-related options, consult [Import](import.md). For a full list of supported commands, consult [Commands](commands.md).

!!! note

    The [`load-pmm-dump`](load-pmm-dump.md) utility spins up PMM Server and sets it up, then imports the dump. We recommend using this semi-automatic solution for importing PMM dumps.

## Running PMM Dump from the Docker container

Starting from version 2.27.0, PMM Server is shipped with PMM Dump. Therefore, you do not need to install it. To run this shipped version, use the `docker exec` command:

``` {.bash data-prompt="$" }
$ sudo docker exec -it pmm-server pmm-dump export \
> --pmm-url="https://*****:*****@`hostname -i`" --allow-insecure-certs
```

This will create an archive file under the `/opt` directory inside the PMM server Docker container. You can copy it to your host machine with the command:

``` {.bash data-prompt="$" }
$ sudo docker cp pmm-server:/opt/pmm-dump-{UNIX TIMESTAMP}.tar.gz.enc .
```

Then you can remove the archive from the container using the command:

``` {.bash data-prompt="$" }
$ sudo docker exec -it pmm-server rm /opt/pmm-dump-{UNIX TIMESTAMP}.tar.gz.enc
```

Replace `pmm-dump-{UNIX TIMESTAMP}.tar.gz.enc` with the actual file name in your environment.
