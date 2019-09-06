# Testing 3D secure

Use the following Datatrans test card data to test through 3D Secure 1 and 2 transactions:

| Type | Number | Token | CVV | Scenario |
| :--- | :--- | :--- | :--- | :--- |
| Mastercard | 5200000000000080 | 520000RIVWAS0080 | 123 | 3D v1 - challenge authenticated |
| Mastercard | 5100001000000022 | 510000DCYPBJ0022 | 123 | 3D v2 - challenge authenticated |
| Mastercard | 5100001000000048 | 510000ZEUNRB0048 | 123 | 3D v2 - challenge declined |
| Mastercard | 5100001000000014 | 510000HNQKIU0014 | 123 | 3D v2 - frictionless authenticated |
| Mastercard | 5100001000000030 | 510000LHDINR0030 | 123 | 3D v2 - frictionless declined  |
| Visa | 4900000000000086 | 490000VUFMRQ0086 | 123 | 3D v1 - challenge authenticated |
| Visa | 4000001000000034 | 400000CLCTBA0034 | 123 | 3D v2 - frictionless declined  |
| Visa | 4000001000000018 | 400000JCLJDP0018 | 123 | 3D v2 - frictionless authenticated |
| Visa | 4000001000000042 | 400000JMMJHM0042 | 123 | 3D v2 - challenge declined |
| Visa | 4000001000000026 | 400000RQFEJQ0026 | 123 | 3D v2 - challenge authenticated |
| AMEX | 375000000000007 | 375000XQJTGJ007 | 1234 | 3D v1 - challenge authenticated |

#### Expiration date

Month: 12 \(December\)  
Year: 21 \(2021\)  
Short: 12/21

#### Password for challenge flow

For text challenges in a browser-based integration use **1234**



