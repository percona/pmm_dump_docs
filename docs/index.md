# PMM Dump Documentation

The `pmm_dump` client utility performs a logical backup of the performance metrics, collected by the PMM Server and imports them into a different PMM Server instance.

PMM Dump allows you to share monitoring data, collected by your PMM server, with Percona Support team securely.

!!! hint alert alert-success "Important"
    Starting with PMM 2.41, the standalone client utility has been seamlessly integrated into PMM and is easily accessible from the main menu **> Help > PMM Dump**.
    We highly recommend transitioning to the integrated version, unless you need to use specific functionalities like filtering or other features exclusive to the utility, or if you need to stay on PMM version 2.40 or older.