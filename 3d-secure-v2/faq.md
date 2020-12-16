---
description: Specific PSD/SCA FAQ. Will be updated continuously
---

# FAQ

## Who is affected by Strong Customer Authentication?

### In scope

Merchants in the European Economic Area \(EEA\) that accept online card payments will be affected by Strong Customer Authentication. This regulation applies to transactions where both the merchant and the merchant's acquirer are are located in the EEA.

### Out of scope

#### One leg out

A merchant does not fall within the scope of PSD2 and SCA if either of the following two criteria is met:

* It does not conduct business in the EEA OR does not offer goods and services to consumers that are based in the EU/EEA **OR**
* It does not use an EEA-based acquirer

{% hint style="warning" %}
#### Strongly recommended

However, we strongly recommend to all merchants offering goods and services to consumers in the EU/EEA to meet the PSD2 requirements for SCA regardless of their location.
{% endhint %}

#### Merchant initiated transactions \(MIT\)

PSD2 and SCA do not regulate merchant initiated transactions, therefore it is regarded as out of scope. Nevertheless SCA has to be applied to the intial merchant initiated transaction.

Please bear in mind that the agreement between merchant and cardholder to setup subsequent merchant initiated transactions requires SCA.

#### Mail and telephone order \(MoTo\)

As MoTo transactions are triggered by agents on behalf of the cardholder, it is not a cardholder initiated transaction and therefore out of scope.

## **Expiration date of authentication data**

* **Visa** Merchants are liable for fraud on reauthorisations including a CAVV that is over 90 days old under the Visa rules, however, the CAVV can still be used as evidence that SCA was performed. VACCs over a year old will fail validation by Visa and will be flagged accordingly.  Source: Visa PSD2 SCA Implementation Guide, Paragraph 4.6.2.3.1.
* **Mastercard** In the current Mastercard rules, there is no limit on the validity of an AAV. It should be valid for at least 90 days. Some Issuers may be able to validate an AAV older than 90 days, which is why a Merchant could try to use an AAV for more than 90 days. If an authorization with a potentially expired AAV \(i.e. more than 90 days old\) is declined, the Merchant could re-send the authorization without the AAV and UCAF data, but the merchant becomes liable in case of fraud \(lost of liability shift\).  Source: Mastercard Authentication Guide for Europe, Paragraph 2.3.

## Grandfathering \(after 14. September 2019\)

* **Visa** For MITs covered by cardholder agreements that were established prior to 14 September 2019, those transactions can continue to be processed without SCA as long as they are identified as MITs using the Visa MIT framework. If the transaction ID of the initial transaction where the mandate was set up is not available, the transaction ID of any related MITs processed before 14 September 2019 can be used. Visa recommends that clients store the transaction ID of the selected transaction and include it in future related MITs to represent the “initial” transaction. However, as stated above, the transaction ID of the previous MIT is also acceptable to use for recurring, installment and unscheduled COF transactions.  Source: Visa Business News of 2 May 2019.
* **Mastercard** Recurring payments solutions already in place on September 14, 2019 \(e.g. existing subscription arrangements like Netflix and Amazon Prime\) do not require SCA. Same principle may be extended to existing MIT solutions.  Source: Mastercard Workshop.

