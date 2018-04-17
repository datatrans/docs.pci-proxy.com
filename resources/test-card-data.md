---
description: Use our test cards on sandbox.
---

# Test card data

We have a set of test credit card numbers that you can use in our sandbox environment to test your integration. Limit and 3D support is only needed for transactions and not for tokenization.

{% hint style="warning" %}
Full credit card information cannot be used in the sandbox.
{% endhint %}

| Brand | Code | PAN | Token | Expiry | CVV | Limit | 3D |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| ![](../.gitbook/assets/logo_visa%20%281%29.png) | VIS | 4242424242424242 | 424242SKMPRI4242 | 12/2018 | 123 | yes | No |
| ![](../.gitbook/assets/logo_visa%20%282%29.png) | VIS | 4900000000000086 | 490000VUFMRQ0086 | 12/2018 | 123 | No | Yes |
| ![](../.gitbook/assets/logo_visa.png) | VIS | 4900000000000003 | 490000PVCGFB0003 | 12/2018 | 123 | No | Yes |
| ![](../.gitbook/assets/logo_mastercard.png) | ECA | 5404000000000001 | 540400FEQOYX0001 | 12/2018 | 123 | Yes | Yes |
| ![](../.gitbook/assets/logo_mastercard%20%281%29.png) | ECA | 5200000000000007 | 520000ZOGGIP0007 | 12/2018 | 123 | No | No |
| ![](../.gitbook/assets/logo_mastercard%20%282%29.png) | ECA | 5200000000000080 | 520000RIVWAS0080 | 12/2018 | 123 | No | Yes |
| ![](../.gitbook/assets/logo_amex.png) | AMX | 375811111111115 | 375811OMTYEE115 | 12/2018 | 1234 | Yes | No |
| ![](../.gitbook/assets/logo_amex%20%281%29.png) | AMX | 375000000000007 | 375000ARZULD007 | 12/2018 | 1234 | No | Yes |
| ![](../.gitbook/assets/logo_amex%20%282%29.png) | AMX | 375811111111123 | 375811MGVGZR123 | 12/2018 | 1234 | No | No |
| ![](../.gitbook/assets/logo_diners.png) | DIN | 36168002586009 | 361680IYUAUR09 | 12/2018 | 123 | Yes | - |
| ![](../.gitbook/assets/logo_diners%20%281%29.png) | DIN | 36167719110012 | 361677GQVJHV12 | 12/2018 | 123 | No | - |
| ![](../.gitbook/assets/logo_discover.png) | DIS | 6011000000000004 | 601100EQYBBH0004 | 06/2018 | 123 | - | - |
| ![](../.gitbook/assets/logo_jcb%20%281%29.png) | JCB | 3569990010030442 | 356999BIUWJW0442 | 12/2018 | 123 | Yes | - |
| ![](../.gitbook/assets/logo_jcb.png) | JCB | 3569990010030400 | 356999PUCUIV0400 | 12/2018 | 123 | No | No |
| ![](../.gitbook/assets/logo_elo%20%281%29.png) | ELO | 6550000000000001 | 655000BFQHZD0001 | 12/2018 | 123 | - | - |
| ![](../.gitbook/assets/logo_elo.png) | ELO | 6362970000457013 | 636297KMDXHG7013 | 12/2018 | 123 | - | - |
| ![](../.gitbook/assets/logo_cup%20%281%29.png) | CUP | 6222821234560017 | 622282XGRFXB0017 | 12/2018 | - | No | Yes |
| ![](../.gitbook/assets/logo_cup.png) | CUP | 6223164991230014 | 622316XWWQYN0014 | 12/2018 | - | No | No |

| [**Create CVV Token** ](https://pilot.datatrans.biz/upp/jsp/upStart.jsp?uppAliasOnly=yes&merchantId=1000011011&amount=1000&currency=CHF&refno=800381&sign=30916165706580013&paymentmethod=VIS&aliasCC=70119122433810042&expm=12&expy=18&cvv=123)for CVV code 123 |
| --- | --- |
| CVV tokens \(`aliasCVV`\) will be deleted after they have been initially used. Once you have used a CVV token for [Forward](../use-stored-cards/forward/), [Show](../use-stored-cards/show.md), or [Authorize](../use-stored-cards/authorize.md), the CVV token expires 30 minutes thereafter. The link above generates fresh CVV tokens for your testing purposes.  |

| \*Limit \(Amount / amount range\) | Error message |
| --- | --- | --- | --- |
| &lt;= 90.-- | Transaction authorized |
| &gt; 90.-- and &lt;= 100.-- | Transaction declined \(i.e. insufficient limit, bad expiry date\) |
| &gt; 110.-- | Card blocked \(lost or stolen\) |



