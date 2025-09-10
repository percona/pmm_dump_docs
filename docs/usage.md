# Using PMM Dump

## Exporting data

PMM Dump exports collected metrics from a PMM instance into a tarball file. By default, the name of the resulting file is `pmm-dump.tar.gz-{CURRENT_TIMESTAMP}.enc`.

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='https://admin:admin@127.0.0.1' \
> --allow-insecure-certs2025-09-10T17:57:58+03:00 INF Credential user was obtained from pmm-url
2025-09-10T17:57:58+03:00 INF Credential password was obtained from pmm-url
2025-09-10T17:57:58+03:00 INF Exporting metrics...
2025-09-10T17:57:58+03:00 INF Processing 1/49 chunk...
2025-09-10T17:57:58+03:00 INF start: 2025-09-10T10:57:58.448Z
2025-09-10T17:57:58+03:00 INF end: 2025-09-10T11:02:58.448Z
2025-09-10T17:57:58+03:00 INF Processing 2/49 chunk...
2025-09-10T17:57:58+03:00 INF start: 2025-09-10T11:02:58.448Z
...
2025-09-10T17:58:05+03:00 INF Writing chunk to the dump... filename=1757515078-1757515378.bin source=vm
2025-09-10T17:58:05+03:00 INF Writing chunk to the dump... filename=1757515378-1757515678.bin source=vm
2025-09-10T17:58:05+03:00 INF Writing chunk to the dump... filename=1757515678-1757515978.bin source=vm
2025-09-10T17:58:05+03:00 INF Writing chunk to the dump... filename=1757515978-1757516278.bin source=vm
2025-09-10T17:58:05+03:00 INF Password: ****************
2025-09-10T17:58:05+03:00 INF Successfully exported!
$ ls pmm-dump.tar.gz*
pmm-dump.tar.gz-1757516278.enc
```
This command exports all performance metrics collected in the last 4 hours and encrypts them with an auto-generated password.

!!! warning
    
    PMM Dump will not export QAN data unless the option `--dump-qan` is specified.

## Importing data

To import data, start a new PMM instance and run the `pmm-dump import` command:

``` {.bash data-prompt="$" }
$ pmm-dump import --pmm-url='https://admin:admin@127.0.0.1' \
> --dump-path=pmm-dump.tar.gz-1757516278.enc --pass=****************
2025-09-10T18:04:29+03:00 INF Credential user was obtained from pmm-url
2025-09-10T18:04:29+03:00 INF Credential password was obtained from pmm-url
2025-09-10T18:04:29+03:00 INF Opening dump file... path=pmm-dump.tar.gz-1757516278.enc
2025-09-10T18:04:29+03:00 INF Importing metrics...
2025-09-10T18:04:29+03:00 INF Processing chunk 'vm/1757501878-1757502178.bin'...
2025-09-10T18:04:29+03:00 INF Processing chunk 'vm/1757502178-1757502478.bin'...
2025-09-10T18:04:29+03:00 INF Processing chunk 'vm/1757502478-1757502778.bin'...
...
2025-09-10T18:04:31+03:00 INF Successfully processed '1757514478-1757514778.bin'
2025-09-10T18:04:31+03:00 INF Successfully processed '1757515978-1757516278.bin'
2025-09-10T18:04:31+03:00 INF Successfully imported!
```

To access imported data, connect to PMM and navigate to the dashboard you want.

PMM Dump supports many custom options allowing you to define which data to export. For more details, consult [Export](export.md). For import-related options, consult [Import](import.md). For a full list of supported commands, consult [Commands](commands.md).

!!! note

    The [`load-pmm-dump`](load-pmm-dump.md) utility spins up PMM Server and sets it up, then imports the dump. We recommend using this semi-automatic solution for importing PMM dumps.

## Running PMM Dump from the Docker container

Starting from version 2.27.0, PMM Server is shipped with PMM Dump. Therefore, you do not need to install it. To run this shipped version, use the `docker exec` command:

``` {.bash data-prompt="$" }
$ sudo docker exec -it pmm-server pmm-dump export \
> --pmm-url="https://admin:admin@`hostname -i`" --allow-insecure-certs
```

This will create an archive file under the `/opt` directory inside the PMM server Docker container. You can copy it to your host machine with the command:

``` {.bash data-prompt="$" }
$ sudo docker cp pmm-server:/opt/pmm-dump-{UNIX TIMESTAMP}.tar.gz .
```

Then you can remove the archive from the container using the command:

``` {.bash data-prompt="$" }
$ sudo docker exec -it pmm-server rm /opt/pmm-dump-{UNIX TIMESTAMP}.tar.gz
```
Replace `pmm-dump-{UNIX TIMESTAMP}.tar.gz` with the actual file name in your environment.
