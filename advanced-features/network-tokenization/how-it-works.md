---
description: Learn how to use the PCI Proxy Network Token solution
---

# How it works

PCI Proxy's approach is an inbuilt Network Tokenization solution which works out of the box for all merchants when activated. It allows you to keep existing PCI Proxy integrations and saves you months of implementation work.&#x20;

Follow this step-by-step guide to understand how to setup your account for the PCI Proxy Network Tokenization solution, create Network Tokens and how to forward them to receivers of your choice.&#x20;

1. [Get an overview about the end-to-end process flow](how-it-works.md#high-level-process-flow-diagram)
2. [Onboard and activate your account ](onboarding-and-activation.md)
3. [Create Network Tokens - Token provisioning ](network-token-provisioning.md)
4. [Forward Network Tokens to 3rd parties (Receivers) ](../../use/forward-proxy/)
5. [Explore the Account Lifecycle management to keep your cards up to date](account-lifecycle-management.md)
6. [How to test Network Tokenization](testing.md)
7. [Abbreviations and Questions](faq-and-terminology.md)

### Good to know

Please carefully read the information below before you start working with Network Tokens.&#x20;

* As of November 2022, Datatrans/PCI Proxy is a certified token requestor for VISA VTS and Mastercard MDES
  * AMEX AETS will follow by end of Q2/2023
  * Other card brands are being reviewed and steadily integrated
* Network Tokenization **only** works with the [Alias 2.0](../../resources/token-formats.md#alias-2.0) and [Alias 2.0 length preserving](../../resources/token-formats.md#alias-2.0-length-preserving) format
  * Please note that we can't grant any exemption here due to security reasons
* Please make sure that your Receiver can process Network Tokens created by a third party
* Although Network Tokenization is a global mandate by the card schemes, the adaption rate is depending on region, country and issuer
* We are actively working on enhancing the Network Tokenization solution to offer you even more value out of it

### High level process flow diagram

The graph below shows a high level end-to-end process flow from creating Network Tokens to forwarding them to Receivers through PCI Proxy.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-26 at 16.52.54.png" alt=""><figcaption></figcaption></figure>

1. Capture card details with one of our Network Tokenization supported integration methods
2. PCI Proxy is requesting a Network Token at the respective scheme&#x20;
3. If a Network Token is returned by the schemes we are mapping it to the PCI Proxy token
4. PCI Proxy token is returned to your servers
5. Call the Alias status API to check if a Network Token has been created or check if an expiry date has changed
6. Forward the PCI Proxy token to the Forward API and specify the payload according what the receiver is expecting
7. Depending on the submitted payload, PCI Proxy decides whether to convert the PCI Proxy token to a PAN or a Network Token. In case of a Network Token PCI Proxy requests a new cryptogram at the schemes and populates the request with it.&#x20;
8. Request is forwarded to the receiver for further processing

