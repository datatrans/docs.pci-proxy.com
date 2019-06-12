---
description: Specific PSD/SCA FAQ. Will be updated continuously
---

# FAQ

## **Expiration date of authentication data**

* **Visa** Merchants are liable for fraud on reauthorisations including a CAVV that is over 90 days old under the Visa rules, however, the CAVV can still be used as evidence that SCA was performed. VACCs over a year old will fail validation by Visa and will be flagged accordingly.  Source: Visa PSD2 SCA Implementation Guide, Paragraph 4.6.2.3.1.
* **Mastercard** In the current Mastercard rules, there is no limit on the validity of an AAV. It should be valid for at least 90 days. Some Issuers may be able to validate an AAV older than 90 days, which is why a Merchant could try to use an AAV for more than 90 days. If an authorization with a potentially expired AAV \(i.e. more than 90 days old\) is declined, the Merchant could re-send the authorization without the AAV and UCAF data, but the merchant becomes liable in case of fraud \(lost of liability shift\).  Source: Mastercard Authentication Guide for Europe, Paragraph 2.3.

## Grandfathering \(after 14. September 2019\)

* **Visa** For MITs covered by cardholder agreements that were established prior to 14 September 2019, those transactions can continue to be processed without SCA as long as they are identified as MITs using the Visa MIT framework. If the transaction ID of the initial transaction where the mandate was set up is not available, the transaction ID of any related MITs processed before 14 September 2019 can be used. Visa recommends that clients store the transaction ID of the selected transaction and include it in future related MITs to represent the “initial” transaction. However, as stated above, the transaction ID of the previous MIT is also acceptable to use for recurring, installment and unscheduled COF transactions.  Source: Visa Business News of 2 May 2019.
* **Mastercard** Recurring payments solutions already in place on September 14, 2019 \(e.g. existing subscription arrangements like Netflix and Amazon Prime\) do not require SCA. Same principle may be extended to existing MIT solutions.  Source: Mastercard Workshop.

