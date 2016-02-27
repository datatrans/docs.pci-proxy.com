# Features

PCI Proxy has 3 major features: Collect, Validate, Use. 

|**[Collect](collect_payment_data.html)**|**[Validate](validate.html)**|**[Utilize](utilize)**|
|---|---|---|
|From [Web Service](webservice.html)|[Credit Card Check](validate.html)|[Forward](forward.html)|
|From [Website / Application](website-application.html)||[Charge](charge.html)|
|From [Mobile App](mobile-app.html)||[Show](show.html)|

## Collect

To keep sensitive payment data from touching your systems, you need to collect payment data with our APIs. They will automatically tokenize the payment data before it is sent to your system.

In general, there are three universes in which you might receive payment data. 

| **[Web Service](webservice.html)** | **[Web Interface](website-application.html)** | **[Mobile App](mobile-app.html)** |
| -- | -- | -- |
| XML / SOAP / JSON / etc. | Website / Application | iOS / Android |
| e.g. Booking.com / Expedia / Stripe | e.g. Checkout / IBE / Callcenter | e.g. Checkout / IBE in mobile app |


*If you have specific environments that are not listed, please get in touch. We are quick and flexible to enhance our features. *

## Validate

After collection you might want to confirm payment data is valid and can be charged. 

## Utilize

Eventually you want to make use of collected payment data. 

| **PCI Proxy allows you to...** |
| -- |
| *[charge](charge.html) payment data* directly through a payment gateway (e.g. Datatrans) |
| *[forward](forward.html) payment data* to PCI-compliant third-parties (e.g. Expedia) |
| *[show](show.html) single payment data sets* (e.g. charge credit card with your POS terminal) |
