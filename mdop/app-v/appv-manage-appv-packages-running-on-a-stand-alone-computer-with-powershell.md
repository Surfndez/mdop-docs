---
title: How to manage App-V packages running on a stand-alone computer by using Windows PowerShell (Windows 10)
description: How to manage App-V packages running on a stand-alone computer by using Windows PowerShell.
author: MaggiePucciEvans
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
ms.date: 04/19/2017
---
# How to manage App-V packages running on a stand-alone computer by using Windows PowerShell

>Applies to: Windows 10, version 1607

The following sections explain how to perform various management tasks on a stand-alone client computer with Windows PowerShell cmdlets.

## Return a list of packages

Enter the **Get-AppvClientPackage** cmdlet to return a list of packages entitled to a specific user. Its parameters are *-Name*, *-Version*, *-PackageID*, and *-VersionID*.

For example:

```PowerShell
Get-AppvClientPackage –Name “ContosoApplication” -Version 2
```

## Add a package

Use the **Add-AppvClientPackage** cmdlet to add a package to a computer.

>[!IMPORTANT]
>This example only adds a package. It does not publish the package to the user or the computer.

For example:

```PowerShell
$Contoso = Add-AppvClientPackage \\\\path\\to\\appv\\package.appv
```

## Publish a package

Use the **Publish-AppvClientPackage** cmdlet to publish a package that has been added to a specific user or globally to any user on the computer.

Enter the cmdlet with the application name to publish it to the user.

```PowerShell
Publish-AppvClientPackage “ContosoApplication”
```

To publish the application globally, just add the *-Global* parameter.

```Powershell
Publish-AppvClientPackage “ContosoApplication” -Global
```

## Publish a package to a specific user

>[!NOTE]  
>You must use App-V 5.0 SP2 Hotfix Package 5 or later to use this parameter.

An administrator can publish a package to a specific user by specifying the optional *–UserSID* parameter with the **Publish-AppvClientPackage** cmdlet, where **-UserSID** represents the end user’s security identifier (SID).

To use this parameter:

- You can run this cmdlet from the user or administrator session.
- You must be logged in with administrative credentials to use the parameter.
- The end-user must be signed in.
- You must provide the end user’s security identifier (SID).

For example:

```PowerShell
Publish-AppvClientPackage “ContosoApplication” -UserSID S-1-2-34-56789012-3456789012-345678901-2345
```

## Add and publish a package

Use the **Add-AppvClientPackage** cmdlet to add a package to a computer and publish it to the user.

For example:

```PowerShell
Add-AppvClientPackage \\\\path\\to\\appv\\package.appv | Publish-AppvClientPackage
```

## Unpublish an existing package

Use the following information to unpublish a package which has been entitled to a user but not remove the package from the computer.

**Cmdlet**: Unpublish-AppvClientPackage

**Example**: Unpublish-AppvClientPackage “ContosoApplication”

## Unpublish a package for a specific user


**Note**  
You must use App-V 5.0 SP2 Hotfix Package 5 or later to use this parameter.

 

An administrator can unpublish a package for a specific user by using the optional **–UserSID** parameter with the **Unpublish-AppvClientPackage** cmdlet, where **-UserSID** represents the end user’s security identifier (SID).

To use this parameter:

-   You can run this cmdlet from the user or administrator session.

-   You must be logged in with administrative credentials to use the parameter.

-   The end user must be logged in.

-   You must provide the end user’s security identifier (SID).

**Cmdlet**: Unpublish-AppvClientPackage

**Example**: Unpublish-AppvClientPackage “ContosoApplication” -UserSID S-1-2-34-56789012-3456789012-345678901-2345

## <a href="" id="bkmk-remove-pkg-standalone-posh"></a>To remove an existing package


Use the following information to remove a package from the computer.

**Cmdlet**: Remove-AppvClientPackage

**Example**: Remove-AppvClientPackage “ContosoApplication”

**Note**  
App-V cmdlets have been assigned to variables for the previous examples for clarity only; assignment is not a requirement. Most cmdlets can be combined as displayed in [To add and publish a package](#bkmk-add-pub-pkg-standalone-posh). For a detailed tutorial, see [App-V 5.0 Client PowerShell Deep Dive](https://blogs.technet.microsoft.com/appv/2012/12/03/app-v-5-0-client-powershell-deep-dive/).

 

## <a href="" id="bkmk-admins-pub-pkgs"></a>To enable only administrators to publish or unpublish packages

Starting in App-V 5.0 SP3, you can use the following cmdlet and parameter to enable only administrators (not end users) to publish or unpublish packages:

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Cmdlet</strong></p></td>
<td align="left"><p>Set-AppvClientConfiguration</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Parameter</strong></p></td>
<td align="left"><p>-RequirePublishAsAdmin</p>
<p>Parameter values:</p>
<ul>
<li><p>0 - False</p></li>
<li><p>1 - True</p></li>
</ul>
<p><strong>Example:</strong>: Set-AppvClientConfiguration –RequirePublishAsAdmin1</p></td>
</tr>
</tbody>
</table>

 

To use the App-V Management console to set this configuration, see [How to Publish a Package by Using the Management Console](appv-publish-a-packages-with-the-management-console.md).

## <a href="" id="bkmk-understd-pend-pkgs"></a>Understanding pending packages (UserPending and GlobalPending)


**Starting in App-V 5.0 SP2**: If you run a Windows PowerShell cmdlet that affects a package that is currently in use, the task that you are trying to perform is placed in a pending state. For example, if you try to publish a package when an application in that package is being used, and then run **Get-AppvClientPackage**, the pending status appears in the cmdlet output as follows:

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Cmdlet output item</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>UserPending</p></td>
<td align="left"><p>Indicates whether the listed package has a pending task that is being applied to the user:</p>
<ul>
<li><p>True</p></li>
<li><p>False</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>GlobalPending</p></td>
<td align="left"><p>Indicates whether the listed package has a pending task that is being applied globally to the computer:</p>
<ul>
<li><p>True</p></li>
<li><p>False</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

The pending task will run later, according to the following rules:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Task type</th>
<th align="left">Applicable rule</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>User-based task, e.g., publishing a package to a user</p></td>
<td align="left"><p>The pending task will be performed after the user logs off and then logs back on.</p></td>
</tr>
<tr class="even">
<td align="left"><p>Globally based task, e.g., enabling a connection group globally</p></td>
<td align="left"><p>The pending task will be performed when the computer is shut down and then restarted.</p></td>
</tr>
</tbody>
</table>

For more information about pending tasks, see [Upgrading an in-use App-V package](appv-application-publishing-and-client-interaction.md#upgrading-an-in-use-app-v-package).

## Have a suggestion for App-V? 

Add or vote on suggestions on the [Application Virtualization feedback site](https://appv.uservoice.com/forums/280448-microsoft-application-virtualization).<br>For App-V issues, use the [App-V TechNet Forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=mdopappv).

## Related topics

[Operations for App-V](appv-operations.md)

[Administering App-V by Using Windows PowerShell](appv-administering-appv-with-powershell.md)

