# Step 4: Go live

## 1. Get your Production Account

Follow these steps to get your Production Account:

1. [**Contact**](/mailto: setup@pci-proxy.com) your sales representative to sign a subscription plan.

2. Once signed, _we setup your Production Account with all Channels and Receiver_ according to your Sandbox Account.

3. You will receive your Production credentials in 2 separate Emails: Login \(merchant ID\), Username, Password.  
   _If you haven't received anything, please check your spam folder or contact support@pci-proxy.com._

4. [**Log in**](https://pilot.datatrans.biz/) with your credentials and follow instructions to create your own password.

5. Setup your Production Account with Security Sign and Salt Value according to [**Step 1**](/step-1-signup-and-setup.md).

6. Change the following details for production usage:

### Production Data vs. Sandbox Data

| Data | Sandbox Account | Production Account |
| :--- | :--- | :--- |
| Login / Merchant ID | 1100001111 | 3000001111 |
| Username & Password | Sandbox Login | Production Login |
| Sign | Sandbox Sign | Production Sign |
| Salt | Sandbox Salt | Production Salt |
| Web Admin Tool | [https://pilot.datatrans.biz/](https://pilot.datatrans.biz/) | [https://payment.datatrans.biz/](https://payment.datatrans.biz/) |
| PULL API Endpoint | [https://sandbox.pci-proxy.com/v1/pull/](https://sandbox.pci-proxy.com/v1/pull/) | [https://api.pci-proxy.com/v1/pull/](https://api.pci-proxy.com/v1/pull/) |
| PUSH API Endpoint | [https://sandbox.pci-proxy.com/v1/push/](https://sandbox.pci-proxy.com/v1/push/) | [https://api.pci-proxy.com/v1/push/](https://api.pci-proxy.com/v1/push) |
| XML Gateway Endpoint | [https://pilot.datatrans.biz/upp/jsp/XML\_authorize.jsp](https://pilot.datatrans.biz/upp/jsp/XML_authorize.jsp) | [https://payment.datatrans.biz/upp/jsp/XML\_authorize.jsp](https://payment.datatrans.biz/upp/jsp/XML_authorize.jsp) |
| Payment Page Endpoint | [https://pilot.datatrans.biz/upp/jsp/upStart.jsp](https://pilot.datatrans.biz/upp/jsp/upStart.jsp) | [https://payment.datatrans.biz/upp/jsp/upStart.jsp](https://payment.datatrans.biz/upp/jsp/upStart.jsp) |
| Tokenizer Endpoint | [https://pilot.datatrans.biz/upp/payment/tokenize](https://pilot.datatrans.biz/upp/payment/tokenize) | [https://payment.datatrans.biz/upp/payment/tokenize](https://payment.datatrans.biz/upp/payment/tokenize) |
| No-Show API | [https://pilot.datatrans.biz/upp/jsp/noShow.jsp](https://pilot.datatrans.biz/upp/jsp/noShow.jsp) | [https://payment.datatrans.biz/upp/jsp/noShow.jsp](https://payment.datatrans.biz/upp/jsp/noShow.jsp) |
| Pay-by-Email Endpoint | [https://pilot.datatrans.biz/upp/jsp/XML\_PayByEmail](https://pilot.datatrans.biz/upp/jsp/XML_PayByEmail) | [https://payment.datatrans.biz/upp/jsp/XML\_PayByEmail](https://payment.datatrans.biz/upp/jsp/XML_PayByEmail) |

---

> #### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



