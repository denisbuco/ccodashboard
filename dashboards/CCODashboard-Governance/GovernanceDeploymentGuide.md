# CCO Azure Governance Dashboard Governance Version 1.0
<div style="text-align: justify">

- [CCO Azure Governance Dashboard Governance Version 1.0](#cco-azure-governance-dashboard-governance-version-10)
  - [Overview](#overview)
    - [Requirements](#requirements)
  - [APIs in use](#apis-in-use)
  - [Resource Providers requirements](#resource-providers-requirements)
- [Installing the custom connector](#installing-the-custom-connector)
- [Setting up the CCO Azure Governance Dashboard Governance](#setting-up-the-cco-azure-governance-dashboard-governance)
  - [Credentials](#credentials)
    - [Clean Credentials on the Data Source](#clean-credentials-on-the-data-source)
    - [Refresh the dashboard](#refresh-the-dashboard)
    - [Credentials for <span>management.azure.com</span> REST API request:](#credentials-for-managementazurecom-rest-api-request)
    - [Credentials for <span>CCO Dashboard Custom Connector</span>:](#credentials-for-cco-dashboard-custom-connector)
    - [Modify Privacy settings](#modify-privacy-settings)
- [Report Pages](#report-pages)
  - [Management Groups and Subscriptions Hierarchy Overview page](#management-groups-and-subscriptions-hierarchy-overview-page)
  - [Tags and naming standards page](#tags-and-naming-standards-page)
  - [Azure Policies page](#azure-policies-page)
  - [Azure Subscription Blueprints page](#azure-subscription-blueprints-page)
  - [Azure Regulatory Compliance Overview tab](#azure-regulatory-compliance-overview-tab)
  - [Azure Resources Regulatory Compliance tab](#azure-resources-regulatory-compliance-tab)

## Overview
The CCO Azure Governance Dashboard is aligned with the Microsoft Cloud Adoption Framework governance principles and will allow to get quick insights around Management Groups, Subscriptions, Blueprints, Polices, Naming Standards, Tagging and Regulatory Standards compliance. The information captured on this Power BI Dashboard can help Cloud Teams, Operations Teams or business decision makers to have a snapshot of the current Azure configuration in just few minutes.

### Requirements

- The CCO Azure Governance Dashboard is a Power BI Template that requires to download and install the Microsoft Power BI Desktop Edition from the Microsoft Store. Below you can find the minimum requirements to run the Dashboard
    -    Windows 10 version **14393.0** or **higher**.
    -    Internet access from the computer running Microsoft Power BI desktop.
    - An Azure account on the desired tenant space with permissions on the subscriptions to read from the Azure Services described above.
    - Install the custom connector and allow the use of any extension to load data without validation or warning. 

## APIs in use
<div style="text-align: justify">
The CCO Azure Governance Dashboard Governance pulls the information from several APIs. You can read the public documentation if you need further information about the calls and methods available:
<br><br>
</div>

| API Name| Dashboard API Version | Last API version | Using latest version|
| --- | :---: | :---: |:---: |
| [Resource Groups](https://docs.microsoft.com/en-us/rest/api/resources/resourcegroups)  |2019-05-01 |2019-05-01|:heavy_check_mark:|
| [Azure Resources](https://docs.microsoft.com/en-us/rest/api/resources/resources)  |2019-05-01 |2019-05-01|:heavy_check_mark:|
| [Azure Subscriptions](https://docs.microsoft.com/en-us/rest/api/resources/subscriptions)  |2019-05-01 |2019-05-01|:heavy_check_mark:|
| [Azure Locations](https://docs.microsoft.com/en-us/rest/api/resources/subscriptions/listlocations)  |2019-05-01 |2019-05-01|:heavy_check_mark:|
| [Azure Blueprints](https://docs.microsoft.com/en-us/rest/api/resources/subscriptions/listlocations)  |2018-11-01-preview |2018-11-01-preview|:heavy_check_mark:|
| [Azure Policies](https://docs.microsoft.com/en-us/rest/api/resources/subscriptions/listlocations)  |2019-09-01 |2019-09-01|:heavy_check_mark:|
| [Azure Regulatory Compliances](https://docs.microsoft.com/en-us/rest/api/resources/subscriptions/listlocations)  |2016-06-01 |2016-06-01|:heavy_check_mark:|



<div style="text-align: justify">


## Resource Providers requirements

Although some of the Resource Providers might be enabled by default, you need to make sure that at least the **Microsoft.Security** resource provider is registered across all the  subscriptions that you plan analyze using the Dashboard. 

Registering this Resource Provider has no cost or performance penalty on the subscription:

1. Click on **Subscriptions**.
2. Click on the Subscription name you want to configure.
3. Click on **Resource Providers**.
4. Click on **Microsoft.Security** and **Register**.

# Installing the custom connector

The new CCO Azure Governance Dashboard requires to install the Power BI Custom Connector that you will find in the same folder as the CCO Governance Dashboard ([CCoDashboardAzureConnector.mez]). This new Custom Connector allows us to leverage new information from Azure Management REST APIs required to put all the information together.

To install the custom connector you must copy the file [CCoDashboardAzureConnector.mez](https://github.com/josunefon/ccodashboard/blob/master/dashboards/CCODashboard-Governance/CcoDashboardAzureConnector.mez) from the **ccodashboard/dashboards/CCODashboard-Governance/** folder to the folder that Power BI creates by default in the Documents folder in your PC. If this folder doesn't exist, you can create a new one with this name.

The path should be **C:\Users\%username%\Documents\Power BI Desktop\Custom Connectors**

![cc](/install/images/customconnectorfolder.PNG)

Then go to Power BI Options and under Global category in the Security section, select **(Not Recommended) Allow any extension to load without validation or warning** and click **OK**. 

![cc](/install/images/customconnectorsecurity.PNG)

# Setting up the CCO Azure Governance Dashboard Governance
## Credentials
By default, the template doesn't have any Azure Account credentials preloaded. Hence, the first step to start showing subscriptions data is to sign-in with the right user credentials.

### Clean Credentials on the Data Source
In some cases, old credentials are cached by previous logins using Power BI Desktop and the dashboard might show errors or blank fields.

- Click on Data sources in **Current file/Global permissions**.
- Click on **Clear Permissions**.
- Click on **Clear All Permissions**.

![credentials1](/install/images/Credentials1.png) ![credentials2](/install/images/Credentials2.png)

### Refresh the dashboard
If the permissions and credentials are properly flushed it should ask you for credentials for each REST API and you will have to set the Privacy Levels for each of them.

- Click on **Refresh**.
  
![refreshgovernance](/install/images/refreshgovernance.png)

### Credentials for <span>management.azure.com</span> REST API request:
- Click on **Organizational Account**.
- Click on **Sign in**.
- Click on **Connect**.
- 
![credentials4](/install/images/Credentials4.png)

### Credentials for <span>CCO Dashboard Custom Connector</span>:
- Click on **Organizational Account**.
- Click on **Sign in**.
- Click on **Connect**.

![cc](/install/images/customconnector.PNG)


### Modify Privacy settings

 - Go to File -> Options -> Privacy and set to Always ignore privacy level settings.

![Privacy](https://user-images.githubusercontent.com/39730064/60920947-3e6d2580-a24e-11e9-9042-f799c9f6fc53.png)

# Report Pages
## Management Groups and Subscriptions Hierarchy Overview page
In this page, you will be able to identify easily the hierarchy within your environment with the view of the Management Groups and Subscriptions.
It's important to mention that this page just gives you a quick view. 

![overview](/install/images/GovernanceOverview.png)

## Tags and naming standards page
In this page you will be able to sort and filter all your Resources and Resource groups based on Tags. It will help you identify any missing Tag and if your naming standards and Tags classifications adheres to your organization guidelines or policies.

![Tagsoverview](/install/images/GovernanceTags.png)

## Azure Policies page
In this page of the report, you will be able to identify the total amount of policies that are you applying in your environment. It will also give a high-level overview of which policies has less compliance level and which resources require more attention.

You can filter the information by:
-  Tenant
-  Management Group with subscriptions
- Subscription
- Policy scope

If you navigate to a impacted resource you will see a quick description of the applied policies.

![policies](/install/images/governancePolicies.png)

## Azure Subscription Blueprints page
In this page of the report, you will be able to identify the total amount of blueprints that are you applying in your environment. It will also show which are the artifacts within the blueprints.

You can filter the information by:
-  Tenant
-  Management Group with subscriptions
- Subscription
- Blueprint Definition
- Published blueprint
- Blueprint Assignment
  

![governanceSubsBlueprints](/install/images/governanceSubsBlueprints.png)

## Azure Regulatory Compliance Overview tab
The fifth tab is used to show the Azure Regulatory Compliance controls level of the environment. It shows the status of the 4 built-in regulatory compliance controls that Azure applies by default to all the environments (SOC TSP, PCI-DSS-3.2, ISO 27001 and Azure CIS 1.1.0).

You can filter the information by:
-  Tenant
-  Management Group with subscriptions
- Subscription
- Resource Groups
    
![regulatorycompliance](/install/images/regulatorycompliance.png)

## Azure Resources Regulatory Compliance tab
In this tab, you will be able to identify which resources are compliant with all the additional regulatory compliance controls. Also it shows how your environment complies with controls and requirements designated by specific regulatory standards and industry benchmarks and provides prescriptive recommendations for how to address these requirements.
(Public preview release of additional supported standards: NIST SP 800-53 R4, SWIFT CSP CSCF v2020, Canada Federal PBMM and UK Official together with UK NHS).

You can filter the information by:
-  Tenant
-  Management Group with subscriptions
- Subscription
- Resource Groups
- Regulatory Standard Name
  
![regulatorycomplianceresources](/install/images/regulatorycomplianceresources.png)
