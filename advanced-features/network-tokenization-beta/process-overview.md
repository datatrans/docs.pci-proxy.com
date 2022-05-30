---
description: Learn how to use the PCI Proxy Network Token solution
---

# Process overview

### Process flow diagram

![High level process flow diagram](<../../.gitbook/assets/NT process flow diagram.png>)

### Onboarding

To use Network Tokens each organisation needs to be registered at the respective Scheme (VTS for VISA, MDES for Mastercard and AETS for American Express) to receive a so called TRID (Token Requestor ID - a unique merchant identifier). \
As PCI Proxy is a certified Token Service Requester we take care of the registration together with your team. Once a TRID has been provided we will store the TRID and act on-behalf of you to issue Network Tokens. \
\
Please note that requesting a new TRID might need some time. We currently expect to create a new TRID within a timeframe between two weeks and up to one month.&#x20;

### Token Provisioning

Token provisioning is the process of requesting that the affected Network issues a token for a specific PAN and for a specific purpose, domain, or device.&#x20;

When the Scheme Token service is activated on your your account - we automatically create a new Scheme Token each time a credit card gets tokenised. As of today the following integration methods support Scheme Tokens provisioning:&#x20;

* [SecureFields](../../collect/secure-fields-js/)
* [Mobile SDKs](../../collect/mobile-sdks.md)
* [3D SecureFields](../../authenticate/3d-secure-fields-js/)

As soon as a credit card hits one of those APIs we create a Scheme Token and the corresponding Cryptogram in the background and map it to our Alias 2.0 format which is returned to your servers.

When authorising with a Scheme Token, usually the corresponding Cryptogram is required for Customer Initiated transactions.&#x20;

{% hint style="danger" %}
We do not return the Scheme Token nor the Cryptogram. They are being considered as sensitive payment information according PCI DSS and would extend your PCI scope significantly when storing or processing them in your environment.&#x20;
{% endhint %}

### Account Lifecycle Management

Use the [Alias status API](../../store/manage/status.md) to benefit from the Scheme Tokenisation Account Lifecycle Management. \
Use the Alias 2.0 and send it to the Status API to check the latest expiry date of the underlying card number.&#x20;

Furthermore, the response body will indicate if a Scheme Token has been provisioned successfully or not. Simply check if the `tokenInfo` element is available in the response. \


{% hint style="info" %}
We do not yet return the Token status, card meta data or card art information.

Please contact us if you need any of those information. Our product team is happy to elaborate the use-case with you.&#x20;
{% endhint %}

### Authorisation

When it comes to authorising a transaction against a payment provider, we leave it fully up to you whether you want to authorise with a normal FPAN or if you want us to send the Scheme Token and the Cryptogram.&#x20;

In any case, use our common [Forward API](../../use/forward-proxy/). Next to inserting our Alias 2.0, just add an additional HTTP header to your request to tell us if we should forward a Scheme Token or FPAN to your payment gateway. In case of a Scheme Token add an empty Cryptogram element to your payload. PCI Proxy has logic to create a new Cryptogram on the fly and populate it to your request towards the payment gateway.&#x20;

Creating a new Cryptogram is required as they have a limited lifespan and needed to be created at the time of the transaction.&#x20;

To sum up, we take care of the entire logic to maintain and send Scheme Tokens to 3rd parties. \
Compared to the current forwarding API we need you to just add the following minor steps:

* Add HTTP header to tell us what we should forward
* Empty Cryptogram element in your payload

### Good to know

* As of today only VTS and MDES is supported
* Network tokenisation only works with the latest [Alias 2.0](../../resources/token-formats.md#alias-2.0) format
* Please make sure that your payment gateway can process 3rd party created Network Tokens
* Although Network Tokenisation is a global mandate by the schemes, the adaption rate is depending on region and country

###





