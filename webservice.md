# From XML/JSON

If you run a web service that receives or requests messages via API from your partners or clients (channel) that include sensitive payment data, PCI Proxy can extract it and automatically store it securely in PCI Proxys’ vault. 

Together with the stored payment data, a reference number (token) is issued that substitutes the payment data field in your request. The message structure of the channel API always remains the same. The token can be used later on to charge, forward or retrieve payment data. All happens before sensitive payment data ever touch your server to cut your PCI scope. 

> You are allowed to store the token in your system, as it is not PCI DSS relevant.

**PCI Proxy supports push and pull APIs**

In general, you either perform a pull request to receive data or a channel pushes data to your server. PCI Proxy can extract payment data from both operations before sensitive payment data touch your server.

#### Extracting from pull API 
When you perform a pull request against another API, payment data can easily extracted from already sup-ported APIs or by adding a new channel API.

**Consider a business that needs this ability:**

*You are a travel technology company that pulls new reservations from connected reservation portals such as Booking.com. When performing a pull request against Booking.com’s API, you receive booking information including payment data as a response. Booking.com asks all of their IT providers, which receive payment data to be PCI DSS compliant.*

*With the use of PCI Proxy, Booking.com removes this requirement from you, as we as a company are PCI DSS compliant and you can bank on our full Level 1 PCI DSS compliance.* 

##### How to start
You can start and perform the following cURL example. It will give you and understanding of how PCI Proxys’ pull channel API works. Once you have understand it, you can use one of our supported pull channel APIs or add a new pull channel API.  

##### Create New Note [POST]
Create a new note using a title and an optional content body.

+ Request with body (application/json)

    + Body

            {
                "title": "My new note",
                "body": "This is the body"
            }

+ Response 201

+ Response 400 (application/json)

    + Body

            {
                "error": "Invalid title"
            }

+ Request without body (application/json)

    + Body

            {
                "title": "My new note"
            }

+ Response 201

+ Response 400 (application/json)

    + Body

            {
                "error": "Invalid title"
            }


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

### Extracting from push API

Some channels push messages directly to a predefined API endpoint at your server. Because these messages contain sensitive payment data, you will avoid that sensitive data hit your server directly. PCI Proxy allows you to [request an API endpoint](request-push-endpoint) that you can pass on to your channel partner. From now on your channel partner can push messages to PCI Proxy where sensitive payment data will be extracted before the messages are forwarded to your original API endpoint at your server. 

*No worries, our servers and connections are blazing fast and handle a little routing in no time so that response times are kept at a minimum. Please get in touch with us, if you want to know more.*

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

**Activate API endpoint**
Once your tests are successful, you can activate it by sending the following data to setup@pci-proxy.com.

|Information| Description   |
|---|---|
|Merchant ID|Once you [register an account](register) you receive your merchant ID.|
|API Endpoint|Test API endpoint that should be activated|

In return you will receive a unique production push URL for the new push channel that you can pass on to your partner. 


