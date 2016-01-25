#Getting Started


PCI Proxy is a service that can securely collect, store and forward credit cards (payment data) to any payment gateway (e.g. Stripe) or other PCI-certified third party (e.g. Expedia). It can even extract payment data out of exist-ing web service calls (e.g. Booking.com) while allowing the message body to remain unaffected. By using tokeni-zation, our APIs ensure sensitive payment data never touches your system environment.

#Overview
Pic Inbound & Outbound

##PCI Proxy supported business cases
The following list of business cases is not complete and should only give an overview of business types that already use PCI Proxy. 

If you run a web service that receives or requests messages via API from your partners or clients (channel) that in-clude sensitive payment data, PCI Proxy can extract it and automatically store it securely in PCI Proxys’ vault. 
Together with the stored payment data, a reference number (token) is issued that substitutes the payment data field in your request. The message structure of the channel API always remains the same. The token can be used later on to charge, forward or retrieve payment data. All of this happens before sensitive payment data ever touch your server to minimize your PCI scope. 
You are allowed to store the token in your system, as it is not PCI DSS relevant.

If you run a web service that receives or requests messages via API from your partners or clients (channel) that in-clude sensitive payment data, PCI Proxy can extract it and automatically store it securely in PCI Proxys’ vault. 
Together with the stored payment data, a reference number (token) is issued that substitutes the payment data field in your request. The message structure of the channel API always remains the same. The token can be used later on to charge, forward or retrieve payment data. All of this happens before sensitive payment data ever touch your server to minimize your PCI scope. 
You are allowed to store the token in your system, as it is not PCI DSS relevant.


> **Mid Office Example**

> _You are a mid office that receives booking information on behalf of your clients._

> _Travel agencies use your software to drop new bookings. At some point, they will enter the customers’ payment data in your software. In order to minimize your PCI scope, this payment data should be added without touching your server._

> PCI Proxy supports a varienty of [different approaches for you to collect the payment data](link). The most common approach is to submit data directly from your software using our [payment pages](link). Another option is [pay-by-email](link) where payment links are issued that can be emailed to customers to let them enter their payment details by them-selves. Now you have shielded your server by using our APIs to extract and collect payment data and stored it in our PCI Proxy vault up front. 

> _On behalf of your clients you want to process the booking or transact with different endpoints (e.g. Expedia, Stripe, TUI, Lufthansa, etc.)._

> PCI Proxy allows you to [forward vaulted payment data](link) to PCI compliant third parties.

# Quick Start Guide

Here is a quick step-by-step instruction on how to get started and quickly reduce your PCI scope.

1.	Collect or extract payment data with our APIs
2.	Use stored paymend data 

**Important: Your API key (merchant ID)**

On the following pages you will find several sample scripts that run on our test environment. You will notice the merchant ID attribute. Merchant IDs are unique API keys that will identify your environments at PCI Proxy once you are registered.

You can have multiple merchant IDs. For instance, if you have different environments on which you receive pay-ment data (e.g. website, web service, mobile app), we recommend separating your environments by using a single merchant ID for each.

> _For your convenience, we have pre-filled our examples with a test API key so you can start off testing right away._

In order to go live, you will need to replace the test API key with a production API key. You can get your produc-tion keys by registering an account at PCI Proxy.


