# PMM Dump 0.8.3-ga

* **Date**

    October 20, 2026

* **Installation**

    [Installing PMM Dump](../installation.md)

## Release Highlights

* This is the General Availability release of PMM Dump. This release updates dependencies and bumps Go version to 1.27.2. 

## Module dependencies updated

## Dependency updates

- `go.mongodb.org/mongo-driver/v2` from 2.9.1 to 2.9.2 (#415)
- `golang.org/x/sync` from 0.23.0 to 0.24.0 (#414)
- `github.com/docker/go-connections` from 0.8.1 to 0.8.2 (#413)
- `github.com/valyala/fasthttp` from 1.74.0 to 1.75.0 (#412)
- `github.com/VictoriaMetrics/metricsql` from 0.87.4 to 0.87.5 (#411)
- `golang.org/x/tools` from 0.50.0 to 0.52.0 (#417)
- `github.com/reviewdog/reviewdog` from 0.21.1 to 0.21.2 (#410)

## Bugs Fixed

* [PMM-15225](https://perconadev.atlassian.net/browse/PMM-15225) Address CVEs in PMM Client and Server and PMM Extensions pre-3.10.0
