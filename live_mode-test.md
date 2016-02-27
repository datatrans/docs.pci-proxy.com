# Developer Test Account

[Sign up](http://www.pci-proxy.com/) for a developer test account to start testing in our test environment.

You will receive the following demo credentials:

 | Credential | Description |
| -- | -- |
| MerchantID | Identifies your environment at PCI Proxy. |
 | X-CC-SIGN | It's a security parameter. You will need to sign your webservice calls when you collect or forward payment data. |
  | Login | Username & Password to login to our [backend](https://pilot.datatrans.biz/). In our [backend](https://pilot.datatrans.biz/) you can set and change the security signs.  |

### Web Administration Tool

| **Web Adminstration Tool:** | 
| -- |
| https://pilot.datatrans.biz/|

### Security signs

Every PCI Proxy account comes with security signs. When you sign up for the developer test account, we set the  *X-CC-SIGN* for you. It is a static security sign that you need to send as http header with every XML/SOAP call.

If you use our [show feature]() to display single payment data, you need a salted SHA.256 security sign.

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
