# verify-vm-native-data

The script `verify-vm-native-data` verifies whether the data in the dump uses VictoriaMetrics 1.77.2 or 1.82.1 native format.

Use this script when you get the error:

``` {.text .no-copy}
Failed to import: failed to write chunk: non-OK response from victoria metrics ... 
error when processing native block: cannot unmarshal native block from ... bytes: 
cannot read ...: src is too short for reading string with size ...; len(src)=1
```

Dumps that use 1.77.2 can be imported into PMM 2.32 or lower. Dumps that use 1.82.1 format can be imported into PMM 2.33 or higher.

See [`SE-83`](https://jira.percona.com/browse/SE-83) for more details.
