#Getting Started


PCI Proxy is a service that can securely collect, store and forward credit cards (payment data) to any payment gateway (e.g. Stripe) or other PCI-certified third party (e.g. Expedia). It can even extract payment data out of exist-ing web service calls (e.g. Booking.com) while allowing the message body to remain unaffected. By using tokeni-zation, our APIs ensure sensitive payment data never touches your system environment.

#Overview
Pic Inbound & Outbound

##Supported Business Cases

The following list of business cases is not complete and should only give an overview of business types that already use PCI Proxy. 

###Middle Office

_You are a mid office that receives booking information on behalf of your clients._

_Travel agencies use your software to drop new bookings. At some point, they will enter the customers’ payment data in your software. In order to minimize your PCI scope, this payment data should be added without touching your server._

PCI Proxy supports a varienty of [different approaches for you to collect the payment data](link). The most common approach is to submit data directly from your software using our [payment pages](link). Another option is [pay-by-email](link) where payment links are issued that can be emailed to customers to let them enter their payment details by them-selves. Now you have shielded your server by using our APIs to extract and collect payment data and stored it in our PCI Proxy vault up front. 

_On behalf of your clients you want to process the booking or transact with different endpoints (e.g. Expedia, Stripe, TUI, Lufthansa, etc.)._

PCI Proxy allows you to [forward vaulted payment data](link) to PCI compliant third parties.

### Channel Manager

_You are a channel manager that requests or receives booking information from booking portals/OTAs, e.g. _[Booking.com](http://www.booking.com/)_.

# Quick Start Guide

Here is a quick step-by-step instruction on how to get started and quickly reduce your PCI scope.

1.	Collect or extract payment data with our APIs
2.	Use stored paymend data 

**Important: Your API key (merchant ID)**

On the following pages you will find several sample scripts that run on our test environment. You will notice the merchant ID attribute. Merchant IDs are unique API keys that will identify your environments at PCI Proxy once you are registered.

You can have multiple merchant IDs. For instance, if you have different environments on which you receive pay-ment data (e.g. website, web service, mobile app), we recommend separating your environments by using a single merchant ID for each.

> _For your convenience, we have pre-filled our examples with a test API key so you can start off testing right away._

In order to go live, you will need to replace the test API key with a production API key. You can get your produc-tion keys by registering an account at PCI Proxy.


```HTTP
GET payment.datatrans.biz/upp/proxy/pull HTTP/1.1X-CC-URL: channel-partner.com/service/
X-CC-XPATH: reservation/customer/cc_number
```





