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

[contact@pci-proxy.com](mailto:%20contact@pci-proxy.com)
{% endhint %}

## Who is affected by Strong Customer Authentication?

Entities in the European Economic Area \(EEA\) that accept online card payments will be affected by Strong Customer Authentication. This regulation applies to transactions where both the entities and the cardholder’s bank are located in the EEA.

## Exemption \(Merchant-initiated-transactions\) 

Under the SCA regulation, there are some exemptions which can be applied. One of them is to flag transactions as merchant-initiated transactions \(MIT\). Thereby many use-cases require merchants to initiate a payment on behalf of the cardholder when the cardholder is not available to perform the authentication. 

This exemptions can only be given by the merchants acquirer or issuer. If the issuer or acquirer does not agree with the exemption request, MIT flagged transactions may be declined.   
Furthermore you have to inform the cardholder about MIT on behalf of the cardholder. 

If you succesfully applied for a MIT exemption please move on with integrating new 3Dv2 suppported APIs [here](integrations.md). 

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

