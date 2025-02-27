---
title: Configure the Client to Receive Package and Connection Groups Updates From the Publishing Server
description: How to Configure the Client to Receive Package and Connection Groups Updates From the Publishing Server
author: aczechowski
ms.assetid: 23b2d03a-20ce-4973-99ee-748f3b682207
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.date: 06/16/2016
---


# Configure the Client to Receive Package and Connection Groups Updates From the Publishing Server


Deploying packages and connection groups using the App-V 5.1 publishing server is helpful because it offers single-point management and high scalability.

Use the following steps to configure the App-V 5.1 client to receive updates from the publishing server.

**Note**  
For the following procedures the management server was installed on a computer named **MyMgmtSrv**, and the publishing server was installed on a computer named **MyPubSrv**.



**To configure the App-V 5.1 client to receive updates from the publishing server**

1.  Deploy the App-V 5.1 management and publishing servers, and add the required packages and connection groups. For more information about adding packages and connection groups, see [How to Add or Upgrade Packages by Using the Management Console](how-to-add-or-upgrade-packages-by-using-the-management-console-51-gb18030.md) and [How to Create a Connection Group](how-to-create-a-connection-group51.md).

2.  To open the management console click the following link, open a browser and type the following: http://MyMgmtSrv/AppvManagement/Console.html in a web browser, and import, publish, and entitle all the packages and connection groups which will be necessary for a particular set of users.

3.  On the computer running the App-V 5.1 client, open an elevated PowerShell command prompt, run the following command:

    **Add-AppvPublishingServer  -Name  ABC  -URL  http:// MyPubSrv/AppvPublishing**

    This command will configure the specified publishing server. You should see output similar to the following:

    Id                        : 1

    SetByGroupPolicy          : False

    Name                      : ABC

    URL                       : http:// MyPubSrv/AppvPublishing

    GlobalRefreshEnabled      : False

    GlobalRefreshOnLogon      : False

    GlobalRefreshInterval     : 0

    GlobalRefreshIntervalUnit : Day

    UserRefreshEnabled        : True

    UserRefreshOnLogon        : True

    UserRefreshInterval       : 0

    UserRefreshIntervalUnit   : Day

    The returned Id – in this case 1

4.  On the computer running the App-V 5.1 client, open a PowerShell command prompt, and type the following command:

    **Sync-AppvPublishingServer  -ServerId  1**

    The command will query the publishing server for the packages and connection groups that need to be added or removed for this particular client based on the entitlements for the packages and connection groups as configured on the management server.

    **Got an App-V issue?** Use the [App-V TechNet Forum](https://social.technet.microsoft.com/Forums/home?forum=mdopappv).

## Related topics


[Operations for App-V 5.1](operations-for-app-v-51.md)









