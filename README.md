# ServiceNow-M365-Health
## Introduction
This application will integrate the Microsoft M365 Service Health &amp; Message Center in [ServiceNow](https://servicenow.com). This app is in beta phase! I do not recommend to install this to a test or production system. Please use a [ServiceNow Development Instance](https://developer.servicenow.com/dev.do) to test this application.

# Preperation

This application is using Microsoft Graph v1.0 API to get ServiceHealth and ServiceAnnouncements from Microsoft. You need to register a application in Azure-AD and give it the permission:
- ServiceMessage.Read.All
- ServiceHealth.Read.All


## Azure AD
### Register Azure Application
Depending on your configuration you may need "global administrator" permission in Azure AD

1.  Go to [Azure Portal](https://portal.azure.com)
2.  Open Azure AD
3.  Go to "App registrations" 
![Azure AD App registrations](images/azure-ad-app-registrations.png?raw=true "Azure AD App registrations")
4.  Click on "New registration"
5.  Enter a name for the application. In my case I choose "ServiceNow DEV"
![Azure AD register app](images/azure-ad-register-an-application.png?raw=true "Azure AD register app")
6.  Save the "Application (client) ID" you need it later in ServiceNow
7.  Go to "Certificates & Secrets" and click on "New client secret" ![Azure AD app secret](images/new-secret.png?raw=true "Azure AD app secret")
8.  Choose how long the secret will be active and enter a description
9.  Save your "Secret ID" you will need this in ServiceNow later

### Add API Permission for this App

1.  Go to "API permission" and click on "Add a permission" ![azure-add-permission](images/azure-add-permission.png?raw=true "azure-add-permission")
2.  Select "Microsoft Graph" ![Microsoft Graph](images/azure-ms-graph.png?raw=true "Microsoft Graph")
3.  Select "Application permission" and add "ServiceHealth.Read.All" ![Microsoft Graph App Permissions](images/azure-app-api.png?raw=true "Microsoft Graph App Permissions")
4.  Repeat this for "ServiceMessage.Read.All"
5.  Your permission should look like this ![Microsoft Graph App Permissions](images/azure-api-permissions.png?raw=true "Microsoft Graph App Permissions")
6.  Click on "Grant admin consent" to activate this permission for this application ![Admin consent](images/azure-admin-consent.png?raw=true "Admin consent")

## ServiceNow
### Import Application Registry entry

1.  Go to your ServiceNow DEV Instance
2.  Open "System OAuth" -> "Appliaction Registry"
3.  Import XML -> Select [application-registry.xml](application-registry.xml) -> This will create "AzureAD ServieNow Integration" in your Appliaction Registry
4.  Edit "AzureAD ServieNow Integration" and add your Client ID and Client Secret you generated in the "Azure AD" part of this manual.
5.  Save your configuration

### Import M365 Health app into ServicNow

1.  Open "Connections &amp; Credentials" -> "Credentials"
2.  Create a new one
3.  Select "Basic Auth Credentials"
4.  Select a name like "GitHub Public"
5.  leave username and password blank
6.  Save it
7.  Open "App Engine Studio" 
8.  Select Import App ![Import App](images/app-studio-import-app.png?raw=true "Import App")