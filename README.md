# Welcome

This site aims to be a comprehensive guide to PCI Proxy. You will learn how to integrate the PCI Proxy.

## What is PCI Proxy?

PCI Proxy is an API toolbox that allows you to instantly reduce your PCI scope.

Our webservice API securely **extracts credit cards out of XML/SOAP calls. ** Your XML/SOAP requests and responses remain unchanged. _For instance, you receive XML reservation data from _[_Booking.com_](http://www.booking.com/)_ that contain credit cards._

Our payment page APIs let you **collect payment data on websites or mobile apps**.

By using tokenization, our APIs ensure **sensitive payment data never touch your systems**. Tokens can be used like normal credit cards. You can validate, forward or charge them. Our APIs detokenize them automatically for processing.

### Overview of major features: Collect, Validate, Use.

| [**Collect**](collect_payment_data.html) | [**Validate**](validate.html) | [**Utilize**](utilize) |
| --- | --- | --- |
| From [Web Service](webservice.html) | [Credit Card Check](validate.html) | [Forward](forward.html) |
| From [Website / Application](website-application.html) |  | [Charge](charge.html) |
| From [Mobile App](mobile-app.html) |  | [Show](show.html) |

## Get Started

Here is a quick start guide on how to use PCI Proxy and quickly reduce your PCI scope.

1. [Sign up](https://www.pci-proxy.com/#/signup) for a free test account.
2. [Choose API](collect_payment_data.html) to collect or extract payment data.
3. Explore features, e.g. [validate](validate.html), [charge](charge.html), [forward](forward.html) or [display](retrieve.html) payment data.
4. After successful testing, [activate your account](live_mode-test.html) and reduce your PCI scope.

_Before you activate your account, you can use PCI Proxy for free in test mode. With the exception that only _[_test credit cards_](live_mode-test.html)_ can be used, all PCI Proxy features are fully available in test mode._

**Note: Merchant IDs**

On the following pages you will find several sample scripts that run on our test environment. You will notice the merchant ID attribute. Merchant IDs are unique and identify your environments at PCI Proxy after [sign up](https://www.pci-proxy.com/#/signup).

You can have many merchant IDs. We recommend to use a unique merchant ID for each environment \(web service, website, mobile app\)..

