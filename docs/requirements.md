# System requirements

The `pmm-dump` utility runs as a client to PMM Server.

The following conditions should be met:

* The source PMM server should be version 2.12 or above.
* The host where PMM Dump is installed, should be able to access PMM Server host via HTTPS or HTTP protocols.
* User account with administrator access should be created within PMM.
* ClickHouse port (default is 9000) should be open to collect QAN data.

!!! note

     By default, Docker installation of PMM does not publish the ClickHouse port. This means you can only collect QAN metrics if run PMM Dump on the same host as PMM and use Docker internal IP address. To overwrite this behavior start PMM instance with option `--publish 9000:9000`:

     ``` {.bash data-prompt="$" }
     $ docker run --detach --restart always \
       --publish 443:443 \
       --publish 9000:9000 \
       -v pmm-data:/srv \
       --name pmm-server \
       percona/pmm-server:2
     ```

