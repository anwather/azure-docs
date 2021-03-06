﻿---
title: Manage reverse DNS records for your Azure (classic) services using PowerShell | Microsoft Docs
description: 'How to manage reverse DNS records or PTR records for Azure services using PowerShell in the classic deployment model. '
services: DNS
documentationcenter: na
author: s-malone
manager: carmonm
editor: ''
tags: azure-service-management

ms.assetid: 9c24d176-6bce-4277-a14c-80fe44a20a87
ms.service: DNS
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/28/2016
ms.author: smalone

---
# How to manage reverse DNS records for your Azure services (classic) using Azure PowerShell

[!INCLUDE [dns-reverse-dns-record-operations-arm-selectors-include.md](../../includes/dns-reverse-dns-record-operations-arm-selectors-include.md)]


[!INCLUDE [DNS-reverse-dns-record-operations-intro-include.md](../../includes/dns-reverse-dns-record-operations-intro-include.md)]


> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. Learn how to [perform these steps using the Resource Manager model](dns-reverse-dns-record-operations-ps.md).

## Validation of reverse DNS records
To ensure a third party can’t create reverse DNS records mapping to your DNS domains, Azure only allows the creation of a reverse DNS record where one of the following is true:

* The reverse DNS FQDN is the name of the Cloud Service for which it has been specified, or any Cloud Service name within the same subscription e.g., reverse DNS is “contosoapp1.cloudapp.net.”.
* The reverse DNS FQDN forward resolves to the name or IP of the Cloud Service for which it has been specified, or to any Cloud Service name or IP within the same subscription e.g., reverse DNS is “app1.contoso.com.” which is a CName alias for contosoapp1.cloudapp.net.

Validation checks are only performed when the reverse DNS property for a Cloud Service is set or modified. Periodic re-validation is not performed.

## Add reverse DNS to existing Cloud Services
You can add a reverse DNS record to an existing Cloud Service using the “Set-AzureService” cmdlet:

    PS C:\> Set-AzureService –ServiceName “contosoapp1” –Description “App1 with Reverse DNS” –ReverseDnsFqdn “contosoapp1.cloudapp.net.”

## Create a Cloud Service with reverse DNS
You can add a new Cloud Service with the reverse DNS property specified using the “Set-AzureService” cmdlet:

    PS C:\> New-AzureService –ServiceName “contosoapp1” –Location “West US” –Description “App1 with Reverse DNS” –ReverseDnsFqdn “contosoapp1.cloudapp.net.”

## View reverse DNS for existing Cloud Services
You can view the configured value for an existing Cloud Service using the “Get-AzureService” cmdlet:

    PS C:\> Get-AzureService "contosoapp1"

## Remove reverse DNS from existing Cloud Services
You can remove a reverse DNS property from an existing Cloud Service using the “Set-AzureService” cmdlet. This is done by setting the reverse DNS property value to blank:

    PS C:\> Set-AzureService –ServiceName “contosoapp1” –Description “App1 with Reverse DNS” –ReverseDnsFqdn “”

[!INCLUDE [FAQ1](../../includes/dns-reverse-dns-record-operations-faq-host-own-arpa-zone-include.md)]

[!INCLUDE [FAQ2](../../includes/dns-reverse-dns-record-operations-faq-asm-include.md)]

