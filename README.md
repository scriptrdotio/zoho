# About this connector 
This is the second version of the connector for [Zoho](https://www.zoho.com). It wraps part of the CRM and DESK API exposed by zoho with full JavaScript objects that can be directly used from within your scripts in scriptr.io.

The first version is still accessible in [branch v1](https://github.com/scriptrdotio/zoho/tree/v1) of this repository

# How to use
Check the [/test/tests](./test/tests) that contains many usage scenarios.

# How to configure
The /config script contains some variables used to configure the connector. In normal circumstances, you only need to specify/change the values of the following: client_id, client_secret and redirect_uri. 

Before you do that, make sure to create a zoho application using zoho's [developer console] (https://accounts.zoho.com/developerconsole). Note that the "Authorized redirect URIs" field should point to the /oauth/getAccessToken script of your zoho deployment (in your scriptr.io IDE) and must be prefixed with a valid scriptr.io auth token. Example:
```
// the token used in the below is for illustration purposes only
https://api.scriptrapps.io/zoho/oauth/getAccessToken?auth_token=UlIxQMgwRjc3Njl6b9hvXeNvnm5lL3RvckpCDDA1Qjc1RTlBOTA0NEJFMUVBQjcxRkY0ATcxMlc1Nw== 
```
Once done creating the zoho app in zoho's developer console, copy/paste the values of the client_id, client_secret and authorized url respectively into the client_id, client_secret and redirect_uri variables of the config file of the connector.

*Note:* to obtain a scriptr.io auth token, click on your username in the [scriptr.io workspace](https://www.scriptr.io/workspace), then click on "Device directory". Create a device or use an existing one then just copy the generated token.

# How to generate an access token from zoho
You can do this manually using the following steps (or you can automate the process using the same scripts):

- *Step1*: send an authorization grant request by executing the /oauth/getAuthorizationGrant script. Make sure to pass "username=<some_username>" as a query parameter. As a result, you will obtain the URL of the zoho access grant form.
- *Step2*: Open the URL in a browser. Sign-in to zoho and grant the requested permissions. The browser will redirect to the /oauth/getAccessToken script, which will persist the resulting access_token and refresh_token for the provided username.

Starting from there, the zoho connector will automatically refresh the token using the obtained refresh_token.

# Backward compatibility
This version of the connector maintains backward compatibility with the [former version](https://github.com/scriptrdotio/zoho/tree/v1). Any scriptr.io application that was using this latter needs to replace the zoho connector with the new one. The legacy pathes and script names are kept the same. The only required changes are the following:

In the /config file, fill the "user" variable of the "Backward compatibility variables" section with a username for which you already have obtained an access token from zoho (see "How to generate an access token from zoho"). Alternatively, you can specify the user when creating an instance of the zoho compatibility class

Example:
```
var zohoCompatibilityModule = require("/modules/zoho/lib/zoho"); // we assume that the zoho connector is deployed in /modules/zoho
var config = {
        
   user: "username_with_access_token", // you should now pass a username for which you have an access_token
   portal: "your_portal_name",
   department: "your_department_name"
};
    
var legacyZoho = new zohoCompatibilityModule.zoho(config);
```
