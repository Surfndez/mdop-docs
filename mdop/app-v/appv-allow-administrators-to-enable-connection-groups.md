---
title: How to Allow Only Administrators to Enable Connection Groups (Windows 10)
description: How to Allow Only Administrators to Enable Connection Groups
author: MaggiePucciEvans
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
---


# How to Allow Only Administrators to Enable Connection Groups

**Applies to**
-   Windows 10, version 1607

You can configure the App-V client so that only administrators (not end users) can enable or disable connection groups. In earlier versions of App-V, you could not prevent end users from performing these tasks.

**Note**<br>
This feature is supported starting in App-V 5.0 SP3.

Use one of the following methods to allow only administrators to enable or disable connection groups.

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Method</th>
<th align="left">Steps</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Group Policy setting</p></td>
<td align="left"><p>Enable the “Require publish as administrator” Group Policy setting, which is located in the following Group Policy Object node:</p>
<p><strong>Computer Configuration &gt; Administrative Templates &gt; System &gt; App-V &gt; Publishing</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows PowerShell cmdlet</p></td>
<td align="left"><p>Run the <strong>Set-AppvClientConfiguration</strong> cmdlet with the <strong>-RequirePublishAsAdmin</strong> parameter.</p>
<p>Parameter values:</p>
<ul>
<li><p>0 - False</p></li>
<li><p>1 - True</p></li>
</ul>
<p>Example: <strong>Set-AppvClientConfiguration -RequirePublishAsAdmin 1</strong></p></td>
</tr>
</tbody>
</table>

## Have a suggestion for App-V?

Add or vote on suggestions on the [Application Virtualization feedback site](http://appv.uservoice.com/forums/280448-microsoft-application-virtualization).<br>For App-V issues, use the [App-V TechNet Forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=mdopappv).

## Related topics

[Managing Connection Groups](appv-managing-connection-groups.md)
