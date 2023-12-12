# Useful commmands for Incident Response

## List user role assignments
```
az account set --subscription "subscription_id"
az role assignment list --all --assignee "upn_name"
```

## Convert GUID to username
```
Get-AzureADObjectByObjectId -objectids <GUID>
```