# Test credentials

## Test Credit and Debit Cards

We have a set of test credit card numbers that you can use in our sandbox environment to test your integration. Limit and 3D support is only needed for transactions and not for tokenization.

{% hint style="warning" %}
Productive credit card information cannot be used in the sandbox.
{% endhint %}

| **Brand**                                          | **Code** | **PAN**          | **Token**                        | **Expiry** | **CVV** | **Limit** | **3D** |
| -------------------------------------------------- | -------- | ---------------- | -------------------------------- | ---------- | ------- | --------- | ------ |
| ![](../.gitbook/assets/logo\_visa.png)             | VIS      | 4242424242424242 | AAABcH0Bq92s3kgAESIAAbGj5NIsAHWC | 06/2025    | 123     | yes       | No     |
| ![](<../.gitbook/assets/logo\_visa (1).png>)       | VIS      | 4900000000000086 | AAABcH0BrE-s3kgAESIAAWdCRyMPAGvp | 06/2025    | 123     | No        | Yes    |
| ![](<../.gitbook/assets/logo\_visa (2).png>)       | VIS      | 4900000000000003 | AAABcH0BrFms3kgAESIAAfHfAmyjACIJ | 06/2025    | 123     | No        | Yes    |
| ![](../.gitbook/assets/logo\_mastercard.png)       | ECA      | 5404000000000001 | AAABcH0BrGOs3kgAESIAAc6gFVXTAGTv | 06/2025    | 123     | Yes       | Yes    |
| ![](<../.gitbook/assets/logo\_mastercard (1).png>) | ECA      | 5200000000000007 | AAABcH0BrG2s3kgAESIAAbmn7rNZAC1l | 06/2025    | 123     | No        | No     |
| ![](<../.gitbook/assets/logo\_mastercard (2).png>) | ECA      | 5200000000000080 | AAABcH0BrHes3kgAESIAAYJ5A6WzAFsz | 06/2025    | 123     | No        | Yes    |
| ![](../.gitbook/assets/logo\_amex.png)             | AMX      | 375811111111115  | AAABcH0BrICs3kgAESIAAQ33vcLxADJm | 06/2025    | 1234    | Yes       | No     |
| ![](<../.gitbook/assets/logo\_amex (1).png>)       | AMX      | 375000000000007  | AAABcH0BrIms3kgAESIAAVp8kILAAAka | 06/2025    | 1234    | No        | Yes    |
| ![](<../.gitbook/assets/logo\_amex (2).png>)       | AMX      | 375811111111123  | AAABcH0BrJ6s3kgAESIAAR0FRZnvADsW | 06/2025    | 1234    | No        | No     |
| ![](../.gitbook/assets/logo\_diners.png)           | DIN      | 36168002586009   | AAABcH0BrKis3kgAESIAARz0vKeyAJP1 | 06/2025    | 123     | Yes       | -      |
| ![](<../.gitbook/assets/logo\_diners (1).png>)     | DIN      | 36167719110012   | AAABcH0BrLKs3kgAESIAAeXMwAnVALLl | 06/2025    | 123     | No        | -      |
| ![](../.gitbook/assets/logo\_discover.png)         | DIS      | 6011000000000004 | AAABcH0BrLys3kgAESIAASKNHo0kAGkv | 06/2025    | 123     | -         | -      |
| ![](../.gitbook/assets/logo\_jcb.png)              | JCB      | 3569990010030442 | AAABcH0BrMas3kgAESIAAQ4E6D72AL1p | 06/2025    | 123     | Yes       | -      |
| ![](<../.gitbook/assets/logo\_jcb (1).png>)        | JCB      | 3569990010030400 | AAABcH0BrM6s3kgAESIAATeCFGr8AHNk | 06/2025    | 123     | No        | No     |
| ![](../.gitbook/assets/logo\_elo.png)              | ELO      | 6550000000000001 | AAABcH0BrNes3kgAESIAAZlN82oMAH2p | 06/2025    | 123     | -         | -      |
| ![](<../.gitbook/assets/logo\_elo (1).png>)        | ELO      | 6362970000457013 | AAABcH0BrOKs3kgAESIAAVLzQBQNADfQ | 06/2025    | 123     | -         | -      |
| ![](../.gitbook/assets/logo\_cup.png)              | CUP      | 6222821234560017 | AAABcH0BrOys3kgAESIAAbnkTiwZAKFg | 06/2025    | -       | No        | Yes    |
| ![](<../.gitbook/assets/logo\_cup (1).png>)        | CUP      | 6223164991230014 | AAABcH0BrPWs3kgAESIAASDQEWOHACL7 | 06/2025    | -       | No        | No     |

