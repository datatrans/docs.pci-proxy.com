---
description: Learn how to setup your sandbox account and activating it for production.
---

# Get started with PCI Proxy

Follow this step-by-step guide to setup your sandbox account and to setup your account production ready by yourself within minutes. \
\
Drop us a line at [support@pci-proxy.com](mailto:support@pci-proxy.com) if you need any further help or advice in terms of setting up your account. 

## 1. Create a test account

Sign up here [https://dashboard.pci-proxy.com/signup](https://dashboard.pci-proxy.com/signup) and complete the form to get a free trial account. \
\
You will be logged in with admin user rights when signing up. Create additional users and share with your team members as needed. 

{% hint style="info" %}
Learn more about [Account structure and User management](guides/pci-proxy-dashboard/account-structure-user-management.md)
{% endhint %}

## 2. Configure your test account 

1\) Configure sandbox API authentication data. Refer to [Authentication ](guides/pci-proxy-dashboard/api-authentication-data.md)for more information. \
2\) Access sandbox API endpoints. Refer to [API endpoints](guides/pci-proxy-dashboard/api-endpoints.md)[ ](guides/pci-proxy-dashboard/api-authentication-data.md)for more information. \
3\) Choose an [integration method](collect-and-store-cards/) for inbound traffic and build the request as documented for each API.\
\
1\) [Webrequests (Filter API)](collect-and-store-cards/filter-payloads/)\
2\) [Frontend (iFrames)](collect-and-store-cards/capture-iframes/)\
3\) [Native mobile Apps](collect-and-store-cards/vault-alias-gateway.md)\
4\) [SFTP](collect-and-store-cards/secure-file-transfer-sftp.md)

As a next step setup the integrations for the outbound traffic if needed.\
\
1\) [Webrequests (Forward API)](use-stored-cards/forward/)\
2\) [Show cardholder data](use-stored-cards/show.md)\
3\) [Check cardholder data](use-stored-cards/check.md)\
4\) [Authorize/Settle](use-stored-cards/authorize-settle/)\


{% hint style="info" %}
Learn more about [adding existing or new integrations to your project](guides/pci-proxy-dashboard/add-integrations.md)
{% endhint %}

## 3. Going live

Once everything has been tested properly on sandbox environment you can activate your account for production environment by yourself within minutes. 

{% hint style="info" %}
Activating your account for production starts the billing process. 
{% endhint %}

Follow below steps to activate your account for production.\
\
1\) Click the **Environment **switcher in the left hand side menu\
2\) Select your subscription plan, complete all required data and press Continue\
3\) Choose your preferred payment method and finally enable your account for production\
4\) A confirmation email with the contract overview will be sent to the admin contact

{% hint style="warning" %}
It might be possible that we will contact you and request for more information and verification data after go live. 
{% endhint %}

## 4. Configure your live account

After you successfully completed the going live process prepare your productive account by following these steps:

1\) Clone the integrations you setup on test environment. \
Switch back to test environment - navigate to Integrations menu - click on Settings of the desired Integration - press the **Clone to production button** on the bottom status bar. \
2\) Setup productive API authentication data. Refer to [Authentication ](guides/pci-proxy-dashboard/api-authentication-data.md)for more information. \
3\) Build the request and route them through productive PCI Proxy endpoints. Refer to [API endpoints](guides/pci-proxy-dashboard/api-endpoints.md)[ ](guides/pci-proxy-dashboard/api-authentication-data.md)for more information. 

## Next up

{% content-ref url="collect-and-store-cards/" %}
[collect-and-store-cards](collect-and-store-cards/)
{% endcontent-ref %}

