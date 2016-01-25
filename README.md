#Getting Started


PCI Proxy is a service that can securely collect, store and forward credit cards (payment data) to any payment gateway (e.g. Stripe) or other PCI-certified third party (e.g. Expedia). It can even extract payment data out of existing web service calls (e.g. Booking.com) while allowing the message body to remain unaffected. By using tokenization, our APIs ensure sensitive payment data never touches your system environment.

#Overview
Pic Inbound & Outbound

##Supported Business Cases

The following list of business cases is not complete and should only give an overview of business types that already use PCI Proxy. 

###Middle Office

_You are a middle office that receives booking information on behalf of your clients._

_Travel agencies use your software to drop new bookings. At some point, they will enter the customers’ payment data in your software. In order to minimize your PCI scope, this payment data should be added without touching your server._

PCI Proxy supports a varienty of [different approaches for you to collect the payment data](##Register an account). The most common approach is to submit data directly from your software using our [payment pages](link). Another option is [pay-by-email](link) where payment links are issued that can be emailed to customers to let them enter their payment details by them-selves. Now you have shielded your server by using our APIs to extract and collect payment data and stored it in our PCI Proxy vault up front. 

_On behalf of your clients you want to process the booking or transact with different endpoints (e.g. Expedia, Stripe, TUI, Lufthansa, etc.)._

PCI Proxy allows you to [forward vaulted payment data](link) to PCI compliant third parties.

### Channel Manager

_You are a channel manager that requests or receives booking information from distribution channels, e.g. [Booking.com](http://www.booking.com/)._

_Hotels and accommodation providers transmit availabilities and prices to various distribution channels. It also automatically retrieves bookings including payment data from the online booking platforms._

PCI Proxy allows you to [extract payment data from web service calls](link) and securely store it in PCI Proxys' vault. Your server will never get in touch with sensitive card data which reduces your PCI scope immediately.  

_Generally, you will store payment data only to allow your hotels to charge cards in case of a no-show._

PCI Proxy provides several ways on how to [use stored payment data](link). Your clients can either [retrieve payment data](link) via NoShow.jsp, [charge payment data](link) against a payment processor or [forward payment data](link) to a PCI-compliant third party, eg. Expedia.


# Quick Start Guide

Here is a quick step-by-step instruction on how to get started and quickly reduce your PCI scope.

1.	[Collect or extract payment data](link) with our APIs.
2.	[Use stored paymend data](link) to retrieve, charge or forward it.

**Important: Your API key (merchant ID)**

On the following pages you will find several sample scripts that run on our test environment. You will notice the merchant ID attribute. Merchant IDs are unique API keys that will identify your environments at PCI Proxy once you are registered.

You can have multiple merchant IDs. For instance, if you have different environments on which you receive pay-ment data (e.g. website, web service, mobile app), we recommend separating your environments by using a single merchant ID for each.

_For your convenience, we have pre-filled our examples with a test API key so you can start off testing right away._

In order to [go live](link), you will need to replace the test API key with a production API key. You can get your produc-tion keys by [registering an account](link) at PCI Proxy.

##Register an account

Before you register an account at PCI Proxy, you can use PCI Proxy only in test mode. With the exception that only [test credit cards](https://www.datatrans.ch/showcase/test-cc-numbers) can be used, all PCI Proxy features are fully available in test mode.
Registering an account at PCI Proxy is simple. You send us an email to <mailto:setup@pci-proxy.com> with the following information:

| Information needed:        | 
| ------------- |
| Company name      |
| Language      |
| Country |
