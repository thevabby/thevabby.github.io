---
title: IdentityNow - Searchable Attributes
date: 2023-09-02 11:12:11 -001
categories: [IdentityNow, SailPoint]
tags: [sailpoint, idn, identitynow, correlation]
---

#### Indexing a SailPoint IdentityNow Attribute in an Identity Cube for use in Correlation Rules

1. API to GET the attribute details

```bash

 HTTP GET https://<<tenant>>.api.identitynow.com/cc/api/identityAttribute/get?name=<<attr_name>>

```

2. Use Response from Step 1 and set "searchable" flag as true.

```bash

HTTP POST https://<<tenant>>.api.identitynow.com/cc/api/identityAttribute/update?name=<<attr_name>>


{
    "displayName": "<<Display Name>>",
    "name": "<<attr_name>>",
    "searchable": true,
    "sources": [
        {
            "properties": {
                "ruleName": "Cloud Promote Identity Attribute",
                "ruleType": "IdentityAttribute"
            },
            "type": "rule"
        }
    ],
    "type": "String"
}


```