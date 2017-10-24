# Step 4: Go live

## 1. Get your Production Account

Follow these steps to get your Production Account:

1. [**Contact**](/mailto: setup@pci-proxy.com) your sales representative to sign a subscription plan.

2. Once signed, _we setup your Production Account with all Channels and Receiver_ according to your Sandbox Account.

3. You will receive your Production credentials in 2 separate Emails: Login \(merchant ID\), Username, Password.  
   _If you haven't received anything, please check your spam folder or contact support@datatrans.com._

4. [**Log in**](https://pilot.datatrans.biz/) with your credentials and follow instructions to create your own password.

5. Setup your Production Account with Security Sign and Salt Value according to [**Step 1**](/step-1-signup-and-setup.md).

> If you are in possession of an existing stock of sensitive cardholder data you would like to tokenize initially in terms of going-live, please refer to our [XML-Alias Gateway](https://docs.pci-proxy.com/xml_alias_gateway.html) or contact us directly.

    6. Change the following details for production usage:

### Production Data vs. Sandbox Data

Our production environment and sandbox environment always behave the same. Once all tests on your Sandbox Account are successful, you can be rest assured that everything works the same in production. However, we differentiate between Production and Sandbox data to keep the environment separated. You will receive an email with the following Production data:

| Data | Sandbox Account |
| :--- | :--- |
| Login / Merchant ID | 1100001111 |
| Username & Password | Sandbox Login |
| Sign | Sandbox Sign |
| Salt | Sandbox Salt |
| Web Admin Tool | [https://admin.sandbox.datatrans.com/](https://admin.sandbox.datatrans.com/) |
| PULL API Endpoint | [https://sandbox.pci-proxy.com/v1/pull/](https://sandbox.pci-proxy.com/v1/pull/) |
| PUSH API Endpoint | [https://sandbox.pci-proxy.com/v1/push/](https://sandbox.pci-proxy.com/v1/push/) |
| XML Gateway Endpoint | [https://api.sandbox.datatrans.com/upp/jsp/XML\_authorize.jsp](https://api.sandbox.datatrans.com/upp/jsp/XML_authorize.jsp) |
| Payment Page Endpoint | [https://pay.sandbox.datatrans.com/upp/jsp/upStart.jsp](https://pay.sandbox.datatrans.com/upp/jsp/upStart.jsp) |
| Tokenizer Endpoint | [https://pay.sandbox.datatrans.com/upp/payment/tokenize](https://pay.sandbox.datatrans.com/upp/payment/tokenize) |
| No-Show API | [https://pay.sandbox.datatrans.com/upp/jsp/noShow.jsp](https://pay.sandbox.datatrans.com/upp/jsp/noShow.jsp) |
| Pay-by-Email Endpoint | [https://api.sandbox.datatrans.com/upp/jsp/XML\_PayByEmail](https://api.sandbox.datatrans.com/upp/jsp/XML_PayByEmail) |

---

> #### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



