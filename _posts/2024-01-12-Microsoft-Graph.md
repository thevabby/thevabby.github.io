---
title: Microsoft Graph
date: 2024-01-12 11:11:11
categories: [Graph]
tags: [microsoft,azure ad, entra id, azure, graph, powershell]
---

# Microsoft Graph

This post has commands on how to use MSGraph Powershell cmdlets to connect to Microsoft Azure AD(Entra ID).

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### To install Microsoft Graph Powershell Module

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```

### To connect to Entra ID using MgGraph

```powershell
Connect-MgGraph
```