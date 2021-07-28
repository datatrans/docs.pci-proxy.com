---
description: 'See our latest features, changes and improvements on the PCI Proxy platform.'
---

# Release notes

## July 2021

**New process for compliance check of** [**Receivers**](3rd-party-receiver-validation.md)\*\*\*\*

A new, automated process for the compliance renewal of the Receivers has been introduced. 

## June 2021

**New integration - mobile SDK \(Android & iOS\)**

Use our mobile libraries for native Android & iOS apps to [tokenize cardholder data](../collect-and-store-cards/mobile-sdk.md) and to [process 3D Secure](../3d-secure-v2/authentication-only/mobile-sdk-3d.md).  

## Mai 2021

#### New value returned - Status API

In addition to `debit` and `credit` the Status API now also returns `prepaid` in the `card.info.type` property.

## April 2021

**Alias 2.0 - Return fingerprint**

We now return a unique identifier \(fingerprint\) for the Alias 2.0 from all relevant APIs. Learn more about our various token formats [here](../resources/token-format.md). 

**Secure Fields API - bank account tokenisation added**

We have added support for tokenizing IBAN, Account Number and Branch code to the [Secure Fields](../collect-and-store-cards/capture-iframes/) integration. 

## March 2021

#### Dashboard - USD pricing 

We have added USD on our pricing page.

## February 2021

#### Dashboard - Enhanced usage statistics

We have improved the usage statistics overview. You can now filter usage across all available sources. 

#### New API parameter - GET Status API

We are now returning `transStatusReason` object from the get [GET Status API](../3d-secure-v2/authentication-only/securefields-1/#status-api)

#### New API parameter - GET Token API

We are now returning `CardInfo` object from the [GET Token API](../collect-and-store-cards/capture-iframes/#token)

#### New API parameter - PATCH API

It's now possible to update the `currency` with the [PATCH API](../3d-secure-v2/authentication-only/securefields-1/update-a-transaction.md)

## January 2021

#### Dashboard - Security improvement

We take security seriously and will check your login password against previously exposed data breaches by using [https://haveibeenpwned.com/](https://haveibeenpwned.com/) 

**New API paramater - GET Status API**

We are now returning `cardHolderInfo` object from the [GET Status API](../3d-secure-v2/authentication-only/securefields-1/#status-api)

## December 2020

#### New feature - Traffic inspector 

We have added a new feature to monitor and debug traffic in real time. Learn more about the Traffic Inspector [here](pci-proxy-dashboard/traffic-inspector.md). 

**Improvement - Usage statistics** 

We have improved the usage statistics in the PCI Proxy Dashboard. It allows you to filter usage each single integration assigned to your project on Contract level. 

## November 2020

**New APIs - Token management**

You can now interact with tokens stored in the PCI Proxy vault with our brand new Token management APIs. Check out [Manage ](../use-stored-cards/manage.md)to see how they work. 

\*\*\*\*



