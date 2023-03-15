# Install PMM Dump

!!! note

    Starting from version 2.27.0, PMM Server is shipped with PMM Dump. Therefore you do not need to install it. To run this shipped version use the `docker exec` command as follows:

    ``` {.bash data-prompt="$" }
    $ docker exec -it pmm-server pmm-dump help
    usage: pmm-dump [<flags>] <command> [<args> ...]
    ...
    ```

## Binary installation

You can download the latest version of PMM Dump from [Percona website](https://www.percona.com/get/pmm-dump). Once downloaded, set executable bit for the `pmm-dump` binary file and you are ready to use it.

``` {.bash data-prompt="$" }
$ curl -OL https://www.percona.com/get/pmm-dump
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 11.9M    0 11.9M    0     0   624k      0 --:--:--  0:00:19 --:--:-- 2628k
$ chmod +x pmm-dump
$ ./pmm-dump version
Version: 0.6.1-rc, Build: e2bc9a9
```

Alternatively, you can download PMM Dump binary from [PMM Dump GitHub Releases](https://github.com/percona/pmm-dump/releases) page. At this place you will find all published versions of PMM Dump.

## Compiling from source

1. Check if version of Go is 1.16 or newer.

    ``` {.bash data-prompt="$" }
    $ go version 
    go version go1.19.4 linux/amd64
    ```

2. Clone PMM Dump [GitHub repository](https://github.com/percona/pmm-dump):

    ``` {.bash data-prompt="$" }
    $ git clone git@github.com:percona/pmm-dump.git
    ```

3. `cd` into the newly created directory and run `make build`:

    ``` {.bash data-prompt="$" }
    $ cd pmm-dump
    $ make build
    $ go build -ldflags "-X 'main.GitBranch=main' -X 'main.GitCommit=b3804a9' -X 'main.GitVersion=v2.32.0'" -o pmm-dump pmm-dump/cmd/pmm-dump
    ``` 

This will compile the `pmm-dump` binary.
