# Welcome 

This site aims to be a comprehensive guide to PCI Proxy. 

## What is PCI Proxy?

PCI Proxy is an API toolbox that allows you to instantly reduce your PCI scope.

You can securely collect, store and forward credit cards (payment data) to payment gateways or PCI-compliant third parties. PCI Proxy can **extract payment data from XML/SOAP calls** (e.g. Booking.com). By using tokenization, our APIs ensure **sensitive payment data never touch your systems**.

PCI Proxy has 3 major features: Collect, Validate, Use. 

|**[Collect](collect_payment_data.html)**|**[Validate](validate.html)**|**[Utilize](utilize)**|
|---|---|---|
|From [Web Service](webservice.html)|[Credit Card Check](validate.html)|[Forward](forward.html)|
|From [Website / Application](website-application.html)||[Charge](charge.html)|
|From [Mobile App](mobile-app.html)||[Show](show.html)|

## Get Started

Here is a quick start guide on how to use PCI Proxy and quickly reduce your PCI scope.

 1. [Sign up](http://www.pci-proxy.com/) for a free test account.
 2. [Choose API](collect_payment_data.html) to collect or extract payment data.
 3. [Explore features](features.html), e.g. [validate](validate.html), [charge](charge.html), [forward](forward.html) or [display](retrieve.html) payment data.
 3. After successful testing, [activate your account](activate) and reduce your PCI scope.

*Before you activate your account, you can use PCI Proxy for free in test mode. With the exception that only [test credit cards](https://www.datatrans.ch/showcase/test-cc-numbers) can be used, all PCI Proxy features are fully available in test mode.*

**Note: Merchant IDs**

On the following pages you will find several sample scripts that run on our test environment. You will notice the merchant ID attribute. Merchant IDs are unique and identify your environments at PCI Proxy after [sign up](http://www.pci-proxy.com/).

You can have many merchant IDs. We recommend separating your environments (web service, website, mobile app) by using a single merchant ID for each.