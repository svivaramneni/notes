## Splunk Query Tips
* Splunk field values are not case sensitive. 
* Common field operators are 
```field=value, !=, <, >, <=, >= , AND, OR, * ```
* Splunk has 3 different search modes. Fast, Smart and Verbose
* Selected fields from sidebar are highlighted in results. You can also generate quick reports from selected fields and tweak them, if needed.
* Search Processing Language queries in Splunk has following Keywords: AS, BY, OVER, WHERE
### Chaining SPL Commands
```
instance=sparc earliest="5/14/2020:22:45:00" latest="5/14/2020:22:51:30" AND rescode!=NULL | where rescode > 200 or rescode < 500
```
### SPL filtering and modifying search results
Field, Search and Rename commands
```
 | fields + baseuri, method, rescode
 | search change_request
 | search change_request | rename rescode as HTTPStatus
```
### SPL Ordering search results: 
```| head (num) : top results
 | tail (num) : last 
 | sort (fieldname) : order field by ascending order
 | reverse
 | tables (fieldname) : For creating tables with specific fields.
```
### Transformative commands : 
```
| top(fieldname) 

instance=sparc earliest="5/14/2020:22:45:00" latest="5/14/2020:22:51:30" AND rescode!=NULL | top limit=10 uri

| rare (fieldname) - least frequently used or bottom 10

| highlight (fieldname1) (fieldname2) - highlights passed in fields in the results.

| contingency (fieldname1) (fieldname2) - Shows association between fields in table.

instance=sparc earliest="5/14/2020:22:45:00" latest="5/14/2020:22:51:30" AND rescode!=NULL | contingency uri rescode
```
### Stats commands
``` | stats count(eval(fieldname)) as newname : ex: | stats count by uri

| stats max(fieldname)

| stats min(fieldname) : ex: | stats min(price) by Neighbourhood

| stats sum(fieldname)
```

### Chart Commands
``` 
| chart somefunction(fieldname) - Returns chart of the data element following command.

| timechart somefunction(fieldname) - Returns time series chart over the data element following command.

instance=sparc earliest="5/14/2020:22:45:00" latest="5/14/2020:22:52:30" AND rescode!=NULL | timechart count as Requests by rescode
```
