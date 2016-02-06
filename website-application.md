# On A Website/Application

If you run a website where you have customers enter their payment data into a HTML web form, PCI Proxy gives you several options on how to collect payment data and securely store it in PCI Proxys’ vault. Many of them assure your servers never get in touch with sensitive card data and reduce your PCI scope to the least.

> Add-on: All available options for collecting payment data offer the possibility to make instant charges to payment data. If you plan to use this feature, please make sure you have a valid acquiring contract with one of the following acquirer (financial institutions).

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

