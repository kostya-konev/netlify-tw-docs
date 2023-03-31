---
title: "Vendor guide creation and update process"
date: 2023-03-09T09:20:00-05:00
draft: false
weight: 1
---
<!-- Weight MUST BE less than 100 -->

{{% notice warning %}}
This article is currently under construction and its contents should not be used until further notice.
{{% /notice %}}

## Creating a new guide

When a vendor guide for an integration needs to be created, a *Tech Doc JIRA Ticket* must be generated requesting that a new guide be created.

Before entering the *Tech Doc JIRA Ticket*, the requestor should email the Teamwork Strategic Partner Manager at partner@teamworkcommerce.com requesting that appropriate SME(s) be assigned to the project.

When creating the ticket, a comment must be added to the ticket supplying the following information:  
- The vendor’s full name.  
- The product or service name.  
- A brief (typically one sentence) overview description of the product or service.  
- The purpose of the product or service.  
- A more detailed description of the product or service (when appropriate).  
- The name of a Technical SME who will be primarily responsible for providing the technical information and images needed by the guide and to review the guide as it is being developed.  
- The name of a Business SME who will be primarily responsible for providing any business or functional information and images needed by the guide and to review the guide as it is being developed.

## Updating a guide

The Tech Writing Team will monitor the POS PRO and CHQ build notifications sent out by the Development Team and if a notification indicates that changes were made which affect a given vendor integration, the Tech Writing Team will determine whether the change(s) need to be reflected in the integration's vendor guide.

If changes need to be made to the guide, the Tech Writer responsible for the update  will email the Teamwork Strategic Partner Manager at partner@teamworkcommerce.com requesting that appropriate SME(s) be assigned to the project.

Once the SME(s) have been identified, the Tech Writer will generate a *Tech Doc JIRA Ticket*.

When creating the ticket, a comment must be added to the ticket supplying the following information:  
- The name of a Technical SME who will be primarily responsible for providing the technical information and images needed by the guide and to review the guide as it is being developed.  
- The name of a Business SME who will be primarily responsible for providing any business or functional information and images needed by the guide and to review the guide as it is being developed.

## Task Checklist

The bulk of the contents of a vendor guide will exist as markdown files presented as part of the *Teamwork Doc Hub* and, therefore, will be created and maintained by the Tech Writing Team. However, for each new guide, a *Task Checklist* page will be created in the *Internal Teamwork Documentation* space in Confluence by the Tech Writer. This page resides in Confluence because its content will be maintained by persons who are not part of the Tech Writing Team.

The guide's *Task Checklist* page in Confluence consists of a list of the tasks which need to be performed before the vendor integration can be released. This list will identify the team who is responsible for performing each task and will include a date for when the task was completed.

As part of creating a new vendor guide, the SME(s) assigned to the project will review the **base task list** (shown below) with the assigned Tech Writer to identify any tasks in the base list which are not appropriate for a given vendor integration and these tasks will not be part of the guide's task list.

In addition, the SME(s) and Tech Writer will add any additional (typically, integration specific) tasks to the guide's task list. For example, the *Adyen Vendor Guide* needed a task added for the setting of Adyen security rights to their proper values in order to ensure that the retailer can access the Adyen service.

<!-- ---- The first entry in the below list MUST BE '1.', any subsequent entry
          numbers can any other value, they will automatically be set sequentially.
-->
The tasks which are part of the **base task list** for a vendor integration are:  
1. Ensure that the Non-Disclosure Agreement has been signed.  
2. Ensure that the Vendor Contract has been signed.  
2. Identify the various vendor contacts.  
2. Establish the marketing contact interval.  
2. Ensure that the Teamwork Commerce Security Questionnaire has been completed.  
2. Obtain any needed billing or financial information from the retailer.
2. Identify the POS PRO software version under which the vendor integration will be released/updated. 
2. Identify the CHQ software version under which the vendor integration will be released/updated.  
2. Identify areas of the integration impacted by changes to POS PRO or CHQ.  
2. Identify and document any appropriate troubleshooting insights for the retailer.  
2. Have the vendor train the Teamwork trainer(s), if needed.  
2. Develop training materials, if needed.  
2. Add training to the Teamwork Academy, if needed.  
2. Train the Pre-implementation Team, if needed.  
2. Train the Implementation Team, if needed.  
2. Train the Sales Team on features and benefits, if needed.  
2. Make a general announcement to Teamwork staff that the vendor integration is available or has been updated.
