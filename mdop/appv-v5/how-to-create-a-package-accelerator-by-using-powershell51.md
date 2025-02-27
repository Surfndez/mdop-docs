---
title: Create a Package Accelerator by Using PowerShell
description: How to Create a Package Accelerator by Using PowerShell
author: aczechowski
ms.assetid: 0cb98394-4477-4193-8c5f-1c1773c7263a
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.date: 06/16/2016
---


# Create a Package Accelerator by Using PowerShell


App-V 5.1 package accelerators automatically sequence large, complex applications. Additionally, when you apply an App-V 5.1 package accelerator, you are not always required to manually install an application to create the virtualized package.

**To create a package accelerator**

1.  Install the App-V 5.1 sequencer. For more information about installing the sequencer see [How to Install the Sequencer](how-to-install-the-sequencer-51beta-gb18030.md).

2.  To open a PowerShell console click **Start** and type **PowerShell**. Right-click **Windows PowerShell** and select **Run as Administrator**. Use the **New-AppvPackageAccelerator** cmdlet.

3.  To create a package accelerator, make sure that you have the .appv package to create an accelerator from, the installation media or installation files, and optionally a read me file for consumers of the accelerator to use. The following parameters are required to use the package accelerator cmdlet:

    -   **InstalledFilesPath** - specifies the application installation path.

    -   **Installer** – specifies the path to the application installer media

    -   **InputPackagePath** – specifies the path to the .appv package

    -   **Path** – specifies the output directory for the package.

    The following example displays how you can create a package accelerator with an .appv package and the installation media:

    **New-AppvPackageAccelerator -InputPackagePath &lt;path to the .appv file&gt; -Installer &lt;path to the installer executable&gt; -Path &lt;directory of the output path&gt;**

    Additional optional parameters that can be used with the **New-AppvPackageAccelerator** cmdlet are displayed in the following list:

    -   **AcceleratorDescriptionFile** - specifies the path to user created package accelerator instructions. The package accelerator instructions are **.txt** or **.rtf** description files that will be packaged with the package created using the package accelerator.

    **Got an App-V issue?** Use the [App-V TechNet Forum](https://social.technet.microsoft.com/Forums/home?forum=mdopappv).

## Related topics


[Administering App-V 5.1 by Using PowerShell](administering-app-v-51-by-using-powershell.md)

 

 





