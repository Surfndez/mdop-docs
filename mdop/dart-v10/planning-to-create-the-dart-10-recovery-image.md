---
title: Planning to create the DaRT 10 recovery image
description: Planning to create the DaRT 10 recovery image.
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/20/2021
---

# Planning to create the DaRT 10 recovery image

Use the information in this section when you are planning to create the Microsoft Diagnostics and Recovery Toolset (DaRT) 10 recovery image.

When you create the DaRT recovery image, you have to decide which tools to include on the image. To make the decision, consider that end users may have access to those tools. If support engineers will take the recovery image media to end users' computers to diagnose issues, you may want to install all of the tools on the recovery image. If you plan to diagnose end user's computers remotely, you may want to disable some of the tools, such as Disk Wipe and Registry Editor, and then enable other tools, including Remote Connection.

When you create the DaRT recovery image, you will also specify whether you want to include additional drivers or files. Determine the locations of any additional drivers or files that you want to include on the DaRT recovery image.

For more information about the DaRT tools, see [Overview of the tools in DaRT 10](overview-of-the-tools-in-dart-10.md). For more information about how to help create a secure recovery image, see [Security considerations for DaRT 10](security-considerations-for-dart-10.md).

## Prerequisites for the recovery image

The following items are required or recommended for creating the DaRT recovery image:

| Prerequisite | Details |
| ------------ | ------- |
| Windows 10 source files | Required to create the DaRT recovery image. Provide the path of a Windows 10 DVD or of Windows 10 source files. |
| [Windows debugging tools](/windows-hardware/drivers/debugger/) | Required when you run the **Crash Analyzer** to determine the cause of a computer failure. We recommend that you specify the path of the Windows Debugging Tools at the time that you create the DaRT recovery image. |
| Optional: Windows symbols files | Typically, debugging information is stored in a symbol file that is separate from the program. You must have access to the symbol information when you debug an application that has stopped responding, for example, if it stopped working. For more information, see [Diagnosing system failures with crash analyzer](diagnosing-system-failures-with-crash-analyzer-dart-10.md). |

## Related topics

- [Planning to Deploy DaRT 10](planning-to-deploy-dart-10.md)
