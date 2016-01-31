Getting Started
===============

PCI Proxy is a service that can **securely collect, store and forward credit cards** (payment data) to any payment gateway (e.g. Stripe) or other PCI-certified third party (e.g. Expedia). It can even **extract payment data out of web service calls** (e.g. Booking.com) while allowing the message body to remain unaffected. By using tokenization, our APIs ensure **sensitive payment data never touches your system environment**.

##How it works
Bild mit komplettem Prozess (Inbound & Outbound)
![enter image description here](http://thomaas.com/img/thomaas.png)

##Quick Start Guide

Here is a quick step-by-step instruction on how to get started and quickly reduce your PCI scope.

 1. Collect or extract payment data with our APIs 
 2. Use stored payment data

####Important: Your API key (merchant ID)
> For your convenience, we have pre-filled our examples with a test API key so you can start off testing right away.

On the following pages you will find several sample scripts that run on our test environment. You will notice the merchant ID attribute. Merchant IDs are unique API keys that will identify your environments at PCI Proxy once you are registered. 

You can have multiple merchant IDs. For instance, if you have different environments on which you receive payment data (e.g. website, web service, mobile app), we recommend separating your environments by using a single merchant ID for each.

In order to [go live](golive), you will need to replace the test API key with a production API key. You can get your production keys by [registering an account at PCI Proxy](register).

### Register Account

Before you register an account at PCI Proxy, you can use PCI Proxy only in test mode. With the exception that only test credit cards can be used, all PCI Proxy features are fully available in test mode.
Registering an account at PCI Proxy is simple. You send us an email to setup@pci-proxy.com with the following information:

|Information|
|---|
|Company name|
|Language|
|Country|	

We will return a form, requesting some basic information about your company, contact persons, etc. 

Sample Business Cases
=====================

The following list of business cases is not complete and should only give an overview of business types that already use PCI Proxy.

## Middle Office

*You are a middle office that receives booking information on behalf of your clients.*

*Travel agencies use your software to drop new bookings. At some point, they will enter the customers’ payment data in your software. In order to minimize your PCI scope, this payment data should be added without touching your server.*

> PCI Proxy supports a varienty of [different approaches for you to collect the payment data][1]. Your server will never get in touch with sensitive card data which reduces your PCI scope immediately.

> The most common approach is to submit data directly from your software using our [payment pages][2]. Another option is [pay-by-email][3] where temporary payment links are issued that can be emailed to customers to let them enter their payment details by themselves. 

*On behalf of your clients you want to process the booking or transact with different endpoints (e.g. Expedia, Stripe, TUI, Lufthansa, etc.).*

> PCI Proxy allows you to [forward vaulted payment data][4] to PCI compliant third parties.



## Channel Manager

*You are a channel manager that requests or receives booking information from distribution channels, e.g. [Booking.com][5].*

*Hotels and accommodation providers transmit availabilities and prices to various distribution channels. It also automatically retrieves bookings including payment data from the online booking platforms.*

> PCI Proxy allows you to [extract payment data from web service calls][6] and securely store it in PCI Proxys' vault. Your server will never get in touch with sensitive card data which reduces your PCI scope immediately.

*Generally, you will store payment data only to allow your hotels to charge cards in case of a no-show.*

> PCI Proxy provides several ways on how to [use stored payment data][7]. Your clients can either [retrieve single payment data sets][8], [charge payment data][9] against a payment processor or [forward payment data][4] to a PCI-compliant third party, eg. Expedia.

 [1]: #collect
 [2]: #paymentpages
 [3]: #paybyemail
 [4]: #forward
 [5]: http://www.booking.com/
 [6]: #extract
 [7]: #use
 [8]: #retrieve
 [9]: #charge

Features
========

PCI Proxy has 3 different features: Collect, Validate, Use. 

|Collect|Validate|Use|
|---|---|---|
|from web service|credit card check|Forward|
|from website||Charge|
|from mobile app||Retrieve|

First you need to collect payment data to store it in our secure vault. You will find different approaches on how you can collect or extract payment data from different environments (e.g. web service APIs, website, mobile app). If you have specific environments that are not listed, please get in touch. We are quick and flexible to enhance our Proxy features. 

Once you have collected the payment data, you might want to validate the credit cards and check if the card is valid and can be charged.

As soon as payment data is collected, you can make use of it. You can either forward payment data to PCI-compliant thirdparties (e.g. Expedia), charge payment data through a payment gateway (e.g. Datatrans), or retrieve single payment data sets (e.g. to book a No-Show). 

Collect payment data
====================

Whether you receive payment data via API, accept credit cards on a website or collect them in a mobile app, you can use PCI Proxy APIs. Our APIs automatically tokenize the payment information before they ever touch your systems to instantly reduce your PCI scope. 

PCI Proxy APIs are organized in environments, meaning the different ways on how you could possibly receive or collect payment data. 

**Considering the following cases:**

 - You receive or request messages including payment data via APIs from your partners or clients. For example, you receive transaction related data from Booking.com. [Learn about Extracting.](extract)
 - You collect payment data on a website. For instance, you have an Internet booking engine running on your website. [Learn about Payment Pages.](paymentpage)
 - You have a native mobile app (iOS or Android) and collect payment from customers. For instance, you give your clients the opportunity to book your product or service through a mobile app. [Learn about Payment Libraries.](paymentlib)
 - You need to enter payment data into your system on behalf of your clients. For instance, you are a travel agency that works with a middle office system and want to avoid that employees get in contact with payment data. [Learn about Pay-by-Email.](paybyemail)


##From web service calls
If you run a web service that receives or requests messages via API from your partners or clients (channel) that include sensitive payment data, PCI Proxy can extract it and automatically store it securely in PCI Proxys’ vault. 

Together with the stored payment data, a reference number (token) is issued that substitutes the payment data field in your request. The message structure of the channel API always remains the same. The token can be used later on to charge, forward or retrieve payment data. All of this happens before sensitive payment data ever touch your server to minimize your PCI scope. 

> You are allowed to store the token in your system, as it is not PCI DSS relevant.

**PCI Proxy supports push and pull APIs**
In general, you either perform a pull request to receive data or a channel pushes data to your server. PCI Proxy can extract payment data from both operations before sensitive payment data touch your server.

###Extracting from pull API
When you perform a pull request against another API, payment data can easily extracted from already sup-ported APIs or by adding a new channel API.

**Consider a business that needs this ability:**

*You are a travel technology company that pulls new reservations from connected reservation portals such as Booking.com. When performing a pull request against Booking.com’s API, you receive booking information including payment data as a response. Booking.com asks all of their IT providers, which receive payment data to be PCI DSS compliant. 
With the use of PCI Proxy, Booking.com removes this requirement from you, as we as a company are PCI DSS compliant and you can bank on our full Level 1 PCI DSS compliance.* 

####How to start
You can start and perform the following cURL example. It will give you and understanding of how PCI Proxys’ pull channel API works. Once you have understand it, you can use one of our supported pull channel APIs or add a new pull channel API.  

    API Endpoint / cURL example einfügen

**Supported pull channel APIs**
We support a variety of channel APIs out of the box. Every day, more and more channels get added. Please find below an uncomplete list of channels we already support. In case your required API is not on the list, add-ing a new channel API is easy. 

    Booking.com – cURL example 

**Adding a new pull channel API**
If your required channel API is not supported yet, you can easily add new pull channel APIs by yourself. Just send us the following information to setup@pci-proxy.com. 

|Information| Description   |
|---|---|
|Target URL|The URL where we should forward the populated request to (your server).|
|Sample Request & Response|Please include API name, required headers, auth fields, and request method.|
|IP Address|IP address of your partners’ server that will send the push messages.|

###Extracting from push API

Some channels push messages directly to a predefined API endpoint at your server. Because these messages contain sensitive payment data, you will avoid that sensitive data hit your server directly. PCI Proxy allows you to [request an API endpoint](request-push-endpoint) that you can pass on to your channel partner. From now on your channel partner can push messages to PCI Proxy where sensitive payment data will be extracted before the messages are forwarded to your original API endpoint at your server. 

*No worries, our servers and connections are blazing fast and handle a little routing in no time so that response times are kept at a minimum. Please get in touch with us, if you want to know more.*

####How to start
You can start of with testing by [requesting an API endpoint](request-push-endpoint) for you. If your partner has a test system, pass on the new test API endpoint to him and exchange it with your old API endpoint. Once your tests are successful, you can [activate your API endpoint](activate-push-endpoint) and receive the productive API endpoint.

**Request test API endpoint:**
Please send the following information to setup@pci-proxy.com. 

|Information| Description   |
|---|---|
|Target URL|The URL where we should forward the populated request to (your server).|
|Sample Request & Response|Please include API name, required headers, auth fields, and request method.|
|IP Address|IP address of your partners’ server that will send the push messages.|

In return you will receive a test API endpoint for this push channel.

    Example API endpoint: 
    https://pilot.datatrans.biz/upp/proxy/push/e1963c626c6eb4b32 

This push URL is hosted in our PCI Proxy pilot environment to let you test the push channel and make sure you receive the correct data. 

**Activate API endpoint**
Once your tests are successful, you can activate it by sending the following data to setup@pci-proxy.com.

|Information| Description   |
|---|---|
|Merchant ID|Once you [register an account](register) you receive your merchant ID.|
|API Endpoint|Test API endpoint that should be activated|

In return you will receive a unique production push URL for the new push channel that you can pass on to your partner. 
	
##On a Website

If you run a website where you have customers enter their payment data into a HTML web form, PCI Proxy gives you several options on how to collect payment data and securely store it in PCI Proxys’ vault. Many of them assure your servers never get in touch with sensitive card data and reduce your PCI scope to the minimum.

> Add-on: All available options for collecting payment data offer the possibility to make instant charges to payment data. If you plan to use this feature, please make sure you have a valid acquiring contract with one of the following acquirer (financial institutions).

####How to start
An easy way to start is by integrating our Redirect or Lightbox Payment Page. It takes care of building a conversion-optimised HTML form, validating input fields, and securing your customers' payment data. 

    `<a href="https://pilot.datatrans.biz/upp/jsp/upStart.jsp
    		?merchantId=1100004624
    		&refno=1234567890
    		&amount=1000
    		&currency=CHF
    		&theme=DT2015
    &uppAliasOnly=yes">Collect payment data</a>`

If you need a more customizable approach, you can try our Inline Mode Payment Page. The Inline Mode allows you to integrate the payment form into your website with an iframe. With this approach you can adjust the style of the payment form by applying your custom CSS.

`<iframe width="600" 
	height="500"
	frameborder="0"
	border="0"
	src="https://pilot.datatrans.biz/upp/jsp/upStart.jsp
		?theme=Inline
		&paymentmethod=VIS
		&merchantId=1100004547
		&refno=1337
		&amount=1000
		&uppAliasOnly=yes
		&currency=CHF
		&customTheme=mytheme">`

####Go Live
You will need to replace the test service URL and test merchant ID with your production credentials. You can get your credentials by [registering a free account](register).

##In a Mobile App

If you offer a mobile iOS or Android app to your customers where they can enter payment data, you can use our In-App Payment Libraries (SDKs) to securely collect sensitive payment data and store it in our PCI Proxy vault.

You will find download links to the SDKs and developer manuals on [Datatrans Showcase][1] page.

 [1]: https://www.datatrans.ch/showcase/documentations/technical-documentation

Validate Payment Data
=====================

How to validate

Use Payment Data
================

##Forward Payment Data 

Once you collect and extract sensitive payment data to shield your server and minimize your PCI scope, you will most likely want to use the stored payment data to process, forward or retrieve payment data for several business cases.

PCI Proxy allows you to forward vaulted payment data to PCI compliant third parties. This can be any 3rd party that is PCI compliant them self (e.g. online travel agency, payment processor, hotel, airline, car rental, etc.).

### Set up a new third party receiver

Before you can forward payment data to PCI compliant third parties, we need the following information to approve and whitelist the new third party:

| General Information                                                               |
| --------------------------------------------------------------------------------- |
| Merchant ID - Once you [register an account][3] you receive your merchant ID. |
| Company name and website of third party                                           |
| AOC document of third party as proof of PCI compliance                            |

| Technical Details         | Description                                                                 |
| ------------------------- | --------------------------------------------------------------------------- |
| Target URL                | The URL where we should forward the populated request to (3rd party).       |
| Sample Request & Response | Please include API name, required headers, auth fields, and request method. |
| IP Address                | IP address of your server                                                   |

Please send this information to setup@datatrans.ch.

### Pull request to forward data

## Charge Payment Data

> `XML Beispiel`

## Retrieve Payment Data

There might be situations, where you have authorized personell that needs to be able to retrieve single payment data sets. For instance, to book a NoShow. The NoShow.jsp is a web interface that can convert single tokens back into full credit card numbers. This web interface, even though it is served by PCI Proxy, extends your PCI scope. You can call it as an embedded iframe or by redirect. Companies that currently use virtual terminals

Click to see NoShow.jsp in action: [Retrieve single credit card][1]

> `https://pilot.datatrans.biz/upp/jsp/noShow.jsp?merchantId=1100005048
> &aliasCC=70119122433810042
> &salt=xUWnv6TR0RqUyPsVWvxgUn0wXKCuPJjWAumgTy67TVUsimiL0V
> &sign=df9ed6edb62df004ce64db6c113038aa21bd769d866ca7cf305bf43610ce6232`

###Important: PCI DSS Compliant User Management

Using the NoShow.jsp requires you to handle your user management in a PCI DSS compliant way. PCI DSS requires certain user and password policies. Below you will find all necessary information for a PCI DSS compliant user management. A more detailed version on PCI DSS user management can be found in the official PCI DSS documents.

**Unique User IDs**

Every single user having access to the No-Show.jsp needs to have a unique user login to be clearly identified. Shared user logins are not allowed. 

**Password Policy**

In general, the following password rules have to be observed:

>  - Passwords must be changed at least every 90 days.
>  - The password must have a minimum length of 8 characters.
>  - The password must contain upper and lower case letters, numbers and at least one special character.
>  - When changing the password none of the last four passwords can be used.
>  - After 6 failed login attempts a user account is locked. It can only be unlocked by the administrator.
>  - After 15 minutes of inactivity, the password must be entered to reactivate the terminal / session.
>  - The maximum session time after which the user must log in again must not exceed 200 minutes.

**No-Show.jsp Usage Logging**

All activity related to the No-Show.jsp has to be logged to provide documentary evidence. Logs must record every time someone accesses regulated data (including cardholder data and log data) to enable a “who-did-what-and-when” audit trail. 

####Go Live

You will need to replace the test service URL and test merchant ID with your production credentials. You can get your credentials by [registering a free account][2].

**Test Service URL:** 
https://pilot.datatrans.biz/upp/jsp/noShow.jsp 

**Production Service URL:** 
https://production.datatrans.biz/upp/jsp/noShow.jsp


 [1]: https://pilot.datatrans.biz/upp/jsp/noShow.jsp?merchantId=1100005048&aliasCC=70119122433810042&salt=xUWnv6TR0RqUyPsVWvxgUn0wXKCuPJjWAumgTy67TVUsimiL0V&sign=df9ed6edb62df004ce64db6c113038aa21bd769d866ca7cf305bf43610ce6232
 [2]: http://register

