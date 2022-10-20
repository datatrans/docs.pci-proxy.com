# Test credentials

## Test Credit and Debit Cards

We have a set of test credit card numbers that you can use in our sandbox environment to test your integration. Limit and 3D support is only needed for transactions and not for tokenization.

{% hint style="warning" %}
Productive credit card information cannot be used in the sandbox.
{% endhint %}

| **Brand**                                                                      | **Code** | **PAN**          | **Token**                        | **Expiry** | **CVV** | **Limit** | **3D** |
| ------------------------------------------------------------------------------ | -------- | ---------------- | -------------------------------- | ---------- | ------- | --------- | ------ |
| <img src="../.gitbook/assets/logo_visa.png" alt="" data-size="line">           | VIS      | 4242424242424242 | AAABcH0Bq92s3kgAESIAAbGj5NIsAHWC | 06/2025    | 123     | yes       | No     |
| <img src="../.gitbook/assets/logo_visa (1).png" alt="" data-size="line">       | VIS      | 4900000000000086 | AAABcH0BrE-s3kgAESIAAWdCRyMPAGvp | 06/2025    | 123     | No        | Yes    |
| <img src="../.gitbook/assets/logo_visa (2).png" alt="" data-size="line">       | VIS      | 4900000000000003 | AAABcH0BrFms3kgAESIAAfHfAmyjACIJ | 06/2025    | 123     | No        | Yes    |
| <img src="../.gitbook/assets/logo_mastercard.png" alt="" data-size="line">     | ECA      | 5404000000000001 | AAABcH0BrGOs3kgAESIAAc6gFVXTAGTv | 06/2025    | 123     | Yes       | Yes    |
| <img src="../.gitbook/assets/logo_mastercard (1).png" alt="" data-size="line"> | ECA      | 5200000000000007 | AAABcH0BrG2s3kgAESIAAbmn7rNZAC1l | 06/2025    | 123     | No        | No     |
| <img src="../.gitbook/assets/logo_mastercard (2).png" alt="" data-size="line"> | ECA      | 5200000000000080 | AAABcH0BrHes3kgAESIAAYJ5A6WzAFsz | 06/2025    | 123     | No        | Yes    |
| <img src="../.gitbook/assets/logo_amex.png" alt="" data-size="line">           | AMX      | 375811111111115  | AAABcH0BrICs3kgAESIAAQ33vcLxADJm | 06/2025    | 1234    | Yes       | No     |
| <img src="../.gitbook/assets/logo_amex (1).png" alt="" data-size="line">       | AMX      | 375000000000007  | AAABcH0BrIms3kgAESIAAVp8kILAAAka | 06/2025    | 1234    | No        | Yes    |
| <img src="../.gitbook/assets/logo_amex (2).png" alt="" data-size="line">       | AMX      | 375811111111123  | AAABcH0BrJ6s3kgAESIAAR0FRZnvADsW | 06/2025    | 1234    | No        | No     |
| <img src="../.gitbook/assets/logo_diners.png" alt="" data-size="line">         | DIN      | 36168002586009   | AAABcH0BrKis3kgAESIAARz0vKeyAJP1 | 06/2025    | 123     | Yes       | -      |
| <img src="../.gitbook/assets/logo_diners (1).png" alt="" data-size="line">     | DIN      | 36167719110012   | AAABcH0BrLKs3kgAESIAAeXMwAnVALLl | 06/2025    | 123     | No        | -      |
| <img src="../.gitbook/assets/logo_discover.png" alt="" data-size="line">       | DIS      | 6011000000000004 | AAABcH0BrLys3kgAESIAASKNHo0kAGkv | 06/2025    | 123     | -         | -      |
| <img src="../.gitbook/assets/logo_jcb.png" alt="" data-size="line">            | JCB      | 3569990010030442 | AAABcH0BrMas3kgAESIAAQ4E6D72AL1p | 06/2025    | 123     | Yes       | -      |
| <img src="../.gitbook/assets/logo_jcb (1).png" alt="" data-size="line">        | JCB      | 3569990010030400 | AAABcH0BrM6s3kgAESIAATeCFGr8AHNk | 06/2025    | 123     | No        | No     |
| <img src="../.gitbook/assets/logo_elo.png" alt="" data-size="line">            | ELO      | 6550000000000001 | AAABcH0BrNes3kgAESIAAZlN82oMAH2p | 06/2025    | 123     | -         | -      |
| <img src="../.gitbook/assets/logo_elo (1).png" alt="" data-size="line">        | ELO      | 6362970000457013 | AAABcH0BrOKs3kgAESIAAVLzQBQNADfQ | 06/2025    | 123     | -         | -      |
| <img src="../.gitbook/assets/image (18).png" alt="" data-size="line">          | HCP      | 3841000000000007 | 7LHXscqwAAEAAAGCPojFf2wsu9gTAChQ | 06/2025    | 123     | No        | No     |
| <img src="../.gitbook/assets/logo_cup.png" alt="" data-size="line">            | CUP      | 6222821234560017 | AAABcH0BrOys3kgAESIAAbnkTiwZAKFg | 06/2025    | -       | No        | Yes    |
| <img src="../.gitbook/assets/logo_cup (1).png" alt="" data-size="line">        | CUP      | 6223164991230014 | AAABcH0BrPWs3kgAESIAASDQEWOHACL7 | 06/2025    | -       | No        | No     |
|                                                                                |          |                  |                                  |            |         |           |        |

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

