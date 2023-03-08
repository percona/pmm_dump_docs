# Using PMM Dump

## Exporting Data

PMM Dump exports collected metrics from PMM instance into tarball file. By default, name of the result file is `pmm-dump-{CURRENT_TIMESTAMP}.tar.gz`.

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='https://admin:admin@127.0.0.1' \
> --allow-insecure-certs
2023-01-05T20:01:33+03:00 INF Credential user was obtained from pmm-url
2023-01-05T20:01:33+03:00 INF Credential password was obtained from pmm-url
2023-01-05T20:01:33+03:00 INF Exporting metrics...
2023-01-05T20:01:33+03:00 INF Processing 1/49 chunk...
2023-01-05T20:01:33+03:00 INF Processing 2/49 chunk...
2023-01-05T20:01:33+03:00 INF Processing 3/49 chunk...
...
2023-01-05T20:01:39+03:00 INF Processing 47/49 chunk...
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672934193-1672934493.bin source=vm
2023-01-05T20:01:39+03:00 INF Processing 48/49 chunk...
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672934493-1672934793.bin source=vm
2023-01-05T20:01:39+03:00 INF Processing 49/49 chunk...
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672934793-1672935093.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672935093-1672935393.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672935393-1672935693.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672935693-1672935993.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672935993-1672936293.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672936293-1672936593.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672936593-1672936893.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672936893-1672937193.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672937193-1672937493.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672937493-1672937793.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672938093-1672938393.bin source=vm
2023-01-05T20:01:39+03:00 INF Writing chunk to the dump... filename=1672937793-1672938093.bin source=vm
2023-01-05T20:01:39+03:00 INF Successfully exported!
$ ls *tar.gz
pmm-dump-1672938093.tar.gz
```

This command will export all performance metrics, collected in last 4 hours.

!!! warning
    
    PMM Dump would not export QAN data unless option `--dump-qan` was specified.

## Importing Data

To import data, fire up new PMM instance and run command `pmm-dump import`:

``` {.bash data-prompt="$" }
$ ./pmm-dump import --pmm-url='https://admin:admin@127.0.0.1' \
> --allow-insecure-certs --dump-path=pmm-dump-1672938093.tar.gz 
2023-01-05T20:09:46+03:00 INF Credential user was obtained from pmm-url
2023-01-05T20:09:46+03:00 INF Credential password was obtained from pmm-url
2023-01-05T20:09:46+03:00 INF Importing metrics...
2023-01-05T20:09:46+03:00 INF Opening dump file... path=pmm-dump-1672938093.tar.gz
2023-01-05T20:09:46+03:00 INF Processing chunk 'vm/1672923693-1672923993.bin'...
2023-01-05T20:09:46+03:00 INF Successfully processed 'vm/1672923693-1672923993.bin'
...
2023-01-05T20:09:55+03:00 INF Processing chunk 'vm/1672937793-1672938093.bin'...
2023-01-05T20:09:55+03:00 INF Successfully processed 'vm/1672937793-1672938093.bin'
2023-01-05T20:09:55+03:00 INF Successfully imported!
```

To access imported data, connect to PMM and navigate to the dashboard you want.

PMM Dump supports many custom options allowing to define which data to export. For more details, consult [Export](export.md). For import-related options, consult [Import](import.md). For full list of supported commands, consult [Commands](commands.md).

!!! note

    Utility [`load-pmm-dump`](load-pmm-dump.md) spins up PMM Server and setups it, then imports dump. We recommend you to use this semi-automatic solution for importing PMM dumps.

## Running PMM Dump from the Docker Container

Starting from version 2.27.0, PMM Server is shipped with PMM Dump. Therefore you do not need to install it. To run this shipped vesion use `docker exec` command:

``` {.bash data-prompt="$" }
$ sudo docker exec -it pmm-server pmm-dump export \
> --pmm-url="https://admin:admin@`hostname -i`" --allow-insecure-certs
```

This will create an archive file under the `/opt` directory inside the PMM server docker container. You can copy it to your host machine with the command:

``` {.bash data-prompt="$" }
$ sudo docker cp pmm-server:/opt/pmm-dump-{UNIX TIMESTAMP}.tar.gz .
```

Then you can remove the archive from the container using the command:

``` {.bash data-prompt="$" }
$ sudo docker exec -it pmm-server rm /opt/pmm-dump-{UNIX TIMESTAMP}.tar.gz
```
Replace `pmm-dump-{UNIX TIMESTAMP}.tar.gz` with the actual file name in your environment.
