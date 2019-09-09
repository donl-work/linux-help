SHOW BIG QUERY TABLE SCHEMA

```
bq show --format=prettyjson projectId:datasetId.TableName
```

Extract JSON
```
bq show --format=prettyjson projectId:datasetId.TableName | jq '.schema.fields'

```
NOTE: 

May need to install jq - Command-line JSON processor
```
sudo apt  install jq

```