# PMM Dump 0.6.2-rc

* **Date**

    March 8, 2023

* **Installation**

    [Installing PMM Dump](../installation.md)

## Release Highlights

* This is the second Release Candidate of PMM Dump. Main purpose of this release is to fix critical bug [SE-83 - PMM Dump cannot import into PMM 2.33](https://jira.percona.com/browse/SE-83).

* New option: export/import in JSON format has been added. This is now default format. Exporting/importing in native VictoriaMetrics format is possible with option `vm-native-data`.

## New Features and Improvements

* Default export/import format for PMM Dump is now JSON. This feature allows to prevent version compatibility issues as in [SE-83](https://jira.percona.com/browse/SE-83). To return pevious behavior, use option `vm-native-data`. This will result in less compatible but smaller backups.

* [SE-41](https://jira.percona.com/browse/SE-41): Number of import threads needs to be configurable

## Bugs Fixed

* [SE-83](https://jira.percona.com/browse/SE-83): PMM Dump cannot import into PMM 2.33

* [SE-85](https://jira.percona.com/browse/SE-85): Typo in meta
