# Test card data

We have a set of test credit card numbers that you can use in our sandbox environment to test your integration. Limit and 3D support is only needed for transactions and not for tokenization.

{% hint style="warning" %}
Productive credit card information cannot be used in the sandbox.
{% endhint %}

| Brand | Code | PAN | Token \(generic "unique" token\) | Expiry | CVV | Limit | 3D |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| ![](.gitbook/assets/logo_visa%20%281%29.png) | VIS | 4242424242424242 | AAABcH0Bq92s3kgAESIAAbGj5NIsAHWC | 12/2021 | 123 | yes | No |
| ![](.gitbook/assets/logo_visa%20%282%29.png) | VIS | 4900000000000086 | AAABcH0BrE-s3kgAESIAAWdCRyMPAGvp | 12/2021 | 123 | No | Yes |
| ![](.gitbook/assets/logo_visa.png) | VIS | 4900000000000003 | AAABcH0BrFms3kgAESIAAfHfAmyjACIJ | 12/2021 | 123 | No | Yes |
| ![](.gitbook/assets/logo_mastercard.png) | ECA | 5404000000000001 | AAABcH0BrGOs3kgAESIAAc6gFVXTAGTv | 12/2021 | 123 | Yes | Yes |
| ![](.gitbook/assets/logo_mastercard%20%281%29.png) | ECA | 5200000000000007 | AAABcH0BrG2s3kgAESIAAbmn7rNZAC1l | 12/2021 | 123 | No | No |
| ![](.gitbook/assets/logo_mastercard%20%282%29.png) | ECA | 5200000000000080 | AAABcH0BrHes3kgAESIAAYJ5A6WzAFsz | 12/2021 | 123 | No | Yes |
| ![](.gitbook/assets/logo_amex.png) | AMX | 375811111111115 | AAABcH0BrICs3kgAESIAAQ33vcLxADJm | 12/2021 | 1234 | Yes | No |
| ![](.gitbook/assets/logo_amex%20%281%29.png) | AMX | 375000000000007 | AAABcH0BrIms3kgAESIAAVp8kILAAAka | 12/2021 | 1234 | No | Yes |
| ![](.gitbook/assets/logo_amex%20%282%29.png) | AMX | 375811111111123 | AAABcH0BrJ6s3kgAESIAAR0FRZnvADsW | 12/2021 | 1234 | No | No |
| ![](.gitbook/assets/logo_diners.png) | DIN | 36168002586009 | AAABcH0BrKis3kgAESIAARz0vKeyAJP1 | 12/2021 | 123 | Yes | - |
| ![](.gitbook/assets/logo_diners%20%281%29.png) | DIN | 36167719110012 | AAABcH0BrLKs3kgAESIAAeXMwAnVALLl | 12/2021 | 123 | No | - |
| ![](.gitbook/assets/logo_discover.png) | DIS | 6011000000000004 | AAABcH0BrLys3kgAESIAASKNHo0kAGkv | 06/2021 | 123 | - | - |
| ![](.gitbook/assets/logo_jcb%20%281%29.png) | JCB | 3569990010030442 | AAABcH0BrMas3kgAESIAAQ4E6D72AL1p | 12/2021 | 123 | Yes | - |
| ![](.gitbook/assets/logo_jcb.png) | JCB | 3569990010030400 | AAABcH0BrM6s3kgAESIAATeCFGr8AHNk | 12/2021 | 123 | No | No |
| ![](.gitbook/assets/logo_elo%20%281%29.png) | ELO | 6550000000000001 | AAABcH0BrNes3kgAESIAAZlN82oMAH2p | 12/2018 | 123 | - | - |
| ![](.gitbook/assets/logo_elo.png) | ELO | 6362970000457013 | AAABcH0BrOKs3kgAESIAAVLzQBQNADfQ | 12/2018 | 123 | - | - |
| ![](.gitbook/assets/logo_cup%20%281%29.png) | CUP | 6222821234560017 | AAABcH0BrOys3kgAESIAAbnkTiwZAKFg | 12/2021 | - | No | Yes |
| ![](.gitbook/assets/logo_cup.png) | CUP | 6223164991230014 | AAABcH0BrPWs3kgAESIAASDQEWOHACL7 | 12/2021 | - | No | No |

| [**Create CVV Token** ](https://sandbox.pci-proxy.com/v1/push/push-tester?cvv=123)for CVV code 123 |
| :--- |
| CVV tokens \(`aliasCVV`\) will be deleted after they have been initially used. Once you have used a CVV token for [Forward](use-stored-cards/forward/), [Show](use-stored-cards/show.md), or [Authorize](use-stored-cards/authorize-settle/), the CVV token expires 30 minutes thereafter. The link above generates fresh CVV tokens for your testing purposes.  |

| \*Limit \(Amount / amount range\) | Error message |
| :--- | :--- |
| &lt;= 90.-- | Transaction authorized |
| &gt; 90.-- and &lt;= 100.-- | Transaction declined \(i.e. insufficient limit, bad expiry date\) |
| &gt; 110.-- | Card blocked \(lost or stolen\) |



