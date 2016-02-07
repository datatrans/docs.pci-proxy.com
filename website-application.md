# Collect payment data on a website or from an application

Let us assume you run a website or application where customers or agents entering payment data into a HTML web form. 

`PCI Proxy gives you several options on how to collect payment data from a HTML web form` and securely store it in our vault. A reference number (token) is issued and sent to your systems. 

*You are allowed to store the token in your system, as it is not PCI DSS relevant.*

The token can be used later on to charge, forward or retrieve payment data. 

*Add-on: All Collect options have a built-in feature to instantly charge payment data. All you need is an existing acquiring contract. *

**All options assure your servers never get in touch with sensitive card data to reduce your PCI scope to the least.**

## Overview

With the following 3 options, you can collect payment data and reduce your PCI scope to the least, qualifying for the [SAQ A](understand_pci_dss.html).

Redirect Mode| Lightbox Mode        | Inline Mode 
:------------:|:--------------------:|:-----------:
![Redirect Mode](redirect.png) | ![Lightbox Mode](lightbox.png) | ![Inline Mode](inline2.png)    
Redirect of consumer to payment page managed by Datatrans. | Payment pages are placed on shop as overlay (iFrame). | Payment page managed by Datatrans is incorporated with iFrame.    
[Demo + Code Sample](https://www.datatrans.ch/showcase/authorisation/redirect-mode) | [Demo + Code Sample](https://www.datatrans.ch/showcase/authorisation/lightbox-mode) | [Demo + Code Sample](https://www.datatrans.ch/showcase/authorisation/inline-mode)



## How to start

An easy way to start is by integrating our Redirect or Lightbox Payment Page. It takes care of building a conversion-optimised HTML form and validating input fields. 

To integrate the redirect mode you could use a simple HTML a tag:

```HTML
    <a href="https://pilot.datatrans.biz/upp/jsp/upStart.jsp
    		?merchantId=1100004624
    		&refno=pci-proxy-redirect
    		&amount=0
    		&currency=CHF
    		&theme=DT2015
            &uppAliasOnly=yes">Collect payment data</a>
    ```

If you need a more customizable approach, you can try our Inline Mode Payment Page. The Inline Mode allows you to integrate the payment form into your website with an iframe. With this approach you can adjust the style of the payment form by applying your custom CSS.

```HTML
<iframe width="600" 
	    height="500"
	    frameborder="0"
	    border="0"
	    src="https://pilot.datatrans.biz/upp/jsp/upStart.jsp
		    ?merchantId=1100004547
		    &refno=pci-proxy-inline
		    &amount=0
		    &currency=CHF
		    &uppAliasOnly=yes
		    &theme=Inline
		    &paymentmethod=VIS
		    &customTheme=mytheme">
    ```


