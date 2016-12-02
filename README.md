# Welcome to PCI Proxy

Here you will find information on how to integrate with and use the PCI Proxy. We have tried to make this documentation user-friendly and example-filled, but please drop us a line if you see room for improvement.  

## Overview

PCI Proxy is a tokenization service that allows you to reduce your PCI scope. 

Our webservice API securely **extracts credit cards out of XML/SOAP calls. ** Your XML/SOAP requests and responses remain unchanged. *For instance, you receive XML reservation data from [Booking.com](http://www.booking.com/) that contain credit cards.* 

Our payment page APIs let you **collect payment data on websites or mobile apps**. 

By using tokenization, our APIs ensure **sensitive payment data never touch your systems**. Tokens can be used like normal credit cards. You can validate, forward or charge them. Our APIs detokenize them automatically for processing.

### Overview of major features: Collect, Validate, Use. 

|**[Collect](collect_payment_data.html)**|**[Validate](validate.html)**|**[Utilize](utilize)**|
|---|---|---|
|From [Web Service](webservice.html)|[Credit Card Check](validate.html)|[Forward](forward.html)|
|From [Website / Application](website-application.html)||[Charge](charge.html)|
|From [Mobile App](mobile-app.html)||[Show](show.html)|

## Quick Start

The fastest way to get started with PCI Proxy is by following our quick start guide. 

 1. [Sign up](https://www.pci-proxy.com/#/signup) for a free test account.
 2. [Choose API](collect_payment_data.html) to collect or extract payment data.
 3. Explore features, e.g. [validate](validate.html), [charge](charge.html), [forward](forward.html) or [display](retrieve.html) payment data.
 3. After successful testing, [activate your account](live_mode-test.html) and reduce your PCI scope.

*Before you activate your account, you can use PCI Proxy for free in test mode. With the exception that only [test credit cards](live_mode-test.html) can be used, all PCI Proxy features are fully available in test mode.*

**Note: Merchant IDs**

On the following pages you will find several sample scripts that run on our test environment. You will notice the merchant ID attribute. Merchant IDs are unique and identify your environments at PCI Proxy after [sign up](https://www.pci-proxy.com/#/signup).

You can have many merchant IDs. We recommend to use a unique merchant ID for each environment (web service, website, mobile app).