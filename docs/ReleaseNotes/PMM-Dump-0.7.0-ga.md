# PMM Dump 0.7.0-ga

* **Date**

    November 22, 2023

* **Installation**

    [Installing PMM Dump](../installation.md)

## Release Highlights

* This is the first General Availability of PMM Dump. It includes bug fixes, Go security updates, and improvements for the regression tests framework.

## Bugs Fixed

* [SE-84](https://jira.percona.com/browse/SE-84): PMM Dump should have regression tests

* [SE-87](https://jira.percona.com/browse/SE-87): pmm-dump miss error while getting pmm server version

* [SE-88](https://jira.percona.com/browse/SE-88): pmm-dump regressions test should be able to use existing pmm containers

* [SE-89](https://jira.percona.com/browse/SE-89): pmm-dump regression test should import to another pmm server to compare differences

* [SE-91](https://jira.percona.com/browse/SE-91): Limit message size for import

* [SE-95](https://jira.percona.com/browse/SE-95): pmm-dump export for QAN data has scalability issues.

## load-pmm-dump.sh Improvements

* [PR-52](https://github.com/percona/pmm-dump/pull/52):  Changes to support multiple file automatic import. 

## PMM GUI Integration Improvements

* [PR-66](https://github.com/percona/pmm-dump/pull/66):  PMM-12460 Add token and cookie authentication support
