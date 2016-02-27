# Collect Payment Data

Whether you receive payment data via API, accept credit cards on a website or collect them in a mobile app, you can use PCI Proxy APIs to keep payment data off your systems.

### Understanding the PCI Proxy

- You can interpose our API between you and the source of credit cards to automatically tokenize the payment data. 
- PCI Proxy filters messages for payment data and replaces them with a reference number (token).
- The payment data is encrypted and securely stored in our vault while you receive the token. 

Thereby **your systems never touch payment data but remain flexible**. You still have the possibility to charge the payment data by using the token.



## Choose API 

In general, there are three environments in which you might receive payment data:

| **[Web Service](webservice.html)** | **[Web Interface](website-application.html)** | **[Native Mobile App](mobile-app.html)** |
| -- | -- | -- |
| XML / SOAP / JSON / etc. | Website / Application | iOS / Android |
| e.g. Booking.com / Expedia / Stripe | e.g. Checkout / IBE / Callcenter | e.g. Checkout / IBE in mobile app |


*If you have specific environments that are not listed, please get in touch. We are quick and flexible to enhance our features. *


**Considering the following cases and choose the API you need:**

 - You receive or request messages including payment data via webservice APIs from your partners or clients. For example, you receive transaction related data via XML from **Booking.com**. [Learn about Webservice.](webservice.html)
 
 - You collect payment data on a website. For instance, you have an Internet booking engine running on your website. [Learn about Payment Pages.](website-application.html)
 
 - You have a native mobile app (iOS or Android) and collect payment from customers. For instance, you give your clients the opportunity to book your product or service through a mobile app. [Learn about Payment Libraries.](mobile-app.html)
 
 - You need to enter payment data into your system on behalf of your clients. For instance, you are a travel agency that works with a middle office system and want to avoid that employees get in contact with payment data. [Learn about Pay-by-Email.](paybyemail)