# Step 2: Collect sensitive card data and store for later use

In general, you have different inbound channels where you receive sensitive card data from customers or partners.

## 1. Choose source of card data

The three main sources of credit card data are:

| Website | Webservice | Native App |
| :--- | :--- | :--- |
| Your customers enter their credit card data on a form within your website. | You receive a request from a remote server including credit card data. | Your customers enter their credit card data on a form within your native app. |
| ie. Internet Booking Engine \(IBE\) | ie. XML messages with card data from [Booking.com](https://www.booking.com), [Expedia](https://www.expedia.com/), etc. | ie. Mobile Booking Application |

In order to avoid sensitive card data touching your systems, you pick the relevant source of credit card data and implement the PCI Proxy according to the respective Quickstart.

**With all described methods, sensitive card data never touch your servers**.

| Jump to Quickstart &gt; [Website](/website-application.md) | Jump to Quickstart &gt; [Webservice](/webservice.md) | Jump to Quickstart &gt; [Native App](/mobile-app.md) |
| :--- | :--- | :--- |
| ![](/assets/Website.png) | ![](/assets/Webservice.png) | ![](/assets/App.png) |
| Seamlessly collect sensitive data within your web application. | Securely extract sensitive card data out of your web service communication. | Natively collect sensitive card data within your mobile app \(iOS / Android\). |

---

> ### **Congrats, Level 2 completed: You are out of PCI scope! **
>
> You have securely captured sensitive card data. **Your systems never record, transmit or store real credit card data, only the token.** **Thus, you are out of PCI scope.** Move on and learn how you can use stored card data. Please continue to [**Step 3**](/step-3-use-stored-data.md).
>
> ##### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



