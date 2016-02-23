# Collect Payment Data

Whether you receive payment data via API, accept credit cards on a website or collect them in a mobile app, you can use PCI Proxy APIs.

## Understanding the PCI Proxy

- Our APIs switch between you and the source to automatically tokenize the payment data. 
- PCI Proxy filters messages for payment data and replaces them with a reference number (token).
- The payment data is encrypted and securely stored in our vault while you receive the token. 

Thereby **your systems never touch payment data but remain flexible**. You still have the possibility to charge the payment data by using the token.



## Considering the following cases:

PCI Proxy APIs are organized in environments, meaning the different ways on how you could possibly receive or collect payment data. 

 - You receive or request messages including payment data via webservice APIs from your partners or clients. For example, you receive transaction related data via XML from Booking.com. [Learn about webservice.](webservice.html)
 
 - You collect payment data on a website. For instance, you have an Internet booking engine running on your website. [Learn about Payment Pages.](website-application.html)
 
 - You have a native mobile app (iOS or Android) and collect payment from customers. For instance, you give your clients the opportunity to book your product or service through a mobile app. [Learn about Payment Libraries.](mobile-app.html)
 
 - You need to enter payment data into your system on behalf of your clients. For instance, you are a travel agency that works with a middle office system and want to avoid that employees get in contact with payment data. [Learn about Pay-by-Email.](paybyemail)