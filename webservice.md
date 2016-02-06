# Collect payment data from XML/SOAP calls

Let us assume you receive or request messages with sensitive data via API from your partners (channel).

By `switching PCI Proxy between you and the channel`, payment data is extracted and automatically stored in our secure vault. A reference number (token) is issued that substitutes the payment data in the request or response. The message structure of the channel API always remains the same. 

*You are allowed to store the token in your system, as it is not PCI DSS relevant.*

The token can be used later on to charge, forward or retrieve payment data. All happens before sensitive payment data ever touch your server to reduce your PCI scope. 

**Failure Security & Response Times**

*No worries, our servers and connections are blazing fast and handle rerouting in no time so that response times are kept at a minimum. [Read More](webseite-security-site)*

*We have SLAs ready for you. Please [get in touch](start@pci-proxy.com) for more info.*

## How to start

In general, you either perform a pull request to receive data or a channel pushes data to your server. PCI Proxy can extract payment data from both.


```Bild & Prozessbeschreibung MSC beschreiben, dass der entpunkt ausgetauscht wird also pull und push```


### Perform a pull request against another API



**Consider a business that needs this ability:**

*You are a travel technology company pulling new reservations from portals such as Booking.com. As reservations may contain payment data, Booking.com asks for your PCI DSS compliance.*

*By using PCI Proxy, Booking.com removes this requirement from you, because we as a company are PCI DSS compliant and you can bank on our full Level 1 PCI DSS compliance.*



#### Quick Start Guide:

1. POST your XML/SOAP request having PCI Proxy as endpoint.
2. ADD header parameter to your request.


- PCI Proxy Endpoint: ```https://pilot.datatrans.biz/upp/proxy/pull```
- Required HTTP Header:


| HTTP Header      | Description                                                        | Example value
| -------------- | -------------------------------------------------------------------| ---
| `X-CC-URL` | Specifies the target (channel) URL that will be called | https://api.partner.com/
| `X-CC-MERCHANT-ID` | Your merchant ID | 1000011011
| `X-CC-SIGN` | Configured security sign | 130709090849785405
            


```java
    $ curl 
        -X POST 
        -H "Content-Type: text/xml" 
        -H "X-CC-MERCHANT-ID: 1100005433" 
        -H "X-CC-URL: https://api.partner.com/" 
        -H "X-CC-SIGN: 160203112421662698" 
        -d 'yourRequest.xml' 
        "https://pilot.datatrans.biz/upp/proxy/pull"
```



## You receive a request from a partner


**Consider a business that needs this ability:**

*You are a travel technology company receiving new reservations from booking portals on an API endpoint at your server. As reservations may contain sensitive payment data, your servers are in PCI scope.*

*With the use of PCI Proxy, payment data ever touch your server and your reduce your PCI scope.* 

#### Quick Start Guide

1. Request an API endpoint 
2. Change API entpoint at your partner


- PCI Proxy Endpoint: ```https://pilot.datatrans.biz/upp/proxy/push/219e781e517d447c```



PCI Proxy allows you to [request an API endpoint](request-push-endpoint) that you can pass on to your channel partner. From now on your channel partner can push messages to PCI Proxy where sensitive payment data will be extracted before the messages are forwarded to your original API endpoint at your server. 



#### How to start
You can start of with testing by [requesting an API endpoint](request-push-endpoint) for you. If your partner has a test system, pass on the new test API endpoint to him and exchange it with your old API endpoint. Once your tests are successful, you can [activate your API endpoint](activate-push-endpoint) and receive the productive API endpoint.

**Request test API endpoint:**
Please send the following information to setup@pci-proxy.com. 

|Information| Description   |
|---|---|
|Target URL|The URL where we should forward the populated request to (your server).|
|Sample Request & Response|Please include API name, required headers, auth fields, and request method.|
|IP Address|IP address of your partners’ server that will send the push messages.|

In return you will receive a test API endpoint for this push channel.

    ```http
    Example API endpoint: 
    https://pilot.datatrans.biz/upp/proxy/push/e1963c626c6eb4b32
    ```

This push URL is hosted in our PCI Proxy pilot environment to let you test the push channel and make sure you receive the correct data. 


### Supported channel APIs

We support a variety of channel APIs out of the box. Every day, more and more channels get added. Please find below an uncomplete list of channels we already support. In case your required API is not on the list, adding a new channel API is easy. 

    Booking.com – cURL example 

**Adding a new pull channel API**

If your required channel API is not supported yet, you can easily add new pull channel APIs by yourself. Just send us the following information to setup@pci-proxy.com. 

|Information| Description   |
|---|---|
|Target URL|The URL where we should forward the request to.|
|Sample Request & Response|Please include API name, required headers, auth fields, and request method.|


**Activate API endpoint**
Once your tests are successful, you can activate it by sending the following data to setup@pci-proxy.com.

|Information| Description   |
|---|---|
|Merchant ID|Once you [register an account](register) you receive your merchant ID.|
|API Endpoint|Test API endpoint that should be activated|

In return you will receive a unique production push URL for the new push channel that you can pass on to your partner. 


