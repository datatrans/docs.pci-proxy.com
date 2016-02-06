# Getting Started

PCI Proxy is a service that can **securely collect, store and forward credit cards** (payment data) to any payment gateway (e.g. Stripe) or other PCI-certified third party (e.g. Expedia). It can even **extract payment data out of web service calls** (e.g. Booking.com) while allowing the message body to remain unaffected. By using tokenization, our APIs ensure **sensitive payment data never touches your system environment**.

## How it works

![enter image description here](http://thomaas.com/img/thomaas.png)


## Quick Start Guide

Here is a quick step-by-step instruction on how to get started and quickly reduce your PCI scope.

 1. Collect or extract payment data with our APIs 
 2. Use stored payment data
 
Important: Your API key (merchant ID)


On the following pages you will find several sample scripts that run on our test environment. You will notice the merchant ID attribute. Merchant IDs are unique API keys that will identify your environments at PCI Proxy once you are registered. 

You can have multiple merchant IDs. For instance, if you have different environments on which you receive payment data (e.g. website, web service, mobile app), we recommend separating your environments by using a single merchant ID for each.

> For your convenience, we have pre-filled our examples with a test API key so you can start off testing right away.

In order to [go live](golive), you will need to replace the test API key with a production API key. You can get your production keys by [registering an account at PCI Proxy](register).

:::

## Register Account

Before you register an account at PCI Proxy, you can use PCI Proxy only in test mode. With the exception that only test credit cards can be used, all PCI Proxy features are fully available in test mode.

Registering an account at PCI Proxy is simple. Send us an email to setup@pci-proxy.com with your company name and email.


We will return a form, requesting some basic information about your company, contact persons, etc. 