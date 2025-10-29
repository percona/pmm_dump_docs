# System requirements

The `pmm-dump` utility runs as a client to PMM Server; a compatible version is already bundled with each version of PMM.  

If you want to run `pmm-dump` external to the PMM container/AMI/VM, the following conditions should be met:

* The source PMM server should be version 2.12 or above.
* The host where PMM Dump is installed should be able to access the PMM Server host via HTTPS or HTTP protocols.
* A user account with administrator access should be created within PMM.
* ClickHouse port (default is 9000) should be open to collect QAN data.

!!! note

     By default, Docker installation of PMM does not publish the ClickHouse port. This means the tool can only collect QAN metrics if `pmm-dump` is run from within the PMM Server container or on the same host as PMM (AMI/OVF). To override this behavior, start the PMM instance with the option `--publish 9000:9000`:

     ``` {.bash data-prompt="$" }
     $ docker run --detach --restart always \
       --publish 443:8443 \
       --publish 9000:9000 \
       -v pmm-data:/srv \
       --name pmm-server \
       percona/pmm-server:3
     ```

