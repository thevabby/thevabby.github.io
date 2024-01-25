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

### Use below script to authenticate to Azure AD using client ID and secret and update extended attributes 

```powershell
$User = "<<client_id>>"
$PWord = ConvertTo-SecureString -String "<<client_secret>>" -AsPlainText -Force

$Credential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $User, $PWord
$ClientSecretCredential = Get-Credential -Credential $Credential

Connect-MgGraph -TenantId "<tenant_id>" -ClientSecretCredential $ClientSecretCredential


$CSVrecords = Import-Csv C:\Temp\AzureAD\script\data.csv -Delimiter ","

# Create arrays for skipped and failed users
$SkippedUsers = @()
$FailedUsers = @()

# Loop trough CSV records
foreach ($CSVrecord in $CSVrecords) {
    $upn = $CSVrecord.UserPrincipalName
    $User = Get-MgUser -Filter "userPrincipalName eq '$upn'"  
    if ($User) {
        try{
        $hash = @{ extension_1234567890_LocationID = $CSVrecord.LocationID; extension_1234567890_JobCode = $CSVrecord.JobCode;extension_1234567890_OpsSupportID = $CSVrecord.OpsSupportID; extension_1234567890_BrandID = $CSVrecord.BrandID; extension_1234567890_CompanyID = $CSVrecord.CompanyID; extension_1234567890_PersonaType = $CSVrecord.PersonaType;extension_1234567890_IdentityType = $CSVrecord.IdentityType; extension_1234567890_AccountType = $CSVrecord.AccountType }

        Update-MgUser -UserId $User.Id -AdditionalProperties $hash
        Write-Host "$upn , user found, Updated Successfully"
        #Get-MgUser -Filter "userPrincipalName eq '$upn'"
        } catch {
        $FailedUsers += $upn
        Add-Content -Path ./failed.txt -Value "$upn , user found, FAILED to update"
        }
    }
    else {
        Add-Content -Path ./skipped.txt -Value "$upn , user not found, skipped"
        $SkippedUsers += $upn
    }
}

```
