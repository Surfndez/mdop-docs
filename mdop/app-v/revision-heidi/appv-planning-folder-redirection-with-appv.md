---
title: Planning to Use Folder Redirection with App-V (Windows 10)
description: Planning to Use Folder Redirection with App-V
author: MaggiePucciEvans
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
ms.date: 04/19/2017
---
# Planning to Use Folder Redirection with App-V

>Applies to Windows 10, version 1607.

Microsoft Application Virtualization (App-V) supports the use of folder redirection, a feature that enables users and administrators to redirect the path of a folder to a new location.

## Requirements and unsupported scenarios for using folder redirection

(FIX LINKS)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Requirements</p></td>
<td align="left"><p>To use %AppData% folder redirection, you must:</p>
<ul>
<li><p>Have an App-V package that has an AppData virtual file system (VFS) folder.</p></li>
<li><p>Enable folder redirection and redirect users’ folders to a shared folder, typically a network folder.</p></li>
<li><p>Roam both or neither of the following:</p>
<ul>
<li><p>Files under %appdata%\Microsoft\AppV\Client\Catalog</p></li>
<li><p>Registry settings under HKEY_CURRENT_USER\Software\Microsoft\AppV\Client\Packages</p>
<p>For more detail, see [Application publishing and client interaction](appv-application-publishing-and-client-interaction.md#bkmk-clt-inter-roam-reqs).</p></li>
</ul></li>
<li><p>Ensure that the following folders are available to each user who logs into the computer that is running the App-V client:</p>
<ul>
<li><p>%AppData% is configured to the desired network location (with or without [Offline Files](http://technet.microsoft.com/library/cc780552.aspx) support).</p></li>
<li><p>%LocalAppData% is configured to the desired local folder.</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>Unsupported scenarios</p></td>
<td align="left"><ul>
<li><p>Configuring %LocalAppData% as a network drive.</p></li>
<li><p>Redirecting the Start menu to a single folder for multiple users.</p></li>
<li><p>If roaming AppData (%AppData%) is redirected to a network share that is not available, App-V applications will fail to launch, unless the unavailable network share has been enabled for Offline Files.</p></li>
</ul></td>
</tr>
</tbody>
</table>

## How to configure folder redirection for use with App-V

Folder redirection can be applied to different folders, such as Desktop, My Documents, My Pictures, etc. However, the only folder that impacts the use of App-V applications is the user’s roaming AppData folder (%AppData%). You can apply folder redirection to any other supported folders without impacting App-V.

## How folder redirection works with App-V

The following table describes how folder redirection works when %AppData% is redirected to a network and when you have met the requirements listed earlier in this article.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Virtual environment state</th>
<th align="left">Action that occurs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>When the virtual environment starts</p></td>
<td align="left"><p>The virtual file system (VFS) AppData folder is mapped to the local AppData folder (%LocalAppData%) instead of to the user’s roaming AppData folder (%AppData%).</p>
<ul>
<li><p>LocalAppData contains a local cache of the user’s roaming AppData folder for the package in use. The local cache is located under:</p>
<p><code>%LocalAppData%\Microsoft\AppV\Client\VFS\PackageGUID\AppData</code></p></li>
<li><p>The latest data from the user’s roaming AppData folder is copied to and replaces the data currently in the local cache.</p></li>
<li><p>While the virtual environment is running, data continues to be saved to the local cache. Data is served only out of %LocalAppData% and is not moved or synchronized with %AppData% until the end user shuts down the computer.</p></li>
<li><p>Entries to the AppData folder are made using the user context, not the system context.</p></li>
</ul>
</td>
</tr>
<tr class="even">
<td align="left"><p>When the virtual environment shuts down</p></td>
<td align="left"><p>The local cached data in AppData (roaming) is zipped up and copied to the “real” roaming AppData folder in %AppData%. A time stamp, which indicates the last known upload, is simultaneously saved as a registry key under:</p>
<p><code>HKCU\Software\Microsoft\AppV\Client\Packages\&lt;PACKAGE_GUID&gt;\AppDataTime</code></p>
<p>To provide redundancy, App-V keeps the three most recent copies of the compressed data under %AppData%.</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="bkmk-folder-redir-overview"></a>Overview of folder redirection


<table>
<colgroup>
<col width="30%" />
<col width="70%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Purpose</p></td>
<td align="left"><p>Enables end users to work with files, which have been redirected to another folder, as if the files still existed on the local drive.</p></td>
</tr>
<tr class="even">
<td align="left"><p>Description</p></td>
<td align="left"><p>Folder redirection allows users and administrators to redirect the path of a folder to a network location. The documents in the folder are available to the user from any computer on the network.</p>
<ul>
<li><p>Folder redirection allows users and administrators to redirect the path of a folder to a network location. The documents in the folder are available to the user from any computer on the network.</p></li>
<li><p>The new location can be a folder on the local computer or a folder on a shared network.</p></li>
<li><p>Folder redirection updates the files immediately, whereas roaming data is typically synchronized when the user logs in or logs off.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>Usage example</p></td>
<td align="left"><p>You can redirect the Documents folder, which is usually stored on the computer's local hard disk, to a network location. The user can access the documents in the folder from any computer on the network.</p></td>
</tr>
<tr class="even">
<td align="left"><p>More resources</p></td>
<td align="left"><p>[Folder redirection overview](http://technet.microsoft.com/library/cc778976.aspx)</p></td>
</tr>
</tbody>
</table>

## Have a suggestion for App-V?

Add or vote on suggestions on the [Application Virtualization feedback site](http://appv.uservoice.com/forums/280448-microsoft-application-virtualization).<br>For App-V issues, use the [App-V TechNet Forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=mdopappv).
