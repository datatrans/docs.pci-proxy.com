# Test Credit Card Number

## Test Card Numbers

We have a set of test credit card numbers that you can use in our test environment to test your integration. Test rules and 3D support is only needed for transactions and not for tokenization.

| Card type | Card number | Expiration Date | CVV  | Test rule | Support 3D |
| -- | -- | -- | -- | -- | -- | -- |
| Visa | 4242424242424242 | 12/2018 or 06/2018 | 123  | w/limit | No |
| Visa | 4900000000000086 | 12/2018 or 06/2018 | 123  | wo/limit | Yes |
| Visa | 4900000000000003 | 12/2018 or 06/2018 | 123  | w/limit | Yes |
| MasterCard | 5404000000000001 | 12/2018 or 06/2018 | 123 | w/limit | Yes |
| MasterCard | 5200000000000007 | 12/2018 or 06/2018 | 123 | w/limit | No |
| MasterCard | 5200000000000080 | 12/2018 or 06/2018 | 123 | wo/limit | Yes |
| Amex | 375811111111115 | 12/2018 or 06/2018 | 1234 | w/limit | No |
| Amex | 375000000000007 | 12/2018 or 06/2018 | 1234 | wo/limit | Yes |
| Amex | 375811111111123 | 12/2018 or 06/2018 | 1234 | wo/limit | No |
| Diners | 36168002586009 | 12/2018 or 06/2018 | 123 | w/limit | - |
| Diners | 36167719110012 | 12/2018 or 06/2018 | 123 | wo/limit | - |
| JCB | 3569990010030442 | 12/2018 or 06/2018 | 123 | w/limit | - |
| JCB | 3569990010030400 | 12/2018 or 06/2018 | 123 | wo/limit | - |


### Test Rules

| Amount / amount range | Error message |
| -- | -- |
| <= 90.-- | Transaction authorized |
| > 90.-- and <= 100.-- | Transaction declined (i.e. insufficient limit, bad expiry date) |
| > 110.-- | Card blocked (lost or stolen) |