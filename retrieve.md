# Retrieve single credit cards

Let us assume you have authorized employees that need to see the original payment data set of a customer.

PCI Proxy enables you to manually retrieve single payment data sets. Basically, it is `a web interface that can convert a token back into its original payment data`. (e.g. to book a no-show, charge payment data via POS terminal, etc.). 

## How to start

There are two ways how you can access and control the interface. You can use our Web Admin Tool and let PCI Proxy handle the user access or call it as an embedded iframe or by redirect in your application. 

*Note: Even though the interface is served by PCI Proxy, your PCI scope can extend.*

**Understanding the process flow:**

![3rd party PULL](3rd Party PULL.png)

## Using our Web Admin Tool

Login to..

## Implement in your application



**Consider a business that needs this ability:**

*You are a travel technology company and process reservations on behalf on your clients against global distribution systems or an online travel agency (e.g. Expedia).*

#### Quick Start Guide:

1. Add a 3rd party to your account
2. POST your XML/SOAP request having PCI Proxy as endpoint.
2. Add HTTP header to your request.


| Test PCI Proxy PULL Endpoint: |
| -- |
| https://pilot.datatrans.biz/upp/proxy/pull/|

- Required HTTP header:

### PCI DSS Compliant User Management

Using the NoShow.jsp requires you to handle your user management in a PCI DSS compliant way. PCI DSS requires certain user and password policies. Below you will find all necessary information for a PCI DSS compliant user management. A more detailed version on PCI DSS user management can be found in the official PCI DSS documents.

### Unique User IDs

Every single user having access to the No-Show.jsp needs to have a unique user login to be clearly identified. Shared user logins are not allowed. 

### Password Policy

In general, the following password rules have to be observed:

 - Passwords must be changed at least every 90 days.
 - The password must have a minimum length of 8 characters.
 - The password must contain upper and lower case letters, numbers and at least one special character.
 - When changing the password none of the last four passwords can be used.
 - After 6 failed login attempts a user account is locked. It can only be unlocked by the administrator.
 - After 15 minutes of inactivity, the password must be entered to reactivate the terminal / session.
 - The maximum session time after which the user must log in again must not exceed 200 minutes.

### No-Show.jsp Usage Logging

Requirement 10

All activity related to the No-Show.jsp has to be logged to provide documentary evidence. Logs must record every time someone accesses regulated data (including cardholder data and log data) to enable a “who-did-what-and-when” audit trail. 
