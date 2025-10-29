# PMM Dump File Content

After successfull export, PMM Dump will a create gzipped tar archive. The resulting archive will be encrypted unless created with option `--no-encryption`, and will contain following files.

 - **meta.json**: metadata about the data dump
 - **vm**: gzipped Victoria Metrics data chunks in JSON format (default) or in native VM format (taken with option `--vm-native-data`), organized by timeframe
 - **ch**: Query Analytics (QAN) data stored in ClickHouse (TSV) format, organized by row count
 - **log.json**: logs detailing the export and archive creation process