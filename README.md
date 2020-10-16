# WabtecOne Platform
WabtecOne platform in short is a sophisticated system designed and developed by WabtecOne team. Platform is a wide concept of WabtecOne to host multiple products to meet the customer needs and demands. These products can be classified as Admin product, remote viewer and many more. Admin product is responsible for driving the platformin many ways.

## WabtecOne Platform is responsible for
1. Managing customers. 
2. Managing customer subscriptions.
3. anaging customer users.
4. Managing products across WabtecOne platform.
5. Managing permissions for platform products
6. Managing user roles.
6. Managing permissions on WabtecOne platform products.
8. Managing licenses

##  Customer Management
WabtecOne products are designed and developed to deal with customers data and are targeted to provide solutions to improve quality of services to their business. Customer management module is designed to onboard a new customer and initiate subscriptions around them. Customer subscriptions can be altered based on demanding needs of a customer. 
Customer Subscriptions Management
Customer Subscription module is designed to define a subscription model around services provided by WabtecOne platform. Customers should get enrolled with subscription(s) to access platform services.

##  User Management
A user is responsible for managing customers data. User management module is designed to enroll new users to system. Users will be mapped to a customer and are associated with different roles based on the intended scope. Customer subscriptions come into picture on maximum number of users a customer can have.

##  Product Management
WabtecOne platform products are designed to serve the customer needs. New products will be designed to serve the demanding needs of customer in many areas such as data analytics, remote viewing of CDU, train management system etc., New avenues and innovations lead to designing of new products. Product management module is designed to configure and enroll products to WabtecOne platform.

## Permission Management
Permission module is designed to define and manage access privileges to a product. Permissions can vary for different products.

##  Roles Management
Roles module is designed to achieve role-based access to products. These roles are assigned to users of a customer based on scope of a user. Roles will be responsible for granting or restricting user access to product resources. Creation, update and deletion of roles are managed across each product.Roles are customer specific .

##  License Management
A product can be categorized as a licensed product or non-licensed product. Licensed products should be tracked to manage the licenses getting consumed. License management module is designed by keeping the aspects of tracking and managing the licenses associated to customer subscriptions.

# Getting Started
## Prerequisites
1. Microsoft Visual Studio 2017
2. .Net Core 2.2
3. Postgress

## Install
Dependent Nuget Packages as below
```
Install-Package WabtecOne.Platform.Model -Version X.X.X
Install-Package WabtecOne.Platform.Common -Version X.X.X
Install-Package WabtecOne.Platform.Security.OktaAd -Version X.X.X
```
Dependent Nuget Packages are available at below endpoint
https://wabtectwo.pkgs.visualstudio.com/WabteONE-Platform/_packaging/torq-wabtecone-platform/nuget/v3/index.json

# EndPoints
WabtecOne Platform Api endpoints can be accessed through multiple ways

| Type    | Url          |
|:--------|:-------------|
| Swagger | https://dev.wabtecone.nonprod.torq.trans.apps.ge.com/swaggerpf/index.html|
| Postman | https://dev.wabtecone.nonprod.torq.trans.apps.ge.com/wabteconepf/svc/api/v1.0/platform/<controller>/{x}|
  
Below are the list of controllers

| controllers   | Description  |
|:------------- |:-------------|
| Customer      | This controller is used for customer related functionality |
| Products      | This controller is used for product related functionality|
| Permissions   | This controller is used for permission related functionality|
| Roles         | This controller is used for roles related functionality|
| ServiceLevels | This controller is used for servicelevel related functionality|
| Users         | This controller is used for user related functionality|
| FloatingProductLicense | This controller is used for product license related functionality |

##  Authentication and Authorization
Authentication is the process of verifying a user’s identity, authorization is the process of verifying that user has been granted permission to perform a specific activity.
 
### Authentication
All WabtecOne Platform Api endpoints fall under authentication. This will happen by decorating each Controller class with [Authorize] attribute. Api endpoints can be authenticated via
  1. Bearer Token - OAuth 2.0
  2. APIKey - Limited access to endpoints

**Bearer Token**
Bearer token is a JSON Web Token (JWT), can be generated through PostMan. Login to PostMan, navigate to Authorization tab and generate new access token by choosing OAuth 2.0
standrad. Please refer to below table for required attributes. 

| Attribute     | Values             |
|:----------------- |:------------------ |
| Token Name        | Random token Name  |
| Grant Type        | Authorization Code |
| Callback URL      | <Callback_url>     |
| Auth URL          | <Auth_url>         |
| Access Token URL  | <Access_Token_URL> |
| Client ID         | <client_id>        |
| Client Secret     | <client_secret>    |
| Scope             | openid email       |
| State             | WM6D               |

