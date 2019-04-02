# Integrations

To apply merchant initiated transactions \(MIT\) you need to authenticate the cardholder on the very first saving of the credit card. We therefore adapt our APIs to mark payments as merchant initiated transactions collected through your frontend. Based on the  result of the 3D secure authentication process the transaction can go through either a frictionless or challenge flow. 

As well we are extending the [charge API](../../use-stored-cards/authorize.md) to authorise payment requests using authentication data received from a third-party 3D Secure 2 provider.

| API | Status |
| :--- | :--- |
| [SecureFields](../../collect-and-store-cards/capture-iframes/) \(Frontend\) | 🚧 Under development |
| [Charge ](../../use-stored-cards/authorize.md)\(Server-to-Server\) | 🚧 Under development |
| Mobile SDK \(Android / iOS\) | 🚧 Coming soon |
| [Filter](../../collect-and-store-cards/filter-payloads.md) \(Server-to-Server\) | ✅ Supported  |
| [Forward](../../use-stored-cards/forward/) \(Server-to-Server\) | ✅ Supported  |

