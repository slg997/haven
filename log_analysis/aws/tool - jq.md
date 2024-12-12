# Use JQ to parse AWS CloudTrail Logs

# Examples
jq -r '.Records[] | select(.eventSource == "s3.amazonaws.com" and .requestParameters.bucketName == "{insert}")' cloudtrail_log.json
