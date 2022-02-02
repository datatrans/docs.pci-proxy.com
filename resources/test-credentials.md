# Test credentials

## Test Credit and Debit Cards

We have a set of test card numbers that you can use in our sandbox environment to test your integration:&#x20;

{% hint style="warning" %}
Productive card information cannot be used in the sandbox.
{% endhint %}

| Brand                                                       | Code  | Number           | CVV  |
| ----------------------------------------------------------- | ----- | ---------------- | ---- |
| ![](../.gitbook/assets/visa.svg)Visa                        | `VIS` | 4242424242424242 | 123  |
| ![](../.gitbook/assets/visa.svg)Visa                        | `VIS` | 4900000000000086 | 123  |
| ![](../.gitbook/assets/visa.svg)Visa                        | `VIS` | 4900000000000003 | 123  |
| ![](../.gitbook/assets/visa.svg)Visa Debit                  | `VIS` | 4444090101010103 | 123  |
| ![](../.gitbook/assets/mastercard.svg)Mastercard            | `ECA` | 5404000000000001 | 123  |
| ![](../.gitbook/assets/mastercard.svg)Mastercard            | `ECA` | 5200000000000007 | 123  |
| ![](../.gitbook/assets/mastercard.svg)Mastercard            | `ECA` | 5200000000000080 | 123  |
| ![](../.gitbook/assets/mastercard.svg)Mastercard Debit      | `ECA` | 5500000000000000 | 123  |
| ![](../.gitbook/assets/card\_amex-old.svg) American Express | `AMX` | 375811111111115  | 1234 |
| ![](../.gitbook/assets/card\_amex-old.svg) American Express | `AMX` | 375000000000007  | 1234 |
| ![](../.gitbook/assets/card\_amex-old.svg) American Express | `AMX` | 375811111111123  | 123  |
| ![](../.gitbook/assets/diners.svg)Diners Club               | `DIN` | 36168002586009   | 123  |
| ![](../.gitbook/assets/diners.svg)Diners Club               | `DIN` | 36167719110012   | 123  |
| ![](../.gitbook/assets/discover.svg)Discover                | `DIS` | 6011000000000004 | 123  |
| ![](../.gitbook/assets/logo\_jcb.png)JCB                    | `JCB` | 3569990010030442 | 123  |
| ![](../.gitbook/assets/logo\_jcb.png)JCB                    | `JCB` | 3569990010030400 | 123  |
| ![](../.gitbook/assets/Elo-logo.png) ELO                    | `ELO` | 6550000000000001 | 123  |
| ![](../.gitbook/assets/Elo-logo.png) ELO                    | `ELO` | 6362970000457013 | 123  |
| ![](../.gitbook/assets/china-union-pay.svg) UnionPay        | `CUP` | 6222821234560017 | -    |
| ![](../.gitbook/assets/china-union-pay.svg) UnionPay        | `CUP` | 6223164991230014 | -    |
| ![](../.gitbook/assets/maestro.svg) Maestro                 | `MMS` | 6759000000000018 | 123  |
| ![](../.gitbook/assets/maestro.svg) Maestro                 | `MMS` | 6759000000000026 | 123  |
| ![](../.gitbook/assets/Dankort.png) Dankort                 | `DNK` | 5019994000124034 | 747  |
| ![](../.gitbook/assets/uatp.svg) UATP                       | `UAP` | 192072420096379  | -    |

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
