---
description: Merchant Intiated Transaction flow
---

# 3D Secure v2

## Background

The European Banking Authority \(EBA\) has launched the Payment Service Directive 2 \(PSD2\). It regulates all banks and financial institutions in the EEA \(European Economic Area\). In addition, 3D Secure 2 helps to comply with [PSD2 and SCA](https://docs.datatrans.ch/docs/psd2-and-sca). In this guideline we focus on the latest elements to be enforced: Regulatory Technical Standards \(RTS\), on Strong Customer Authentication \(SCA\) and secure communication under PSD2 in relation to [Credit Cards](https://docs.datatrans.ch/docs/credit-cards) schemes for merchant-initiated-transaction. 

## Timeline

On 14th of September 2019 Regulatory Technical Standards \(RTS\) on Strong Customer Authentication \(SCA\) and secure communication under PSD2 comes into effect.

{% hint style="info" %}
We will support you with the integration of 3D Secure 2, whilst trying to keep your required technical resources efforts to a minimum.  
  
Please bear in mind that this guidance is based on our knowledge and best practices within payment industry and therefore still beeing under development. If you have any specific use-cases or questions please send us a message.

contact@pci-proxy.com
{% endhint %}

## Integrations

To apply merchant initiated transactions \(MIT\) you need to authenticate the cardholder on the very first saving of the credit card. We therefore adapt our APIs to mark payments as merchant initiated transactions collected through your frontend. 

As well we are extending the [charge API](../use-stored-cards/authorize.md) to authorise payment requests using authentication data from a third-party 3D Secure 2 provider.

| API | Status |
| :--- | :--- |
| [SecureFields](../collect-and-store-cards/capture-iframes/) \(Frontend\) | Under development |
| [Charge ](../use-stored-cards/authorize.md)\(Server-to-Server\) | Under development |
| [Filter](../collect-and-store-cards/filter-payloads.md) | Supported  |
| [Forward](../use-stored-cards/forward/) | Supported |

## Goal

Advantages of 3D Secure 2 according to the Credit Card schemes:

#### Enhance conversion

* Support of frictionless flow
* No card enrollment during the payment process
* Harmonized look and feel

#### Enhance security

* Risk based analysis
* Strong customer authentication
* Strong support of biometry

#### Support new technology

* Strong support of mobile devices
* Supports non-payment customer authentication as for Wallets or Card on File

