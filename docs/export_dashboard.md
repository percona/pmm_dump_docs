# Exporting Metrics for a Specific Dashboard

PMM has many dashboards, and you may not want to export them all. Instead, you may prefer to export only a few of them related to the performance issue you are experiencing.

PMM Dump supports the option `--dashboard` that allows specifying which dashboard name or names you want to export.

For example, to export only the "MySQL InnoDB Details" dashboard, use the command:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url= 'http://admin:admin@127.0.0.1' \
> --dashboard='MySQL InnoDB Details'
```

To export several dashboards, specify the `--dashboard` option more than once:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url= 'http://admin:admin@127.0.0.1' \
> --dashboard='MySQL InnoDB Details' \
> --dashboard='Node Summary' --dashboard='MySQL Instance Summary'
```

This command exports the dashboards "MySQL InnoDB Details", "Node Summary", and "MySQL Instance Summary".

You can combine the option `--dashboard` with the option `--instance` to export only required dashboards for the instances you need help with.

The following will export dashboards "MongoDB Instance Summary" and "Node Summary" for instances `supp-mongo_3599`, `supp-mongo_3600`, and `supp-mongo-3601`:

``` {.bash data-prompt="$" }
$ pmm-dump export --pmm-url= 'http://admin:admin@127.0.0.1' \
> --dashboard='MongoDB Instance Summary' --dashboard='Node Summary'\
> --instance='supp-mongo_3599' --instance='supp-mongo_3600' \
> --instance='supp-mongo_3601'
```


