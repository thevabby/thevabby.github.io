---
title: Connect to Microsoft Graph using Python
date: 2024-01-24 11:11:11
categories: [Graph]
tags: [microsoft,azure ad, entra id, azure, graph, powershell]
---

# Connect to Microsoft Graph using Python

Below set of commands can be used to connect to Azure AD / Enttra ID using Python requests module.

### Below script can be used to authenticate to Azure AD using  Client ID and Client Secret

#### This script authenticates and uses generated token to update application identifier URI

##### Client ID and Secret used should have required API permissions set in Azure AD.

```python
import requests
import json
import sys

url = "https://login.microsoftonline.com/"+sys.argv[1].strip()+"/oauth2/v2.0/token"

payload = "client_id="+sys.argv[2].strip()+"&client_secret="+sys.argv[3].strip()+ "&grant_type=client_credentials&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default"
headers = {
  'Content-Type': 'application/x-www-form-urlencoded'
}

response = requests.request("GET", url, headers=headers, data=payload)
jsondata = response.json()
token = jsondata["access_token"]

url = "https://graph.microsoft.com/v1.0/applications/" + sys.argv[4].strip()
payload = json.dumps({
  "identifierUris": [
    sys.argv[5]
  ]
})
headers = {
  'Authorization': 'Bearer ' + token,
'Content-Type': 'application/json'
}
response = requests.request("PATCH", url, headers=headers, data=payload)

```

### To run above script

```python
python3 script.py <<tenant_id>> <<client_id>> <<client_secret>> <<applcation_id>>
```