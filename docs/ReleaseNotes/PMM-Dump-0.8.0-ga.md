# PMM Dump 0.8.0-ga (Not Yet Released)

* **Date**

    October 28, 2025

* **Installation**

    [Installing PMM Dump](../installation.md)

## Release Highlights

* This is the third General Availability release of PMM Dump. It includes encryption support, bug fixes, improvements, and Go security updates.

## New Features

* [SE-97](https://jira.percona.com/browse/SE-97) PMM-Dump Tool - SecOps Request

PMM Dump now supports encryption. Dump files are encrypted by default with an auto-generated password or a user-defined password, specified by the option `--pass`. The auto-generated password is either printed to the screen at the end of the `export` operation or stored in a file specified by the option `--pass-filepath`.

Output logging to `STDOUT` is disabled for the `export` operation by default and can be overridden by specifying the option `--no-just-key`. You can also obtain the log from the file `log.json` in the PMM Dump resulting archive.

Encryption can be disabled with the option `--no-encryption`.

## Bugs Fixed

* [PR-292](https://github.com/percona/pmm-dump/pull/292) Fix services node name retrieval - Thanks to Davide Sbetti for the contribution

* [SE-96](https://jira.percona.com/browse/SE-96) pmm-dump export hitting -search.maxSamplesPerQuery limits

* [SE-109](https://jira.percona.com/browse/SE-109) Automatic tests are unstable

* [SE-110](https://jira.percona.com/browse/SE-110) pmm-dump cannot parse time

* [SE-112](https://jira.percona.com/browse/SE-112) load-pmm-dump prints error "line 75: [2: command not found"

* [SE-119](https://jira.percona.com/browse/SE-119) More errors "[2: command not found" in load-pmm-dump after fix for SE-112
