# PMM Dump 0.6.1-rc

* **Date**

    July 1, 2022

* **Installation**

    [Installing PMM Dump](../installation.md)

## Release Highlights

* This is the first Release Candidate of PMM Dump. The main focus of this release is to improve usability of the product. We also finalized the name of the product.

## New Features and Improvements

* [SE-20](https://jira.percona.com/browse/SE-20): In addition to printing logs, save them also in the resulting dump

* [SE-56](https://jira.percona.com/browse/SE-56): Warn user when filters for QAN metrics are specified and are not specified for core metrics. And vice versa

* [SE-57](https://jira.percona.com/browse/SE-57): Store time zone information in the meta file

* [SE-60](https://jira.percona.com/browse/SE-60): Safe threshold for RAM usage within the tool

* [SE-62](https://jira.percona.com/browse/SE-62): Add release version to the version string

* [SE-64](https://jira.percona.com/browse/SE-64): Improve output messages when collection is stopped due to load.

* [SE-65](https://jira.percona.com/browse/SE-65): Add options for specifying PMM credentials.

* [SE-66](https://jira.percona.com/browse/SE-66): Check if PMM server version is supported

* [SE-69](https://jira.percona.com/browse/SE-69): PMM Transferer meta file should have arguments used.

* [SE-70](https://jira.percona.com/browse/SE-70): Add the list of services being monitored by the PMM Server to the meta.json file

* [SE-82](https://jira.percona.com/browse/SE-82): Improve error messages when chunk is too large.

## Bugs Fixed

* [SE-61](https://jira.percona.com/browse/SE-61): When copying single dashboard for one instance PMM Transferer also copies all other instances names

* [SE-63](https://jira.percona.com/browse/SE-63): --critical-load and --max-load designed with 1 CPU in mind

* [SE-68](https://jira.percona.com/browse/SE-68): PMM Transferer cannot work with usernames with special characters

* [SE-73](https://jira.percona.com/browse/SE-73): Unable to import file created using pmm-dump export stdout 

* [SE-76](https://jira.percona.com/browse/SE-76): Option version requires connection string for PMM

* [SE-77](https://jira.percona.com/browse/SE-77): MYRAM parameter documentation

* [SE-78](https://jira.percona.com/browse/SE-78): PMM-Dump sets time stamp to incorrect value in the dump file

* [SE-79](https://jira.percona.com/browse/SE-79): pmm-dump show meta doesn't report any information about services

* [SE-80](https://jira.percona.com/browse/SE-80): pmm-dump stores PMM password within the archive
