---
description: Everything about testing Network Tokenisation
---

# Testing

### To get started with testing

* [ ] Activate your account for Network Tokens
* [ ] Request test credentials from our team
* [ ] Make sure the receiver integration is able to consume Network Tokens
* [ ] Complete the [test cases](testing.md#test-cases)

### Test credentials

To ensure that test card credentials can be used across the entire payment eco system, we use test cards issued by the schemes directly. However, those test cards are currently limited in usage and are being blocked for a certain period when the limit is reached. &#x20;

Please reach out to our team to get access to our Network Token test card set.&#x20;

### Test cases

Try to complete the test cases below and review together with our integration engineers if everything is working properly.&#x20;

1. Capture card details with the SecureFields integration and check if a Network Token has been created
2. Check if the expiry date has changed by calling the Status API
3. Setup your receiver integration to be able to consume Network Tokens in our dashboard
4. Authorize a transaction by forwarding a request which uses Network Tokens
