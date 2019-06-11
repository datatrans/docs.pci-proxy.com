---
description: Specific PSD/SCA FAQ. Will be updated continuously
---

# FAQ

## **Expiration Date of Authentication Data**

* **Visa** Merchants are liable for fraud on reauthorisations including a CAVV that is over 90 days old under the Visa rules, however, the CAVV can still be used as evidence that SCA was performed. VACCs over a year old will fail validation by Visa and will be flagged accordingly. Quelle: Visa PSD2 SCA Implementation Guide, Paragraph 4.6.2.3.1.
* **Mastercard** In the current Mastercard rules, there is no limit on the validity of an AAV. It should be valid for at least 90 days. Some Issuers may be able to validate an AAV older than 90 days, which is why a Merchant could try to use an AAV for more than 90 days. If an authorization with a potentially expired AAV \(i.e. more than 90 days old\) is declined, the Merchant could re-send the authorization without the AAV and UCAF data, but the merchant becomes liable in case of fraud \(lost of liability shift\). Quelle: Mastercard Authentication Guide for Europe, Paragraph 2.3.



