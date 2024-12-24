# Azure Cloud Shell
## Bash
### Enumeration
#### User
> az ad user list
OR
> az ad user list --filter "startswith('xxx',displayName)"
#### Group
> az ad group list
OR
> az ad group list --group "group_name"
#### Role Assignment
> az role assignment list --assignee "group_id" --all