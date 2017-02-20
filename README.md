# Scriptr Zoho Module
[Zoho](http://www.zoho.com "Zoho") is a CRM and Support as a service platform. 
## Purpose of the scriptr zoho module
This module allows you access to zoho support APIs from scriptr.io, by providing you with a few apis that you can directly call from your own scriptr application. 
For example, using the information about the speed of a vehicle and its oil level, you can create zoho ticket based on the threshold rules for speed and oil you have defined in your application, you can also list all the tickets of the vehicle, as well as update the status of those tickets.

## Configuring Zoho Module

### Zoho account settings
When creating a Zoho Support account, you will have to specify your organization name, which Zoho uses to automatically create a "portal" and a "department".
Hence, if your chose "acme" as an organization name, your default portal and default department will be named "acme" as well.

Note: if you wish to create more portals and departments, you can do this from the setup page

From the "Access Settings" section of your Zoho setup page, make sure to associate a department to your portal

### Authentication token
In order to get access to your Zoho account, you have to generate an access token.
if you are signed in to Zoho, you can obtain a token by sending a request to the following url: https://accounts.zoho.com/apiauthtoken/create?SCOPE=ZohoSupport/supportapi,ZohoSearch/SearchAPI

If you are not signed in to Zoho, you can add your email and password to the above request as in the below example

Example of a request to generate a zoho token: 
`https://accounts.zoho.com/apiauthtoken/nb/create?SCOPE=ZohoSupport/supportapi,ZohoSearch/SearchAPI&EMAIL_ID=your_username&PASSWORD=application_password`
If you don't send EMAIL_ID and PASSWORD you will be redirected to the Zoho login page.

### Zoho Module Config
Once you have a token, update the "zoho/config" file in your scriptr.io workspace, as follows:

Set the value of "supportAuthToken" to the Zoho token you generated,
Set the value of "portal" to the name of the portal you created in Zoho (by default, use the name of your organization)
Set the value of "department" to the name of the department you created in zoho and associated to the portal (by default, use the name of your organization)
