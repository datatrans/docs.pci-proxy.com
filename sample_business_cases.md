# Case Studies

The following list of business cases gives an overview of business types that already use PCI Proxy.

## Middle Office

*You are a middle office that receives booking information on behalf of your clients.*

*Travel agencies use your software to drop new bookings. At some point, they will enter the customers’ payment data in your software. In order to minimize your PCI scope, this payment data should be added without touching your server.*

 PCI Proxy supports a varienty of [different approaches for you to collect the payment data][1]. Your server will never get in touch with sensitive card data which reduces your PCI scope immediately.

 The most common approach is to submit data directly from your software using our [payment pages][2]. Another option is [pay-by-email][3] where temporary payment links are issued that can be emailed to customers to let them enter their payment details by themselves. 

*On behalf of your clients you want to process the booking or transact with different endpoints (e.g. Expedia, Stripe, TUI, Lufthansa, etc.).*

 PCI Proxy allows you to [forward vaulted payment data][4] to PCI compliant third parties.



## Channel Manager

*You are a channel manager that requests or receives booking information from distribution channels, e.g. [Booking.com][5].*

*Hotels and accommodation providers transmit availabilities and prices to various distribution channels. It also automatically retrieves bookings including payment data from the online booking platforms.*

 PCI Proxy allows you to [extract payment data from web service calls][6] and securely store it in PCI Proxys' vault. Your server will never get in touch with sensitive card data which reduces your PCI scope immediately.

*Generally, you will store payment data only to allow your hotels to charge cards in case of a no-show.*

 PCI Proxy provides several ways on how to [use stored payment data][7]. Your clients can either [retrieve single payment data sets][8], [charge payment data][9] against a payment processor or [forward payment data][4] to a PCI-compliant third party, eg. Expedia.

 [1]: #collect
 [2]: #paymentpages
 [3]: #paybyemail
 [4]: #forward
 [5]: http://www.booking.com/
 [6]: #extract
 [7]: #use
 [8]: #retrieve
 [9]: #charge
