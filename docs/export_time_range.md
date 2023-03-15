# Exporting specific time range

By default, PMM Dump exports the last four hours of performance data. However, you may need to extract data for the different time range.

PMM Dump supports options `--start-ts` and `--end-ts` that allow specifying start and end time for the exported data.

Time should be in the [RFC3339](https://www.rfc-editor.org/rfc/rfc3339) format. For example, `2021-01-02T15:04:05Z` represents `January 2, 2021 15:04:05` in the UTC time zone and `2021-01-02T20:04:05+03:00` represents `January 2, 2021 20:04:05` in the Istanbul time zone. In order to export data within this time frame use command:

``` {.bash data-prompt="$" }
$ pmm-dump export --start-ts="2021-01-02T15:04:05Z" \
> --end-ts="2021-01-02T20:04:05+03:00"
```

PMM Dump does not support such shortcuts as `Now` or `Now - 1 hour` but if you are on Linux you can create such a time with the help of the command `date`.

For example, command `date --rfc-3339=seconds --date='TZ="Europe/Istanbul" 09:00 today'` will return the datetime string for 9am today. If called on October 8, 2021 result will be:

``` {.bash data-prompt="$" }
$ date --rfc-3339=seconds --date='TZ="Europe/Istanbul" 09:00 today'
2021-10-08 09:00:00+03:00
```

You can also add such shortcuts as `now - 1 hour`:

``` {.bash data-prompt="$" }
$ date --rfc-3339=seconds --date='TZ="Europe/Istanbul" now - 1 hour'
2021-10-08 13:17:31+03:00
```

However, the Go `time.RFC3339` format requires the `T` symbol as a delimiter between date and time part. Therefore, you need to translate the output of the date command prior to using it with PMM Dump:

``` {.bash data-prompt="$" }
$ date --rfc-3339=seconds --date='TZ="Europe/Istanbul" 09:00 today' | tr ' ' T
2021-10-08T09:00:00+03:00

$ date --rfc-3339=seconds --date='TZ="Europe/Istanbul" now - 1 hour' | tr ' ' T
2021-10-08T13:36:49+03:00
```

Then you can pass the resulting date as an argument for the tool. In order to export metrics from 9am today until current time minus 1 hour, run the command:

``` {.bash data-prompt="$" }
pmm-dump export  --pmm-url='http://admin:admin@127.0.0.1'  \
--start-ts="`date --rfc-3339=seconds --date='TZ="Europe/Istanbul" 09:00 today' | tr ' ' T`" \
--end-ts="`date --rfc-3339=seconds --date='TZ="Europe/Istanbul" now - 1 hour' | tr ' ' T`"
```
