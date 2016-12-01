# Developer Test Account

[Sign up](https://www.pci-proxy.com/#/signup) for a developer test account to start testing in our test environment.

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

---


##Live and Testing

PCI Proxy accounts are divided into two environments, namely test and production. 

All your API requests and testing go through our test environment until you activate your account. 

In test mode, you can only use [test credit cards](https://www.datatrans.ch/showcase/test-cc-numbers). 

You can differentiate test and production environment based on the URL.

 
 | Environment |URL |
| -- | -- |
| PROD: | `https://payment.datatrans.biz/upp/proxy/` |
 | TEST: | `https://pilot.datatrans.biz/upp/proxy/` |
 
 ---

 
## Activate your account

Once your tests are successful, please activate your account to receive your productive credentials. Send the following data to [setup@pci-proxy.com](mailto:setup@pci-proxy.com):

|Information| Description   |
|---|---|
|Merchant ID|Once you receive your merchant ID.|

You will receive your productive merchant ID and productive push URLs depending on your setup. You can pass the push URLs on to your partner. 
