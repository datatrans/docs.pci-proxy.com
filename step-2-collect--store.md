### Step 2: Securely collect sensitive card data and store for later use

In general, you have different inbound channels where you receive sensitive card data from customers or partners. The three main sources are:

| Website | Webservice | Native App |
| :--- | :--- | :--- |
| Your customers enter their credit card data on a form within your website. | You receive a request from a remote server including credit card data. | Your customers enter their credit card data on a form within your native app. |
| ie. Internet Booking Engine \(IBE\) | ie. XML messages with card data from [Booking.com](https://www.booking.com), [Expedia](https://www.expedia.com/), etc. | ie. Mobile Booking Application |

In order to avoid sensitive card data touching your systems, you pick the relevant source of credit card data and implement the PCI Proxy according to the respective Quickstart.

#### Quickstart:

With all described methods, **sensitive card data never touch your servers**.

| Jump to Quickstart &gt; [Website](/website-application.md) | Jump to Quickstart &gt; [Webservice](/webservice.md) | Jump to Quickstart &gt; [Native App](/mobile-app.md) |
| :--- | :--- | :--- |
| Seamlessly collect sensitive data within your website. | Simply redirect requests with sensitive data through PCI Proxy. | Natively collect sensitive card data within your mobile app \(iOS / Android\) |

> #### **Congrats, Level 1 completed: You are out of PCI scope! **
>
> Once sensitive card data is captured, we store the real credit card data in our vaults in Switzerland and return a credit card token to you. **Your systems never record, transmit or store real credit card data, only the token.** **Thus, you are out of PCI scope.** Move on to the next level.



