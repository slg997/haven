# Use JQ to parse AWS CloudTrail Logs

## Examples
## Filter by S3 Service and BucketName
jq -r '.Records[] | select(.eventSource == "s3.amazonaws.com" and .requestParameters.bucketName == "{insert}")' cloudtrail_log.json

- The -r flag tells jq to output the results in RAW format instead of JSON. 
- The FILTER conditions are enclosed with single quotes.

## Display Defined Fields
jq -r '.Records[] | select(.eventSource == "s3.amazonaws.com" and .requestParameters.bucketName=="{insert}") | [.eventTime, .eventName, .userIdentity.userName // "N/A",.requestParameters.bucketName // "N/A", .requestParameters.key // "N/A", .sourceIPAddress // "N/A"]' cloudtrail_log.json 

- [] process and create any array with specified from each reach
- The string // "N/A" is included for formatting reasons. If the field does not have a value, it will display N/A instead.
- @tsv outputs to tab-separated values.
- column -t -s $'\t' beautifies the results by processing all tabs and aligning the columns.

## Display Defined Fields in Columns
jq -r '["Event_Time", "Event_Name", "User_Name", "Bucket_Name", "Key", "Source_IP"],(.Records[] | select(.eventSource == "s3.amazonaws.com" and .requestParameters.bucketName=="{insert}") | [.eventTime, .eventName, .userIdentity.userName // "N/A",.requestParameters.bucketName // "N/A", .requestParameters.key // "N/A", .sourceIPAddress // "N/A"]) | @tsv' cloudtrail_log.json | column -t -s $'\t'

- ["Event_Time", "Event_Name", "User_Name", "Bucket_Name", "Key", "Source_IP"] prepends a column header row using square brackets
- @tsv outputs to tab-separated values.
- column -t -s $'\t' beautifies the results by processing all tabs and aligning the columns.