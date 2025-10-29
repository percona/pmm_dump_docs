# load-pmm-dump

The utility `load-pmm-dump` creates an empty PMM instance and prints commands which you can use to load the dump into a test PMM instance, redirect the PMM port to another machine, and destroy the Docker PMM container after use.

The main goal of the utility is to aid in handling imported data coming from a PMM dump export file (or files). The `load-pmm-dump` script will:

- Create a PMM server container
- Disable the nginx cap for `client_max_body_size`
- Try to automatically import `pmm-dump` dump files
- Provide useful commands and information on how to further use the container

**Note:** The PMM server container will be created without a data volume/container, so this tool is NOT for deploying any other kind of PMM server other than ones holding volatile and temporary data!

## Running the script

There are three ways to run the script (all of them require at least one parameter -- the ticket number or container name string).

- This will assume the latest PMM v3 server version, and will deploy one container: `pmm-server-CS0012345`

``` {.bash data-prompt="$" }
load-pmm-dump CS0012345
```

- This will use the second argument as the PMM server Docker version tag (all other possible arguments are ignored).

``` {.bash data-prompt="$" }
load-pmm-dump CS0012345 2.26.0
```

- This will get the PMM server Docker version tag from the .tar.gz/.tgz file metadata, and it will use it for the container. Additionally, it will try to automatically import the data with `pmm-dump import` (optionally, other files can be added as third and following arguments).

``` {.bash data-prompt="$" }
load-pmm-dump CS0012345 /path/to/pmm-dump-1653879141.tar.gz
```

After it's done, the tool will output some helpful information and copy/paste-ready commands. For example:

```{.text .no-copy}
## USEFUL INFORMATION AND COMMANDS.

## Port 443 is exported to: 49277

## Use the following for port redirection from your local machine:
ssh -L 8443:127.0.0.1:49277 tp-support03.tp.int.percona.com

## To import a PMM dump:
pmm-dump import --allow-insecure-certs --pmm-url=https://admin:admin@127.0.0.1:49277 --dump-path=[...]

## Use the following to get human readable dates from a Unix timestamp:
date -d @1657948064

## Increase 'Data Retention' in the advanced settings if the samples are older than the default 30 days.
## For example, to increase to 60 days:
## docker exec pmm-server-CS0037806 curl -s -u admin:admin --request POST -k --url https://127.0.0.1:443/v1/Settings/Change -H 'Content-Type: application/json' -d '{"data_retention":"5184000s"}'

## To destroy docker PMM server container:
docker rm -vf pmm-server-CS0037806
```
