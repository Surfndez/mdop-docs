---
title: How to Convert a Package Created in a Previous Version of App-V (Windows 10)
description: How to Convert a Package Created in a Previous Version of App-V
author: MaggiePucciEvans
ms.pagetype: mdop, appcompat, virtualization
ms.mktglfcycl: deploy
ms.sitesec: library
ms.prod: w10
---


# How to Convert a Package Created in a Previous Version of App-V

**Applies to**
-   Windows 10, version 1607

You can use the package converter utility to upgrade virtual application packages that have been created with previous versions of App-V.

> [!NOTE]  
> If you are running a computer with a 64-bit architecture, you must use the x86 version of Windows PowerShell.

The package converter can only directly convert packages that were created by using the App-V 4.5 sequencer or later. Packages that were created using a version prior to App-V 4.5 must be upgraded to at least App-V 4.5 before conversion.

The following information provides direction for converting existing virtual application packages.

> [!IMPORTANT]  
> You must configure the package converter to always save the package ingredients file to a secure location and directory. A secure location is accessible only by an administrator. Additionally, when you deploy the package, you should save the package to a location that is secure, or make sure that no other user is allowed to be logged in during the conversion process.

## App-V 4.6 installation folder is redirected to virtual file system root

When you convert packages from App-V 4.6 to App-V for Windows 10, the App-V for Windows 10 package can access the hardcoded drive that you were required to use when you created 4.6 packages. The drive letter will be the drive you selected as the installation drive on the 4.6 sequencing machine. (The default drive letter is Q:\\.)

**Technical Details:** The App-V package converter will save the App-V 4.6 installation root folder and short folder names in the FilesystemMetadata.xml file in the Filesystem element. When the App-V for Windows 10 client creates the virtual process, it will map requests from the App-V 4.6 installation root to the virtual file system root.

## Getting started

1.  Install the App-V Sequencer on a computer in your environment. For information about how to install the Sequencer, see [How to Install the Sequencer](appv-install-the-sequencer.md).

2.  The following cmdlets are available:

    -   **Test-AppvLegacyPackage** – This cmdlet is designed to check packages. It will return information about any failures with the package such as missing **.sft** files, an invalid source, **.osd** file errors, or invalid package version. This cmdlet will not parse the **.sft** file or do any in depth validation. For information about options and basic functionality for this cmdlet, using Windows PowerShell, type `Test-AppvLegacyPackage -?`.

    -   **ConvertFrom-AppvLegacyPackage** – To convert an existing package, type `ConvertFrom-AppvLegacyPackage c:\contentStore c:\convertedPackages`. In this command, `c:\contentStore` represents the location of the existing package and `c:\convertedPackages` is the output directory to which the resulting App-V for Windows 10 virtual application package file will be saved. By default, if you do not specify a new name, the old package name will be used.

        Additionally, the package converter optimizes performance of packages in App-V for Windows 10 by setting the package to stream fault the App-V package.  This is more performant than the primary feature block and fully downloading the package. The flag **DownloadFullPackageOnFirstLaunch** allows you to convert the package and set the package to be fully downloaded by default.

        > [!NOTE]  
        > Before you specify the output directory, you must create the output directory.

### Advanced Conversion Tips

-   Piping - Windows PowerShell supports piping. Piping allows you to call `dir c:\contentStore\myPackage | Test-AppvLegacyPackage`. In this example, the directory object that represents `myPackage` will be given as input to the `Test-AppvLegacyPackage` command and bound to the `-Source` parameter. Piping like this is especially useful when you want to batch commands together; for example, `dir .\ | Test-AppvLegacyPackage | ConvertFrom-AppvLegacyAppvPackage -Target .\ConvertedPackages`. This piped command would test the packages and then pass those objects on to actually be converted. You can also apply a filter on packages without errors or only specify a directory which contains an **.sprj** file or pipe them to another cmdlet that adds the filtered package to the server or publishes them to the App-V client.

-   Batching - The Windows PowerShell command enables batching. More specifically, the cmdlets support taking a string\[\] object for the `-Source` parameter which represents a list of directory paths. This allows you to enter `$packages = dir c:\contentStore` and then call `ConvertFrom-AppvLegacyAppvPackage-Source $packages -Target c:\ConvertedPackages` or to use piping and call `dir c:\ContentStore | ConvertFrom-AppvLegacyAppvPackage -Target C:\ConvertedPackages`.

-   Other functionality - Windows PowerShell has other built-in functionality for features such as aliases, piping, lazy-binding, .NET object, and many others. All of these are usable in Windows PowerShell and can help you create advanced scenarios for the Package Converter.

## Have a suggestion for App-V?

Add or vote on suggestions on the [Application Virtualization feedback site](http://appv.uservoice.com/forums/280448-microsoft-application-virtualization).<br>For App-V issues, use the [App-V TechNet Forum](https://social.technet.microsoft.com/Forums/en-US/home?forum=mdopappv).

## Related topics

- [Operations for App-V](appv-operations.md)