| **Limit (Amount / amount range)** | **Error message**                                               |
| --------------------------------- | --------------------------------------------------------------- |
| <= 90.--                          | Transaction authorized                                          |
| > 90.-- and <= 100.--             | Transaction declined (i.e. insufficient limit, bad expiry date) |
| > 110.--                          | Card blocked (lost or stolen)                                   |

## Test IBAN, Account Number, and Branch Code&#x20;

Please use the following credentials to test IBAN, Account Number, and Branch Code tokenization:

{% hint style="warning" %}
Productive bank information cannot be used in the sandbox.
{% endhint %}

| Field            | Number                 |
| ---------------- | ---------------------- |
| `IBAN`           | DE85123456781234512345 |
| `Account Number` | 31510604               |
| `Branch Code`    | 100000                 |

## Test 3D Secure Cards

Use the following test card data to simulate 3D Secure v1 and 3D Secure v2 transactions:

{% hint style="warning" %}
Productive card information cannot be used in the sandbox.
{% endhint %}

| Brand                                                       | Code  | Number           | CVV  | Scenario                           |
| ----------------------------------------------------------- | ----- | ---------------- | ---- | ---------------------------------- |
| ![](../.gitbook/assets/mastercard.svg)Mastercard            | `ECA` | 5200000000000080 | 123  | 3D v1 - challenge authenticated    |
| ![](../.gitbook/assets/mastercard.svg)Mastercard            | `ECA` | 5100001000000022 | 123  | 3D v2 - challenge authenticated    |
| ![](../.gitbook/assets/mastercard.svg)Mastercard            | `ECA` | 5100001000000048 | 123  | 3D v2 - challenge declined         |
| ![](../.gitbook/assets/mastercard.svg)Mastercard            | `ECA` | 5100001000000014 | 123  | 3D v2 - frictionless authenticated |
| ![](../.gitbook/assets/mastercard.svg)Mastercard            | `ECA` | 5100001000000030 | 123  | 3D v2 - frictionless declined      |
| ![](../.gitbook/assets/visa.svg)Visa                        | `VIS` | 4900000000000086 | 123  | 3D v1 - challenge authenticated    |
| ![](../.gitbook/assets/visa.svg)Visa                        | `VIS` | 4000001000000034 | 123  | 3D v2 - frictionless declined      |
| ![](../.gitbook/assets/visa.svg)Visa                        | `VIS` | 4000001000000018 | 123  | 3D v2 - frictionless authenticated |
| ![](../.gitbook/assets/visa.svg)Visa                        | `VIS` | 4000001000000042 | 123  | 3D v2 - challenge declined         |
| ![](../.gitbook/assets/visa.svg)Visa                        | `VIS` | 4000001000000026 | 123  | 3D v2 - challenge authenticated    |
| ![](../.gitbook/assets/card\_amex-old.svg) American Express | `AMX` | 375000000000007  | 1234 | 3D v1 - challenge authenticated    |
| ![](../.gitbook/assets/card\_amex-old.svg) American Express | `AMX` | 340000100000024  | 1234 | 3D v2 - challenge authenticated    |
| ![](../.gitbook/assets/card\_amex-old.svg) American Express | `AMX` | 340000100000040  | 1234 | 3D v2 - challenge declined         |
| ![](../.gitbook/assets/card\_amex-old.svg) American Express | `AMX` | 340000100000016  | 1234 | 3D v2 - frictionless authenticated |
| ![](../.gitbook/assets/card\_amex-old.svg) American Express | `AMX` | 340000100000032  | 1234 | 3D v2 - frictionless declined      |
| ![](../.gitbook/assets/diners.svg)Diners Club               | `DIN` | 30569309025904   | 123  | 3D v2 - challenge authenticated    |
| ![](../.gitbook/assets/discover.svg)Discover                | `DIS` | 6011000000000004 | 123  | 3D v2 - challenge authenticated    |

#### Expiration Date: <a href="#expiration-date" id="expiration-date"></a>

Month: 06 (June)\
Year: 25 (2025)\
Short: 06/25

#### Password for Challenge Flow: <a href="#password-for-challenge-flow" id="password-for-challenge-flow"></a>

Use the following passwords to determine the result of a 3D v2 enrolled card.

4444 = authenticated

4009 = declined

## Add Test Cards

{% hint style="info" %}
[Contact us](mailto:support@pci-proxy.com) if you want to add more test card numbers to your sandbox account.
{% endhint %}
