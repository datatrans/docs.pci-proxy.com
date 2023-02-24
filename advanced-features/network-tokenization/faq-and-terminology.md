# FAQ & Terminology

### Terminology Network Tokenisation&#x20;

| Term  | Description                                                                                                                                                   |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AETS  | American Express Token Service                                                                                                                                |
| CIT   | Customer Initiated. The cardholder is in session and triggered the payment.                                                                                   |
| DPAN  | Device Primary Account Number                                                                                                                                 |
| ECI   | Electronic Commerce Indicator (ECI) security level associated with the Network Token.                                                                         |
| FPAN  | Full Primary Account Number (raw credit card number)                                                                                                          |
| MDES  | Mastercard Digital Enablement Service                                                                                                                         |
| MIT   | Merchant Initiated. They payment is triggered by the merchant in absence of the cardholder.                                                                   |
| OBOTR | On-Behalf-Of Token Requestor. Entity which is requesting a Network Token on behalf of a merchant.                                                             |
| PAN   | Primary Account Number. Plain text credit card number.                                                                                                        |
| TAVV  | Token Authentication Verification Value (Cryptogram). Unique value each transaction which must be sent in the authorisation request to the Payment Provider.  |
| TRID  | Token Request ID - Merchant specific identifier that is used for provisioning Network Tokens.                                                                 |
| TSP   | Token Service Provider - Entity which is issuing the Network Token.                                                                                           |
| VTS   | Visa Token Services                                                                                                                                           |

### FAQ



**Which card brands are supported?**&#x20;

As of November 2022, PCI Proxy is a certified Token Requestor for `VISA VTS` and `MasterCard MDES`. `AMEX AETS` is planned for mid of 2023. For any other brand please contact our team.&#x20;

#### How do I know if a Network Token has been provisioned successfully?&#x20;

Use the [Tokenization API](../../collect/secure-fields-js/#4.-obtain-the-tokens) (if you have a transactionID) or the [Alias Status API](account-lifecycle-management.md#alias-status-api) (if you have a PCI Proxy alias) and look for the `tokenInfo` object if you are not sure if a Network Token has been provisioned.&#x20;

**Can we remove a PAN from the PCI Proxy Vault if a Network Token has been created?**&#x20;

Yes - to remove a PAN mapped to an alias you can make use of the [Alias PATCH API.](../../store/manage/patch.md) Make sure a Network Token has been provisioned before you remove the underlying PAN by calling the [Alias Status API](../../store/manage/status.md).&#x20;

**Do Network Tokens provide any liability shift?**

No - in case you want to shift the liability to the issuer, strong customer authentication is still required. We recommend to use the [3D-Secure APIs](../../authenticate/overview.md) to authenticate cardholders.&#x20;

**Do I need to have a card verification code (CVC) to create a Network Token?**

A CVC is not required for the creation of a Network Token - however, we recommend to check per use-case if you still need to capture the CVC code. Depending on your agreement with the acquirer you might need a CVC code when authorizing with PAN and not Network Tokens.&#x20;



&#x20;&#x20;
