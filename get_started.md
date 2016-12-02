# Quick Start Guide

Get ready to start collecting cardholder data and more. The following sections describe how to use the PCI Proxy Sandbox: 
                  
                  





1.	Create a Sandbox Account

2.	Generate a Security Sign  

3.	Choose your API

3.	Add a Channel, Third Party or Payment Gateway to your Sandbox

4.	Start collect or extract payment information




---




## 1. Create A Sandbox Account

To create a new test account in the Sandbox: 

5.	Sign up for a free test account at http://www.pci-proxy.com/#/signup

6.	Once submitted, you will receive your Sandbox login data.

7.	Log in to the Sandbox https://pilot.datatrans.biz/.

8.	Navigate to user administration and create a new password. 


If you need further information about the sandbox environment, please visit https://docs.pci-proxy.com/live_mode-test.html



## 2. Generate a Security Sign: 



Once you logged in and set your password, you have to generate a security sign:


1.	Navigate to UPP Administration

2.	Go to Security 

3.	Choose between Static Sign 1 (X-CC-SIGN) and Dynamic Sign 2 (SHA HASH) 

4.	Generate new sign or salt 

5.	Click on Update 


If you do not know which sign you need, please visit https://docs.pci-proxy.com/live_mode-test.html


## 3. Add a Channel or Third Party to your Sandbox


Before you can collect or extract cardholder data, you will need to send us the following information to setup@pci-proxy.com: 

  1.	Channel Type (Define if it is a push or pull channel)

  2.	API Endpoint (The URL where we should forward the request to)

  3.	Sample Request & Response (Please Include API name, required heards, auth fields and request method)

  4.	Attestation of Compliance (only for Forwards)

