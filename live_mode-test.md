# Developer Test Account

[Sign up](http://www.pci-proxy.com/) for a developer test account to start testing in our test environment.

You will receive the following demo credentials:

 | Credential | Description |
| -- | -- |
| MerchantID | Identifies your environment at PCI Proxy. |
 | X-CC-SIGN | It's a security parameter. You will need to sign your webservice calls when you collect or forward payment data. |
  | Login | Username & Password to login to our [web admin tool](https://pilot.datatrans.biz/). In our [web admin tool](https://pilot.datatrans.biz/) you can set and change the security signs.  |

### Web Administration Tool

Our web admin tool gives you a comprehensive management tool (backoffice) for initiating charges and credits, analysing of transactions, creation of reports and management of configuration data. 

| **Web Adminstration Tool:** | 
| -- |
| https://pilot.datatrans.biz/|

For more Information, please visit [Datatrans Backoffice](https://www.datatrans.ch/en/offer/backoffice).

### Security signs

For every call you make against our PCI Proxy, we ask for your security sign, a digital signature that tells us that it is really you. We differentiate between the following 2:

**Static Sign (X-CC-SIGN):**
You send it as X-CC-SIGN in the http header with every webservice call (collect or forward). When you sign up for the developer test account, we set the  *X-CC-SIGN* for you. You can change it any time in our [backend](http://pilot.datatrans.biz) under *“UPP Administration” / “Security”*.

**Dynamic Sign (SHA Hash): **
If you use our [show feature](show.html) to display single payment data, you need to dynamically sign your call with salted SHA hash. It is built as follows:

`SHA.256(salt+merchantId+aliasCC)`

Generate the *salt* value in our [backend](http://pilot.datatrans.biz) under *“UPP Administration” / “Security” / “Other Services”*.


##Live and Testing

PCI Proxy accounts are divided into two environments, namely test and production. 

All your API requests and testing go through our test environment until you activate your account. 

In test mode, you can only use [test credit cards](https://www.datatrans.ch/showcase/test-cc-numbers). 

You can differentiate test and production environment based on the URL.

 
 | Environment |URL |
| -- | -- |
| PROD: | `https://production.datatrans.biz/upp/proxy/` |
 | TEST: | `https://pilot.datatrans.biz/upp/proxy/` |


 
## Activate your account

Once your tests are successful, please activate your account to receive your productive credentials. Send the following data to [setup@pci-proxy.com](mailto:setup@pci-proxy.com):

|Information| Description   |
|---|---|
|Merchant ID|Once you  you receive your merchant ID.|

You will receive your productive merchant ID and depending on your set up productive push URLs. you can pass on to your partner. 
