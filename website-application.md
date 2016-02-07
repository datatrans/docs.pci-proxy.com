# Collect payment data on a website or from an application

Let us assume you run a website or application where customers or agents entering payment data into a HTML web form. 

`PCI Proxy gives you several options on how to collect payment data from a HTML web form` and securely store it in our vault. A reference number (token) is issued and sent to your systems. 

*You are allowed to store the token in your system, as it is not PCI DSS relevant.*

The token can be used later on to charge, forward or retrieve payment data. 

*Add-on: All Collect options have a built-in feature to instantly charge payment data. All you need is an existing acquiring contract. *

**All options assure your servers never get in touch with sensitive card data to reduce your PCI scope to the least.**

Redirect Mode| Lightbox Mode        | Inline Mode 
:------------:|:--------------------:|:-----------:
<img src="../../img/redirect.png" width="150"> | <img src="../../img/lightbox.png" width="150"> | <img src="../../img/inline.png" width="150">      
Redirect of consumer to payment page managed by Datatrans. | Payment pages are placed on shop as overlay (iFrame). | Payment page managed by Datatrans is incorporated with iFrame.    
[Demo + Code Sample](https://www.datatrans.ch/showcase/authorisation/redirect-mode) | [Demo + Code Sample](https://www.datatrans.ch/showcase/authorisation/lightbox-mode) | [Demo + Code Sample](https://www.datatrans.ch/showcase/authorisation/inline-mode)

A comprehensive documentation of our Payment pages can be found on our [Showcase](https://datatrans.ch/showcase/authorisation/redirect-mode)

## How to start

An easy way to start is by integrating our Redirect or Lightbox Payment Page. It takes care of building a conversion-optimised HTML form, validating input fields, and securing your customers' payment data. 

```http
    <a href="https://pilot.datatrans.biz/upp/jsp/upStart.jsp
    		?merchantId=1100004624
    		&refno=1234567890
    		&amount=1000
    		&currency=CHF
    		&theme=DT2015
    &uppAliasOnly=yes">Collect payment data</a>
    ```

If you need a more customizable approach, you can try our Inline Mode Payment Page. The Inline Mode allows you to integrate the payment form into your website with an iframe. With this approach you can adjust the style of the payment form by applying your custom CSS.

```http
<iframe width="600" 
	height="500"
	frameborder="0"
	border="0"
	src="https://pilot.datatrans.biz/upp/jsp/upStart.jsp
		?theme=Inline
		&paymentmethod=VIS
		&merchantId=1100004547
		&refno=1337
		&amount=1000
		&uppAliasOnly=yes
		&currency=CHF
		&customTheme=mytheme">
		```

## Go Live
You will need to replace the test service URL and test merchant ID with your production credentials. You can get your credentials by [registering a free account](register).

