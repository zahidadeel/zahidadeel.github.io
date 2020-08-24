# Microsoft Azure AD Integration with Keycloak as IdP
Microsoft Azure Active Directory (AD) can be integrated with Keycloak as a third-party Identity Provider (IdP). The overall configuration process is divided into three steps:
- App registration on Microsoft Azure AD
- Microsoft IdP (Identity provider) profile creation in Keycloak
- Linking IdP profile endpoint as redirect URI in newly registered App

## 1. App registration on Microsoft Azure AD
Log into your Azure Portal (portal.azure.com)
Locate and click on Azure Active Directory in the shown menu
Click App Registrations in the left menu and wait for the right side pane to load. Click on New Registration.
Give your app a name. Choose Accounts in any organizational directory (Any Azure AD directory - Multitenant) under the supported account types. Leave Redirect URI (optional) empty for now. We are going to fill it at the very end of the configuration process. Just click on Register to register this app.
Upon registration, the newly registered app will become available in the App Registrations home page. Click on this app name which will load a new page containing a menu on the left side and some client details in right-side pane.
To create a Microsoft IdP profile on Keycloak, we need Client ID and Client Secret. Note down the value of Application (client) ID which will be used as Client ID.
To generate a Client Secret for your app, click on Certificates & Secrets in the left menu. Then click on New Client Secret, choose the expiry period, and click on Add. Save this secret value because it is going to be used in the next step along with Client ID.
Now we need to expose our registered app. From the left menu click on Expose an API then click on Application ID URI to edit it. URI should be relevant to your domain. In the upper right corner, locate and mouse over your user name to find your domain. Use the domain value for your App ID URI. For example, if your domain is zahidadeelxyz.com, your App ID URI should start with https://zahidadeelxyz.com i.e. https://sparkcognition.com/f891c182-157f-49df-98d7-d92b97a1404f

## 2. Create Microsoft IdP Profile in Keycloak
Log into your Keycloak instance.
On the left-side menu, click on Identity Providers.
Use the Add provider drop-down and select Microsoft.
We only require Client ID and Client Secret values (from the section above) to complete this profile registration. Fill in the Client ID and Client Secret values and click on save.
From the very top of this form, copy Redirect URI which should be something like this https://keycloak.zahidadeelxyz.com/auth/realms/DemoRealm/broker/microsoft/endpoint. Note down this Redirect URI value, we will be needing it in the next step.

## 3. Link Keycloak IdP Profile with Azure AD App
This is the last step of this configuration process. We now just need to add our Idp profile URL in our Azure AD app. To do this:
Log into your Azure Portal (portal.azure.com)
Locate and click on Azure Active Directory in the shown menu
Click App Registrations in the left menu and wait for the right side pane to load.
From the left menu, click on Authentication. There under Web section, add Redirect URI (collected from the above section) in the text field and click on save.

Verify the Integration
To verify that everything went quite well. You have to log in to Keycloak through Microsoft account to verify that everything is working fine.
Open the following URL depending upon your realm:

https://keycloak.zahidadeelxyz.com/auth/realms/{realm}/account
For example for DemoRealm realm it would be:
https://keycloak.zahidadeelxyz.com/auth/realms/DemoRealm/account
Open this url. A Microsoft login button will be visible on the login page. Logging in with your Microsoft credentials should be working for you.
