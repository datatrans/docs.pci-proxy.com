# Release Notes

## January 2022

**New TOKEN endpoint**

The `GET TOKEN` endpoint has been replaced with a new [TOKEN API](../collect/secure-fields-js/#4.-obtain-the-tokens). ****&#x20;

**Idempotency**

We have added Idempotency handling for the [TOKEN API](../collect/secure-fields-js/#4.-obtain-the-tokens). See the details here [https://docs.pci-proxy.com/resources/idempotency](https://docs.pci-proxy.com/resources/idempotency)

**Secure Fields - Added autofill support**

We have added support to autofill expiry date and CVV code for the [Secure Fields](../collect/secure-fields-js/) integration.&#x20;

## September 2021

**Redesign - NoShow authentication email**

We have redesigned the look and feel of the [NoShow authentication](../use/show-interface.md) email.

## July 2021

**New Process for Compliance Check of Receivers**

A new, automated process for the compliance renewal of the Receivers has been introduced.&#x20;

## June 2021

**New Integration - Mobile SDK (Android & iOS)**

Use our mobile libraries for native Android & iOS apps to [tokenize cardholder data](../collect/mobile-sdks.md) and to [process 3D Secure](../authenticate/3d-secure-mobile-sdks.md). &#x20;

## Mai 2021

#### New Value Returned - Status API

In addition to `debit` and `credit` the Status API now also returns `prepaid` in the `card.info.type` property.

## April 2021

**Alias 2.0 - Return fingerprint**

We now return a unique identifier (fingerprint) for the Alias 2.0 from all relevant APIs. Learn more about our various token formats [here](token-formats.md).&#x20;

**Secure Fields API - Bank Account Tokenisation**

We have added support for tokenizing IBAN, Account Number and Branch code to the [Secure Fields ](../collect/secure-fields-js/)integration.&#x20;

## March 2021

#### Dashboard - USD Pricing&#x20;

We have added USD on our pricing page.

## February 2021

#### Dashboard - Enhanced Usage Statistics

We have improved the usage statistics overview. You can now filter usage across all available sources.&#x20;

#### New API Parameter - Status API

We are now returning `transStatusReason` object from the get GET Status API

#### New API Parameter - Token API

We are now returning `CardInfo` object from the GET Token API

#### New API Parameter - PATCH API

It's now possible to update the `currency` with the [PATCH API](../authenticate/3d-secure-fields-js/update-amount-currency.md)

## January 2021

#### Dashboard - Security Improvement

We take security seriously and will check your login password against previously exposed data breaches by using [https://haveibeenpwned.com/](https://haveibeenpwned.com)&#x20;

**New API Paramater - Status API**

We are now returning `cardHolderInfo` object from the [Status API](../authenticate/3d-secure-fields-js/#status-api)

## December 2020

#### New Feature - Traffic Inspector&#x20;

We have added a new feature to monitor and debug traffic in real time. Learn more about the Traffic Inspector [here](pci-proxy-dashboard/traffic-inspector.md).&#x20;

**Improvement - Usage Statistics**&#x20;

We have improved the usage statistics in the PCI Proxy Dashboard. It allows you to filter usage across each single integration assigned to your project on contract level.&#x20;

## November 2020

**New APIs - Token Management**

You can now interact with tokens stored in the PCI Proxy vault with our brand new [Manage APIs](../store/manage/).