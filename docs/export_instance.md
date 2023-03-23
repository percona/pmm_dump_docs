# Exporting metrics for a specific database instance

You may monitor dozens of database servers with PMM, but you may need to export metrics only for one or a few of them at the moment.

To filter exported data for an instance, first you need to identify the instance name or the Service ID. You can find these details in the "Inventory / Services" dashboard:

![image](assets/images/PMM_Inventory.png)

Once you've identified the instance you want to export data for, you can use the PMM Dump filtering option.

PMM Server stores performance metrics in VictoriaMetrics and Query Analytics (QAN) data in ClickHouse. Therefore PMM Dump has to query these two databases separately.

## Filtering performance metrics

If you want to export performance metrics for a specific service, you need to get the service name of the instance and use the option `--instance='YOUR_INSTANCE_NAME'`. For example, to export data for the instance `my_mysql_8025`, use the command:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='http://admin:admin@127.0.0.1' \
> --instance='my_mysql_8025'
```

If you want to export data for multiple instances, specify the option `--instance` as many times as needed. Thus, to export data for instances `supp-mongo_23599`, `supp-mongo_23600`, and `supp-mongo_23601`, use the command:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url= 'http://admin:admin@127.0.0.1' \
> --instance='supp-mongo_23599' \
> --instance='supp-mongo_23600' \
> --instance='supp-mongo_23601'
```

## Filtering QAN data

To export QAN data for the specific instance, use the `--where="service_name='YOUR_INSTANCE_NAME'"` or the `--where="service_id='/service_id/YOUR_INSTANCE_SERVICE_ID'"` options.

For example, to export QAN data for the instance `my_mysql_8025` and `service_id` equal to `"/service_id/a70ca022-9368-46b8-86b7-e7bc922fb459"` you can use one of the following commands:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='http://admin:admin@172.17.0.3' \
> --where="service_name='my_mysql_8025'" --dump-qan
```
or

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='http://admin:admin@172.17.0.3' \
> --where="service_id='/service_id/a70ca022-9368-46b8-86b7-e7bc922fb459'" \
> --dump-qan
```

Option `--where` supports selecting by other fields, such as `node_id` as well as boolean operators. For example, to export QAN data for both the instances `my_mysql_8025` and `supp-mongo_23599` run the following command:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url='http://admin:admin@172.17.0.3' \
> --where="service_name='supp-mongo_23599' or service_name='my_mysql_8025'" \
> --dump-qan
```

!!! warning

    Do not forget to use the option `--dump-qan`. Otherwise, the tool won't export the QAN data.

!!! note

    If you want to export only QAN data and do not want to export performance metrics, add the option `--no-dump-core`.
