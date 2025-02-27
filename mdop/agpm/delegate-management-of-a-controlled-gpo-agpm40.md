---
title: How to Delegate Management of a Controlled GPO
description: How to Delegate Management of a Controlled GPO
author: aczechowski
ms.assetid: 96b4bfb3-5657-4267-8326-85d7a0db87ce
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.pagetype: mdop
ms.mktglfcycl: manage
ms.sitesec: library
ms.date: 06/16/2016
---


# How to Delegate Management of a Controlled GPO


An Approver can delegate the management of a controlled Group Policy Object (GPO) that was created by that Approver. Like an AGPM Administrator (Full Control), the Approver can delegate access to such a GPO so that selected Editors can edit it, Reviewers can review it, and other Approvers can approve it. By default, an Approver cannot delegate access to GPOs created by another Group Policy administrator.

A user account with the AGPM Administrator (Full Control) role, the user account of the Approver who created the GPO, or a user account with the necessary permissions in Advanced Group Policy Management (AGPM) is required to complete this procedure. Review the details in "Additional considerations" in this topic.

**To delegate the management of a controlled GPO**

1.  In the **Group Policy Management Console** tree, click **Change Control** in the forest and domain in which you want to manage GPOs.

2.  On the **Contents** tab in the details pane, click the **Controlled** tab to display controlled GPOs, and then click the GPO to delegate:

    1.  To add access for a user or group, click the **Add** button, select the user or group, and click **OK**. In the **Add Group or User** dialog box, select a role and click **OK**.

    2.  To remove access for a user or group, select the user or group, and then click the **Remove** button.

        **Note**  
        If a user or group inherits domain-wide access, the **Remove** button is unavailable. You can modify domain-wide access on the **Domain Delegation** tab.



    3.  To modify the roles and permissions delegated to a user or group, click the **Advanced** button. In the **Permissions** dialog box, select the user or group, select the check box for each role to be assigned to that user or group, and then click **OK**.

        **Note**  
        Editor and Approver include Reviewer permissions.



### Additional considerations

-   By default, you must be the Approver who created or controlled the GPO or an AGPM Administrator (Full Control) to perform this procedure. Specifically, you must have **List Contents** permission for the domain and **Modify Security** permission for the GPO.

-   To delegate read access to Group Policy administrators who use AGPM, you must grant them **List Contents** as well as **Read Settings** permissions. This enables them to view GPOs on the **Contents** tab of AGPM. Other permissions must be explicitly delegated.

-   Editors must have **Read** permission for the deployed copy of a GPO to make full use of Group Policy Software Installation.

### Additional references

-   [Creating or Controlling a GPO](creating-or-controlling-a-gpo-agpm40-app.md)









