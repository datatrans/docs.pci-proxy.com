# PCI Proxy Documentation

Welcome to PCI Proxy! With this documentation you get familiar with PCI Proxy and reduce your PCI scope in no time.

## Overview

Before we get started, take a minute and let us introduce you to the magic of PCI Proxy.

> ##### PCI Proxy is a tokenization service that reduces your PCI scope in a simple and secure way.

Our customer base spans across many different industries and business types. All of them have specific needs and processes in place. PCI Proxy is build with flexibility in mind to accommodate those needs at best.

PCI Proxy is a battle-tested tokenization solution that is powered by [Datatrans AG](https://www.datatrans.ch/), the leading Swiss Payment Service Provider.

---

## Getting Started

PCI Proxy operates on the following principle:

* #### Step 1: Sign up for your free, dedicated sandbox account. 

* #### Step 1: [Securely collect sensitive card data with one of our APIs](#step1-securely-collect-sensitive-card-data-with-one-of-our-apis)
* #### Step 2: [Use stored card data](#use-stored-card-data)



### Step1: Securely collect sensitive card data

In general, you have different inbound channels where you receive sensitive card data from customers or partners. The three main sources are:

| Website | Webservice | Native App |
| :--- | :--- | :--- |
| Your customers enter their credit card data on a form within your website. | You receive a request from a remote server including credit card data. | Your customers enter their credit card data on a form within your native app. |

In order to avoid sensitive card data touching your systems, you pick the relevant source of credit card data and implement the PCI Proxy according to the respective Quickstart.

#### Quickstart:

With all described methods, **sensitive card data never touch your servers**.

* [**Website:** Seamlessly collect sensitive data within your website.](/website-application.md)
* [**Webservice:** Simply redirect requests with sensitive data through PCI Proxy.](/webservice.md)
* [**Native App:** Natively collect sensitive card data within your mobile app \(iOS / Android\).](/mobile-app.md)

Once sensitive card data is captured, we store the real credit card data in our vaults in Switzerland and return a credit card token to you. Your systems never record, transmit or store real credit card data, only the token. Thus, you are out of PCI scope. With the credit card token linked to the real credit card data, you can now use the token to process the underlying credit card.

---

### Step 2: Use stored card data

PCI Proxy allows you to keep your existing business processes as before. 

We provide three methods for using stored card data:

| Charge | Forward | Show |
| :--- | :--- | :--- |
| Use our payment gateway to charge or validate a stored card. | Pass stored card data on to any PCI-compliant 3rd party. | Let authorized users manually de-tokenize stored card to see it. |





Our Webservice API securely **extracts credit cards out of any XML/SOAP/JSON calls. ** Thereby, your requests and responses remain unchanged. Means, we leave you complete control over your processes. _For instance, you receive XML reservation data from _[_Booking.com_](http://www.booking.com/)\_ or other third party systems that contain credit cards, our webservice API filters the card data and replaces them with a token. The rest of the response will remain unchanged, whit the small difference, that there will be a token instead of a real card number. \_Same procedure if you use our payment page APIs that will let you **collect payment data on websites or mobile apps**.

By using tokenization, our APIs ensure **sensitive payment data never touch your systems**. Tokens can be used like normal credit cards. You can validate, forward or charge them. Our APIs detokenize them automatically for processing.

### Overview of major features: Collect, Validate, Use.

| [**Collect**](collect_payment_data.html) | [**Validate**](validate.html) | [**Utilize**](utilize) |
| --- | --- | --- |
| From [Web Service](webservice.html) | [Credit Card Check](validate.html) | [Forward](forward.html) |
| From [Website / Application](website-application.html) |  | [Charge](charge.html) |
| From [Mobile App](mobile-app.html) |  | [Show](show.html) |

## Quick Start

If you are just getting started with PCI Proxy, it is highly recommended that you start with the get started guide first.

1. [Sign up](https://www.pci-proxy.com/#/signup) for a free test account.
2. [Choose API](collect_payment_data.html) to collect or extract payment data.
3. Explore features, e.g. [validate](validate.html), [charge](charge.html), [forward](forward.html) or [display](retrieve.html) payment data.
4. After successful testing, [activate your account](live_mode-test.html) and reduce your PCI scope.

_Before you activate your account, you can use PCI Proxy for free in test mode. With the exception that only _[_test credit cards_](live_mode-test.html)_ can be used, all PCI Proxy features are fully available in test mode._

# Questions? {#questions}



