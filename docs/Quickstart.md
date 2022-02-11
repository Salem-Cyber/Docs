| [Docs Home](../index.md) |

# Quickstart: Deploy Salem
This quick start will guide you though deployment of Salem, The AI Cyber Security Analyst.

### Prerequisites
Salem current requires you to have:
* An active Azure subscription, including Azure AD
* An active Microsoft 365 license that includes Microsoft Teams

### Objectives
1. **Create Azure AD application registration.**  
*Required to support user authentication*
3. **Deploy Salem from Azure Marketplace.**  
*Requires a private class C IP address block (ex. 10.2.0.0/24)*
4. **Install Salem App in Mircosoft Teams**  
*MS Teams is Salem's primary user interface* 

## Create Azure AD application registration
#### Create App Registration
1. From a web browser, go to the [Azure Portal](https://portal.azure.com) and sign in.
2. From the Azure portal, search for and select 'Azure Active Directory'.
3. Select 'Add' and 'App registration'
4. From the Register an application page:
    * Enter a name
    * Select account type  
    *Typically Single tenant will typically be the best option however Multitenant capability might be useful depending on your situation*
    * Enter Redirect URI. Platform type 'Web' with a value of 'https://token.botframework.com/.auth/web/redirect'
5. Select 'Register'
6. **Note down the Application ID, Object ID, and Directory ID.**

#### Create App Secret
7. Select 'Certificates & secrets'
8. Create 'New client secret'  
*Select a reasonable expiry time, if the secret expires, users will no longer be able to logon to Salem*
9. **Note down the secret value**

#### Create App User Roles
10. Select 'App Roles'
11. Create Application Roles
    * There are three Salem roles (salem.user, salem.analyst, salem.admin) and you an create AD roles that contain any combination of these roles.  For now, create a new role:
        * Display Name: **Salem_Admins**
        * Allowed Member Types: **Users/Groups**
        * Value: **salem.analyst,salem.admin**
        * Description: **Users with this role will have both analyst and admin permissions**

#### Add Users
12. Return to Azure Active Directory in the Azure portal
13. Select 'Enterprise applications'
14. Search for and select the name of the app registration you just created
15. Select 'Users and groups'
16. Add user/group
    * Select a user or group
    * Select the role created above
    * Continue adding individual users as needed.  *NOTE: each user or group can only be assigned on app role*

## Deploy Salem Application
1. From the Azure portal, search for and select 'Marketplace'.
2. Find 'Salem AI Cyber Analyst'.  
*This app may be located in private products under my marketplace*
3. Select and Create
    * App configuration details should have been note when creating the app registration
    * Under 'Network Configuration', provide a non-overlapping class C IP address (meaning an IP address block not in use in any network you may connect to Salem).  These IP address will be used if you peer the Salem Vnet to other Vnets in your Azure subscription.  Network peering will allow you to send and receive information from Salem without needing to connect to the Internet.  Some communication between Azure services will continue to use Azure network routing.
    * It may take 30 minutes or more to fully provision Salem

## Install Salem Teams App
1. Customize Salem app manifest
    * The latest app manifest can be found [here](https://github.com/Salem-Cyber/Utils/tree/main/Teams%20App)
    * Add in the Deployment ID, and Salem Bot Name. *These values can be found from the Salem app in Azure under Parameters and Outputs.  This ID is NOT the ID of the App registration*
2. Create App package
    * create a zip archive containing the manifest.json, Salem_color.png, and Salem_outline.png files at the root level of the archive.
3. From the teams admin portal, upload the app zip package.
4. Once installed, from Microsoft Teams, select Apps and search form Salem AI Cyber Analyst
5. Open Salem
    * after a few seconds, Salem should send you a welcome message and then a login prompt
6. You've no successfully deployed Salem!