Use the following test card data to simulate **3D Secure v2** transaction. 3D Secure v1 enabled cards are not supported anymore by the card brands since October 2022 and will therefore lead to a decline when still used.&#x20;

{% hint style="warning" %}
Productive card information cannot be used in the sandbox.
{% endhint %}

| Brand                                                                                     | Code  | Number           | CVV  | Scenario                           |
| ----------------------------------------------------------------------------------------- | ----- | ---------------- | ---- | ---------------------------------- |
| <img src="../.gitbook/assets/mastercard.svg" alt="" data-size="line">Mastercard           | `ECA` | 5100001000000022 | 123  | 3D v2 - challenge authenticated    |
| <img src="../.gitbook/assets/mastercard.svg" alt="" data-size="line">Mastercard           | `ECA` | 5100001000000048 | 123  | 3D v2 - challenge declined         |
| <img src="../.gitbook/assets/mastercard.svg" alt="" data-size="line">Mastercard           | `ECA` | 5100001000000014 | 123  | 3D v2 - frictionless authenticated |
| <img src="../.gitbook/assets/mastercard.svg" alt="" data-size="line">Mastercard           | `ECA` | 5100001000000030 | 123  | 3D v2 - frictionless declined      |
| <img src="../.gitbook/assets/visa.svg" alt="" data-size="line">Visa                       | `VIS` | 4000001000000034 | 123  | 3D v2 - frictionless declined      |
| <img src="../.gitbook/assets/visa.svg" alt="" data-size="line">Visa                       | `VIS` | 4000001000000018 | 123  | 3D v2 - frictionless authenticated |
| <img src="../.gitbook/assets/visa.svg" alt="" data-size="line">Visa                       | `VIS` | 4000001000000042 | 123  | 3D v2 - challenge declined         |
| <img src="../.gitbook/assets/visa.svg" alt="" data-size="line">Visa                       | `VIS` | 4000001000000026 | 123  | 3D v2 - challenge authenticated    |
| <img src="../.gitbook/assets/card_amex-old.svg" alt="" data-size="line"> American Express | `AMX` | 340000100000024  | 1234 | 3D v2 - challenge authenticated    |
| <img src="../.gitbook/assets/card_amex-old.svg" alt="" data-size="line"> American Express | `AMX` | 340000100000040  | 1234 | 3D v2 - challenge declined         |
| <img src="../.gitbook/assets/card_amex-old.svg" alt="" data-size="line"> American Express | `AMX` | 340000100000016  | 1234 | 3D v2 - frictionless authenticated |
| <img src="../.gitbook/assets/card_amex-old.svg" alt="" data-size="line"> American Express | `AMX` | 340000100000032  | 1234 | 3D v2 - frictionless declined      |
| <img src="../.gitbook/assets/diners.svg" alt="" data-size="line">Diners Club              | `DIN` | 30569309025904   | 123  | 3D v2 - challenge authenticated    |
| <img src="../.gitbook/assets/discover.svg" alt="" data-size="line">Discover               | `DIS` | 6011000000000004 | 123  | 3D v2 - challenge authenticated    |

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
