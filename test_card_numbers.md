# Test Card Numbers

| Card type | Card number | Expiration Date | CVV | Country | Test rule | Support 3D |
| -- | -- | -- | -- | -- | -- | -- |
| Visa | 4242424242424242 | 12/2018 or 06/2018 | 123 | CHE | With limit | No |
| Visa | 4900000000000086 | 12/2018 or 06/2018 | 123 | USA | Without limit | Yes |
| Visa | 4900000000000003 | 12/2018 or 06/2018 | 123 | USA | Without limit | Yes |
| MasterCard | 5404000000000001 | 12/2018 or 06/2018 | 123 | RUS | With limit | Yes |
| MasterCard | 5200000000000007 | 12/2018 or 06/2018 | 123 | MYS | Without limit | No |
| MasterCard | 5200000000000080 | 12/2018 or 06/2018 | 123 | MYS | Without limit | Yes |
| Amex | 375811111111115 | 12/2018 or 06/2018 | 1234 | - | With limit | No |
| Amex | 375000000000007 | 12/2018 or 06/2018 | 1234 | - | Without limit | Yes |
| Amex | 375811111111123 | 12/2018 or 06/2018 | 1234 | - | Without limit | No |
| Diners | 36168002586009 | 12/2018 or 06/2018 | 123 | - | With limit | - |
| Diners | 36167719110012 | 12/2018 or 06/2018 | 123 | - | Without limit | - |
| JCB | 3569990010030442 | 12/2018 or 06/2018 | 123 | - | With limit | - |
| JCB | 3569990010030400 | 12/2018 or 06/2018 | 123 | - | Without limit | - |


## Test Rules

| Amount / amount range | Error message |
| -- | -- |
| <= 90.-- | Transaction authorized |
| > 90.-- and <= 100.-- | Transaction declined (i.e. insufficient limit, bad expiry date) |
| > 110.-- | Card blocked (lost or stolen) |



	
	
	
	
