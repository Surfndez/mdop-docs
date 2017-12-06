---
title: About the Connection Group File (Windows 10)
description: About the Connection Group File
author: MaggiePucciEvans
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
ms.date: 04/19/2017
---


# About the Connection Group File

**Applies to**
-   Windows 10, version 1607

**In this topic:**

-   [Connection group file purpose and location](#bkmk-cg-purpose-loc)

-   [Structure of the connection group XML file](#bkmk-define-cg-5-0sp3)

-   [Configuring the priority of packages in a connection group](#bkmk-config-pkg-priority-incg)

-   [Supported virtual application connection configurations](#bkmk-va-conn-configs)

## <a href="" id="bkmk-cg-purpose-loc"></a>Connection group file purpose and location


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Connection group purpose</p></td>
<td align="left"><p>A connection group is an App-V feature that enables you to group packages together to create a virtual environment in which the applications in those packages can interact with each other.</p>
<p>Example: You want to use plug-ins with Microsoft Office. You can create a package that contains the plug-ins, and create another package that contains Office, and then add both packages to a connection group to enable Office to use those plug-ins.</p></td>
</tr>
<tr class="even">
<td align="left"><p>How the connection group file works</p></td>
<td align="left"><p>When you apply an App-V connection group file, the packages that are enumerated in the file will be combined at runtime into a single virtual environment. Use the Microsoft Application Virtualization (App-V) connection group file to configure existing App-V connection groups.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Example file path</p></td>
<td align="left"><p>%APPDATA%\Microsoft\AppV\Client\Catalog\PackageGroups\{6CCC7575-162E-4152-9407-ED411DA138F4}\{4D1E16E1-8EF8-41ED-92D5-8910A8527F96}.</p></td>
</tr>
</tbody>
</table>

 

## <a href="" id="bkmk-define-cg-5-0sp3"></a>Structure of the connection group XML file


**In this section:**

-   [Parameters that define the connection group](#bkmk-params-define-cg)

-   [Parameters that define the packages in the connection group](#bkmk-params-define-pkgs-incg)

-   [App-V example connection group XML file](#bkmk-50sp3-exp-cg-xml)

### <a href="" id="bkmk-params-define-cg"></a>Parameters that define the connection group

The following table describes the parameters in the XML file that define the connection group itself, not the packages.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Field</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Schema name</p></td>
<td align="left"><p>Name of the schema.</p>
<p>If you want to use the “optional packages” and “use any version” features that are described in this table, you must specify the following schema in the XML file:</p>
<p><code>xmlns=&quot;http://schemas.microsoft.com/appv/2014/virtualapplicationconnectiongroup&quot;</code></p></td>
</tr>
<tr class="even">
<td align="left"><p>AppConnectionGroupId</p></td>
<td align="left"><p>Unique GUID identifier for this connection group. The connection group state is associated with this identifier. Specify this identifier only when you create the connection group.</p>
<p>You can create a new GUID by typing: <strong>[Guid]::NewGuid()</strong>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>VersionId</p></td>
<td align="left"><p>Version GUID identifier for this version of the connection group.</p>
<p>When you update a connection group (for example, by adding or updating a new package), you must update the version GUID to reflect the new version.</p></td>
</tr>
<tr class="even">
<td align="left"><p>DisplayName</p></td>
<td align="left"><p>Display name of the connection group.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Priority</p></td>
<td align="left"><p>Optional priority field for the connection group.</p>
<p><strong>“0”</strong> - indicates the highest priority.</p>
<p>If a priority is required, but has not been configured, the package will fail because the correct connection group to use cannot be determined.</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="bkmk-params-define-pkgs-incg"></a>Parameters that define the packages in the connection group

In the &lt;Packages&gt; section of the connection group XML file, you list the member packages in the connection group by specifying each package’s unique package identifier and version identifier, as described in the following table. The first package in the list has the highest precedence.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Field</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PackageId</p></td>
<td align="left"><p>Unique GUID identifier for this package. This GUID doesn’t change when newer versions of the package are published.</p></td>
</tr>
<tr class="even">
<td align="left"><p>VersionId</p></td>
<td align="left"><p>Unique GUID identifier for the version of the package.</p>
<p>If you specify <strong>“*”</strong> for the package version, the GUID of the latest available package version is dynamically inserted.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IsOptional</p></td>
<td align="left"><p>Parameter that enables you to make a package optional within the connection group. Valid entries are:</p>
<ul>
<li><p><strong>“true”</strong> – package is optional in the connection group</p></li>
<li><p><strong>“false”</strong> – package is required in the connection group</p></li>
</ul>
</td>
</tr>
</tbody>
</table>

 

### <a href="" id="bkmk-50sp3-exp-cg-xml"></a>App-V example connection group XML file

The following example connection group XML file shows examples of the fields in the previous tables.

```
<?xml version="1.0" encoding="UTF-16"?>
<appv:AppConnectionGroup
xmlns="http://schemas.microsoft.com/appv/2014/virtualapplicationconnectiongroup"
xmlns:appv="http://schemas.microsoft.com/appv/2014/virtualapplicationconnectiongroup"
  AppConnectionGroupId="61BE9B14-D2B4-41CE-A6E3-A1B658DE7000"
  VersionId="E6B6AA57-F2A7-49C9-ADF8-F2B5B3C8A42F"
  Priority="0"
  DisplayName="Sample Connection Group">
  <appv:Packages>
    <appv:Package
      PackageId="1DC709C8-309F-4AB4-BD47-F75926D04276"
      VersionId="*"
      IsOptional=”true”
    />    
    <appv:Package
      PackageId="04220DCA-EE77-42BE-A9F5-96FD8E8593F2"
      VersionId="E15EFFE9-043D-4C01-BC52-AD2BD1E8BAFA"
      IsOptional=”false”
    />
  </appv:Packages>
```

## <a href="" id="bkmk-config-pkg-priority-incg"></a>Configuring the priority of packages in a connection group


Package precedence is configured using the package list order. The first package in the document has the highest precedence. Subsequent packages in the list have descending priority.

Package precedence is the resolution for otherwise inevitable resource collisions during virtual environment initialization. For example, if two packages that are opening in the same virtual environment define the same registry DWORD value, the package with the highest precedence determines the value that is set.

You can use the connection group file to configure each connection group by using the following methods:

-   Specify runtime priorities for connection groups. To edit priority by using the App-V Management Console, click the connection group and then click **Edit**.

    **Note**  
    Priority is required only if the package is associated with more than one connection group.

     

-   Specify package precedence within the connection group.

The priority field is required when a running virtual application initiates from a native application request, for example, Microsoft Windows Explorer. The App-V client uses the priority to determine which connection group virtual environment the application should run in. This situation occurs if a virtual application is part of multiple connection groups.

If a virtual application is opened using another virtual application the virtual environment of the original virtual application will be used. The priority field is not used in this case.

**Example:**

The virtual application Microsoft Outlook is running in virtual environment **XYZ**. When you open an attached Microsoft Word document, a virtualized version Microsoft Word opens in the virtual environment **XYZ**, regardless of the virtualized Microsoft Word’s associated connection groups or runtime priorities.

## <a href="" id="bkmk-va-conn-configs"></a>Supported virtual application connection configurations

The following application connection configurations are supported.

- **An. exe file and plug-in (.dll)**. For example, you might want to distribute Microsoft Office to all users, but distribute a Microsoft Excel plug-in to only a subset of users.

    Enable the connection group for the appropriate users. Update each package individually as required.

- **An. exe file and a middleware application**. You might have an application that requires a middleware application, or several applications that all depend on the same middleware runtime version.

    All computers that require one or more of the applications receive the connection groups with the application and middleware application runtime. You can optionally combine multiple middleware applications into a single connection group.

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">Example</th>
    <th align="left">Example description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>Virtual application connection group for the financial division</p></td>
    <td align="left"><ul>
    <li><p>Middleware application 1</p></li>
    <li><p>Middleware application 2</p></li>
    <li><p>Middleware application 3</p></li>
    <li><p>Middleware application runtime</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Virtual application connection group for HR division</p></td>
    <td align="left"><ul>
    <li><p>Middleware application 5</p></li>
    <li><p>Middleware application 6</p></li>
    <li><p>Middleware application runtime</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>

- **An. exe file and an .exe file**. You might have an application that relies on another application, and you want to keep the packages separate for operational efficiencies, licensing restrictions, or rollout timelines.

    For example, if you are deploying Microsoft Lync 2010, you can use three packages:
    - Microsoft Office 2010    
    - Microsoft Communicator 2007
    - Microsoft Lync 2010<br><br>
    
  You can manage the deployment using the following connection groups:
    - Microsoft Office 2010 and Microsoft Communicator 2007
    - Microsoft Office 2010 and Microsoft Lync 2010<br><br>
    
  When the deployment has completed, you can either create a single new Microsoft Office 2010 + Microsoft Lync 2010 package, or keep and maintain them as separate packages and deploy them by using a connection group.

## Have a suggestion for App-V?

Add or vote on suggestions on the [Application Virtualization feedback site](http://appv.uservoice.com/forums/280448-microsoft-application-virtualization).<br>For App-V issues, use the [App-V TechNet Forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=mdopappv).

## Related topics

[Managing Connection Groups](appv-managing-connection-groups.md)
