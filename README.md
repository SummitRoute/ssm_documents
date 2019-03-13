Collection of the AWS SSM documents.  These were acquired as follows:

```
aws ssm list-documents > list-documents.json
cat list-documents.json | jq -cr '.DocumentIdentifiers[].Name' | xargs -n1 sh -c 'aws ssm get-document --name $1 | jq ".Content|fromjson" > "documents/$1"' sh
```

This formats the double-encoded json document to prettified single json.
