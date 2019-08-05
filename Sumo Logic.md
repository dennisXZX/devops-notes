## Sumo Logic

#### Fudamentals

- Sumo logic data flow: 
  - data collection (collectors & sources)
  - search & analyze (operators & charts)
  - visualize & monitor (alerts & dashboards)
  
- Use the `logReduce` feature to group together similar logs. `_sourceCategory=prod01/motorcycle/* | logreduce`

- You can find your collectors by using `Collection` tab or the query `* | count by _sourceCategory`

- Before you want to create a query, first look at the `shared` folder to see if there's anything you can use, then use the `App Catalog` as a starter.

__Query Syntax__

```
_sourceCategory=Labs/Apache/Access and "Mozilla"     # metadata and keywords
| parse "GET * HTTP/1.1\ *" as url, status_code      # parse the result
| timeslice 5m                                       # slice the time
| where status_code matches "5*"                     # filter the result
| count by _timeslice, status_code                   # aggregate the result
| sort by _count                                     # format the result
| limit 3                                            # format the result
``` 

You can set up `Field Extraction Rules` so the data is parsed as it is injected into Sumo Logic.
