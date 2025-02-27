---
title: Connection Settings for AGPM Server
description: Connection Settings for AGPM Server
author: aczechowski
ms.assetid: cc67f122-6309-4820-92c2-f6a27d897123
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.pagetype: mdop
ms.mktglfcycl: manage
ms.sitesec: library
ms.date: 06/16/2016
---


# Connection Settings for AGPM Server


You can use Administrative template settings for Advanced Group Policy Management (AGPM) to centrally configure AGPM Server connections for Group Policy administrators to whom a Group Policy Object (GPO) with these settings is applied.

The following settings are available under User Configuration\\Policies\\Administrative Templates\\Windows Components\\AGPM when editing a GPO.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Setting</th>
<th align="left">Effect</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>AGPM: Specify default AGPM Server (all domains)</strong></p></td>
<td align="left"><p>This policy setting allows you to specify a default AGPM Server for all domains. This is used only by AGPM Clients, and restricts Group Policy administrators from connecting to another archive. You can override this default for individual domains using the <strong>AGPM: Specify AGPM Servers</strong> setting.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>AGPM: Specify AGPM Servers</strong></p></td>
<td align="left"><p>This policy setting allows you to specify the AGPM Servers for individual domains. This is used only by AGPM Clients, and restricts Group Policy administrators from connecting to a different archive for the specified domain. To specify a default AGPM Server, use the <strong>AGPM: Specify default AGPM Server (all domains)</strong> setting and use this policy setting to override the default on a per domain basis.</p></td>
</tr>
</tbody>
</table>

 

### Additional references

-   [Administrative Templates Folder](administrative-templates-folder-agpm40.md)

-   [Performing AGPM Administrator Tasks](performing-agpm-administrator-tasks-agpm40.md)

 

 