**APIKey**
Bearer token works with applications hosted on WabtecOne cluster. Applications hosted on non-wabtecone cluster has to follow "apikey" approach to access platform api. APIkey is secure string shared by the WabtecOne platform team to be passed along with Httprequest. Keep your apikey securely.

| Attribute     | Values          |
|:------------- |:----------------|
| Key           | apikey          |
| Value         | <secure_string> |

**Limitationa on ApiKey**
Below is the list of endpoints can be accessed with ApiKey

| EndPoint          | Description  |
|:------------------|:-------------|
| GetUserByUsername | Retrieves logged in user details by username |

## Authorization
The security of APIs doesn’t stop at authentication, they need an additional authorization to access the resources. Authorization is the process of verifying that a user is granted permission to perform an action.

## DataBase
Postgress is the database used for the WabtecOne Platform.

| Table          | Description  |
|:---------------|:-------------|
| user           | Stores the User info|
| user_role_xref | Stores the User role ref data|
| customer       | stores customer data|
| customer_service_level_xref | stores customer service ref data |
| product        | stores product information |
| permission     | stores permission info |
| role_permission_xref | stores role permission ref data |
| service_level  | stores service leavel info|
| service_level_permission_xref | stores service level permission ref data |
| floating_product_license      | stores licensed product data of customers |
| active_license                | stores active license data from licensed applications |

Below is the list of Organisation Types

| OrgType          | Description  |
|:------------------|:-------------|
| 1 | Railroad |
| 2 | Shipper |
| 3 | Holding company |

# Problems or Suggestions
XBIWabtecOnePlatformTeam@wabtec.com

# integrating header in external applications

Follow the link to integrate the changes 

https://gitlab.torq.trans.apps.ge.com/wabtecone-platform/library/npm/wabtecone-header/edit/develop/README.md
__________________________________________________________________________________________
# Kong Key Auth Plugin Implementation

### Step 1.
Create a new ingress & kong ingress by pointing to the service but with different unique path and kong plugin for key auth

For example, in platform api created new ingress with a unique path & plugin as shown below 

![Alt-Text](/Images/KeyAuth_Ingress_and_kongIngress_screenshot.jpg)

### Step 2.
Create a Kong plugin file with plugin type as Key-auth as shown in the screen shot below.

![Alt-Text](/Images/KeyAuth_Kongplugin_sample_screenshot.jpg)

### Step 3.
Create a KongConsumer & KongCredential yaml to define a unique key for this ingress.

Key can be of 32 char

Note: key should be unique

![Alt-Text](/Images/KeyAuth_KongConsumer_Credential_sample_screenshot.jpg)

### Step 4.
Deploy the ingress kongplugin kongconsumer & kongcredential in torq

### Step 5.
Changes to Api to consume the key auth calls

•	Add a custom authorization filter to authorize the keyauth calls by validating the key 
•	Once kongplugin validate the key then requested will be routed to api with apikey as header and we are again authorizing the request with the custom filter 

Sample Code as shown in below screenshot

![Alt-Text](/Images/KeyAuth_DotNet_Api_Filter_Changes.jpg)

•	Changes to the api controller by adding following attribute to the method 
	AllowAnonymous: To make method available outside Jwt authorization
	Adding Custom Attribute (AuthorizeKeyAuth): so that key auth key which is sent in header get authorized.

As shown Below Screenshot 

![Alt-Text](/Images/KeyAuth_DotNet_Api_Filter_Auth.jpg)

### Step 6.

How to consume the method which is protected with keyauth 

•	Postman:

Use the url which is defined for keyauth ingress followed by api path 

Example: 

Base URL : https://dev.wabtecone.nonprod.torq.trans.apps.ge.com/keyauthpf

Api Path: /api/v1/platform/Users/GetUserByUserName?userName=sjayanthy@wabtec.com

url : https://dev.wabtecone.nonprod.torq.trans.apps.ge.com/keyauthpf/api/v1/platform/Users/GetUserByUserName?userName=sjayanthy@wabtec.com

In authorization tab select API Key and enter following details 

1.  Key: apikey

2.  Value: unique key which was defined in kongcredentials 

And now you can consume it 

Sample as shown in the screenshot below 

![Alt-Text](/Images/KeyAuth_postman_screenshot.jpg)

•	Swagger:

In Swagger Ui click on the Authorize button and enter the key auth key as shown in the below screenshot 

![Alt-Text](/Images/KeyAuth_swagger_screenshot.jpg)

Call the Api method which is exposed to keyauth as shown below 

![Alt-Text](/Images/KeyAuth_swagger_full_screenshot.jpg)

