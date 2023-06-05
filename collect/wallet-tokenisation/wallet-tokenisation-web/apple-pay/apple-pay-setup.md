---
description: Requirements to setup Apple Pay direct integration
---

# Apple Pay setup

Follow the instructions on this page to learn how to setup Apple Pay on your merchantID.&#x20;

1. [**Sign up for an Apple developer account**](https://developer.apple.com/programs/enroll/)\
   \
   Please make sure to use an email address which is linked to a generic group inbox when creating an Apple account so you get notified in case of a certificate expiration. The assigned account role should be either **Account Holder** or **Admin** role. \

2. [**Create a merchant identifier**](https://developer.apple.com/help/account/configure-app-capabilities/configure-apple-pay#create-a-merchant-identifier) \
   \
   A merchant identifier uniquely identifies you as a merchant to accept and process Apple Pay. \
   We recommend to setup Apple Pay merchantIDs, domains and certificates for each, test and productive environment with unique and clearly identifiable names to avoid mismatches between the environments. \

3. [**Create a payment processing certificate**](https://developer.apple.com/help/account/configure-app-capabilities/configure-apple-pay#create-a-payment-processing-certificate)\
   \
   A _payment processing certificate_ is associated with your merchant identifier and used to encrypt payment information. The payment processing certificate expires **every 25 months**.&#x20;
   1. Instead of creating a `.csr` file with the KeyChain Access tool as described in the Apple tutorial, you should navigate to the `Apple Pay Settings` tab located in the `Developers` menu of your project section in the [PCI Proxy dashboard ](https://dashboard.pci-proxy.com/login)to download the file there.&#x20;
   2. Click the button `Download CSR file`
   3. Login to your Apple developer account and create a `Certificate` (Apple Pay Payment Processing Certificate). Select the Merchant identifier created in step 1, upload the CSR file provided by us and finally click _Download_ to get your `.cer` file.
   4. Go back to `Apple Pay Settings` screen in the PCI Proxy dashboard and upload your `Apple Payment Processing Certificate`\

4. [**Register and verify domain**](https://developer.apple.com/help/account/configure-app-capabilities/configure-apple-pay-on-the-web#register-a-merchant-domain)\
   \
   Register all domains and subdomains where you plan to call the Apple Pay API from. \

5. [**Create a merchant identity certificate**](https://developer.apple.com/help/account/configure-app-capabilities/configure-apple-pay-on-the-web#create-a-merchant-identity-certificate)\
   \
   Use the merchant identity certificate to authenticate your communication with the Apple Pay servers.&#x20;
   1. Instead of creating a `.csr` file with the KeyChain Access tool as described in the Apple tutorial we recommend to use openssl. Issue the following command to create a certificate signing request for the Apple Pay Merchant Identity:\
      `openssl req -sha256 -nodes -newkey rsa:2048 -keyout applepaytls.key -out applepaytls.csr`
   2. Login to your Apple Developer account, in [Certificates, Identifiers & Profiles](https://developer.apple.com/account/resources), click Identifiers in the sidebar, then select Merchant IDs from the pop-up menu on the top right and select the merchant identified created in step 1.&#x20;
   3. Navigate to the _**Apple Pay Merchant Identity Certificate**_ section and select _Create Certificate_
   4. Upload the `applepaytls.csr` file you just created in your terminal, select _Continue_ and then _Download_ to get your `.cer` file
   5. Convert the `.cer` certificate to a `.pem` certificate using the following command: \
      `openssl x509 -inform der -in certFromApple.cer -out applepaytls.pem`

**Next steps**

When you have successfully completed the Apple Pay setup continue with step 2 [here](./#2.-convert-apple-pay-token-into-a-pci-proxy-alias) to finish the Apple Pay integration.&#x20;
