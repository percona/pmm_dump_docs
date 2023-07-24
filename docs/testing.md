# Testing PMM Dump

PMM Dump source code is shipped with regression tests that use test PMM and MongoDB instances. These instances are started automatically when tests are started unless you change this behavior in the configuration files.

## Requirements

- Go compiler
- Docker

## Running Regression Tests

Run

``` {.bash data-prompt="$" }
$ make run-tests
```

This command will initialize test setup, then run all regression tests, then shutdown the test setup. If any of tests fails, all subsequent tests will be stopped.

## Shutting Down Test Environment

If, for some reason, test environment was not destroyed automatically, you can destroy it by command

``` {.bash data-prompt="$" }
$ make down-tests
```

## Adjusting options for your test instances

When you run 

``` {.bash data-prompt="$" }
$ make run-tests
```
for the first time, it implicitly calls command

``` {.bash data-prompt="$" }
$ make init-tests
```

that creates temporary directory `test` for test configuration and results. Files `.env.test` and `.env2.test` define environment for your test instances. Instance that contain test data that needs to be **exported**, defined in `.env.test`. Instance that tests **import**, defined in `.env2.test`. All subsequent test runs keep these files if they exist and if you need to redefine ports and Docker container names, you can do it here.

Available options are:

| Name                 |          `.env.test` default |         `.env2.test` default | Description                                            |
|----------------------|------------------------------|------------------------------|--------------------------------------------------------|
| PMM_SERVER_NAME      |              pmm-server-test |            pmm-server-test-2 | Container name for PMM Server                          |
| PMM_CLIENT_NAME      |              pmm-client-test |            pmm-client-test-2 | Container name for PMM Client                          |
| PMM_MONGO_NAME       |                   mongo-test |                 mongo-test-2 | Container name for MongoDB test instance               |
| PMM_HTTP_PORT        |                         8282 |                         8283 | HTTP port for PMM                                      |
| PMM_HTTPS_PORT       |                         8384 |                         8385 | HTTPS port for PMM                                     |
| CLICKHOUSE_PORT      |                         9001 |                         9002 | Clickhouse port (for QAN export/import)                |
| CLICKHOUSE_PORT_HTTP |                         8124 |                         8125 | HTTP port for Clickhouse (for QAN export/import)       |
| MONGO_PORT           |                        27018 |                        27019 | MongoDB port                                           |
| USE_EXISTING_PMM     |                        false |                        false | Use existing PMM Server installation?                  |
| PMM_URL              | http://admin:admin@localhost | http://admin:admin@localhost | PMM Server url (used only while USE_EXISTING_PMM=true) |

## Using existing PMM Server instance

To use existing PMM Server instance either for export or import, set option `USE_EXISTING_PMM` to `true` and `PMM_URL` to valid URL of your PMM instance.

## PMM versions compatibility test

PMM versions compatibility test `TestPMMCompatibility` uses configuration file `./internal/test/e2e/data/versions.yaml` with list of versions that need to be checked for compatibility. Edit this file before running tests if you need add or remove particular version.
