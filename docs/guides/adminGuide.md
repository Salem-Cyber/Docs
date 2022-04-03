# Administration Guide

## Topics In this doc

- Access Control
- Configure Salem
- Troubleshoot

### Access Control

#### Salem Chat

Salem uses Role Based Access Control (RBAC) to authorize activity. Currently their are three roles:

| Role          | Description                                    |
| ------------- | ---------------------------------------------- |
| salem.user    | Read only access to Salem                      |
| salem.analyst | React to Salem alerts, incidents and questions |
| salem.admin   | View and manage Salem configurations in chat   |

To create new user roles, refer to the Salem [Quickstart](/guides/Quickstart.md) guide

#### Salem Azure App

Access to Salem Azure application is controlled via the IAM functionality in the [Azure Portal](https://portal.azure.com). From the azure portal, you can view the salem managed application and the Salem managed resource group. You have limited access to make changes to the Salem managed resource group. Review the configuration section of this document for more details

### Configure Salem

There are three types of Salem configurations

| Type | Description |
| ---- | ----------- |
| Alert Configurations | These configuration control how Salem processes alerts, incidents and questions.  Alert Configurations can generally be scoped to specific alerts by source, alert name, and or disposition |
| System Configurations | System configurations control various Salem processing, but can't be scoped to specific alert scenarios  |
| Azure App Configurations | Azure app configures generally relate to network configurations that allow Salem to connect to various systems both inside and outside your organization |

#### Alert Configuration
There are 4 types of configuration files currently supported by Salem:
* [ActionConf](/confSpec/ActionConf.md)
* [ActionDefinition](/confSpec/ActionDefinition.md)
* [ParsingConf](/confSpec/ParsingConf.md)
* [ReportConf](/confSpec/ReportConf.md)

Each file is in JSON format and can be viewed and updated via Salem Chat.  To view configurations type 'configure' in the Salem Chat window.  To make changes to configurations type 'update conf' in the Salem Chat window.

#### System Configuration
System configurations can be viewed and updated from the [Azure Portal](https://portal.azure.com).  They can be found in the app configuration resource within the Salem managed resource group.  Access to this object requires IAM permissions associated with the Salem managed application.  You can find the name of the managed resource group from the overview tab of the Salem managed application.

#### Azure App Configuration
Owners and contributors of the Salme managed application will have access to update some settings for resources in the Salem managed resource group.  These settings include:

* Vnet Peering
* Vnet DNS configuration
* Key Vault Secrets
* App Configuration Keys (for the app configuration resource)
* Event Hub IP network rules

Additionally, you have read permissions over every resource which allows you to implement Azure Policies to monitor changes in Salem resource settings.

### Troubleshoot
Salem Azure Application leverages an Azure Application Insights resource, found in the Azure managed resource group in the [Azure Portal](https://portal.azure.com).  Access to the Application Insights resource requires Owner or Contributor role access for the Azure Managed Application.

Application insights has useful information regarding Salem performance and errors.  Your Salem support contact also has access to this resource and can assist in troubleshooting Salem errors.
