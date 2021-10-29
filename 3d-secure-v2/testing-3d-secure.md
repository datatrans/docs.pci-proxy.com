# Testing 3D Secure

Use the following Datatrans test card data to test through 3D Secure v1 and v2 transactions:

| **Type**   | **Number**       | **CVV** | **Scenario**                       |
| ---------- | ---------------- | ------- | ---------------------------------- |
| Mastercard | 5200000000000080 | 123     | 3D v1 - challenge authenticated    |
| Mastercard | 5100001000000022 | 123     | 3D v2 - challenge authenticated    |
| Mastercard | 5100001000000048 | 123     | 3D v2 - challenge declined         |
| Mastercard | 5100001000000014 | 123     | 3D v2 - frictionless authenticated |
| Mastercard | 5100001000000030 | 123     | 3D v2 - frictionless declined      |
| Visa       | 4900000000000086 | 123     | 3D v1 - challenge authenticated    |
| Visa       | 4000001000000034 | 123     | 3D v2 - frictionless declined      |
| Visa       | 4000001000000018 | 123     | 3D v2 - frictionless authenticated |
| Visa       | 4000001000000042 | 123     | 3D v2 - challenge declined         |
| Visa       | 4000001000000026 | 123     | 3D v2 - challenge authenticated    |
| AMEX       | 375000000000007  | 1234    | 3D v1 - challenge authenticated    |
| AMEX       | 340000100000024  | 1234    | 3D v2 - challenge authenticated    |
| AMEX       | 340000100000040  | 1234    | 3D v2 - challenge declined         |
| AMEX       | 340000100000016  | 1234    | 3D v2 - frictionless authenticated |
| AMEX       | 340000100000032  | 1234    | 3D v2 - frictionless declined      |
| DIN        | 30569309025904   | 123     | 3D v2 - challenge authenticated    |
| DIS        | 6011000000000004 | 123     | 3D v2 - challenge authenticated    |

#### Expiration date

Month: 12 (December)\
Year: 21 (2021)\
Short: 12/21

#### Password for challenge flow

Use following OTP password codes to determine the result of a 3D v2 enrolled card.

4444 = authenticated\
4009 = declined
