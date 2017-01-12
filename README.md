# PCI Proxy Documentation

Welcome to PCI Proxy! With this documentation you get familiar with PCI Proxy and reduce your PCI scope in no time.

## Overview

Before we get started, take a minute and let us introduce you to the magic of PCI Proxy.

> ##### PCI Proxy is a tokenization service that reduces your PCI scope in a simple and secure way.

PCI Proxy let you **instantly collect and store credit card data **without touching your servers. Once stored and tokenized, you can simply **use tokens to validate, charge, display, or forward **your stored card data.

Our customer base spans across many different industries and business types. All of them have specific needs and processes in place. PCI Proxy is build with flexibility in mind to accommodate those needs at best.

PCI Proxy is a battle-tested tokenization solution that is powered by [Datatrans AG](https://www.datatrans.ch/), the leading Swiss Payment Service Provider.

---

## Integration: Getting Started

PCI Proxy can be integrated by following two steps. Simply level through our guides to achieve PCI compliance:

* #### Step 1: Create Sandbox
* #### Step 1: [Securely collect sensitive card data and store for later use](#step1-securely-collect-sensitive-card-data)
* #### Step 2: [Use stored card data](#use-stored-card-data)

#### 

### Step 1: Securely collect sensitive card data and store for later use

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

---

### Step 2: Use stored card data

Now that you have your credit card token, you can make use of it. PCI Proxy allows you to keep your existing business processes as before. As we connect every stored credit card number to a specific credit card token, you simply use the token to tell PCI Proxy what you want to do with the underlying credit card data.

With the following three methods you can use stored card data:

| Learn to &gt; [Charge](/charge.md) a stored card | Learn to &gt; [Forward](/charge.md) a stored card | Learn to &gt; [Show](/show.md) a stored card |
| :--- | :--- | :--- |
| Use our payment gateway to charge or validate a stored card. | Pass stored card data on to any PCI-compliant 3rd party. | Let authorized users manually de-tokenize stored card to see it. |

> #### Done! Enjoy PCI compliance in a risk-free environment.
>
> Now you should have covered all your business processes that existed before you implemented PCI Proxy - just without the PCI hassle. Keep in mind that you can use stored data as often as you need it.

---

# Questions? {#questions}

Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.

Phone: +41 44 256 81 91  
Email: support@pci-proxy.com

