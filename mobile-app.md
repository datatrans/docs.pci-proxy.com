# Quickstart: Collect credit cards from native mobile apps

Let us assume you offer a native mobile app to your customers where they can enter credit cards.

`Our SDKs for iOS and Android collect credit cards in native apps` and automatically store it in our secure vault. A reference number \(token\) is issued and sent to your systems.

**All SDKs assure your servers never get in touch with sensitive card data to reduce your PCI scope to the least.**

---

Our library allows you to tokenize credit cards by using your own native forms \(hidden mode\). In hidden mode, you invoke our payment library with the necessary credit card data to generate an alias.

## 1a. Integrate on iOS

**You can use the following code snippet to generate a token:**

```swift
DTCardPaymentMethod* card = [[DTCardPaymentMethod alloc] 
    initWithPaymentMethod:DTPaymentMethodVisa 
      number:@"4444333322221111"
      expMonth:12 
      expYear:2015 
      cvv:@"123" 
      holder:nil
  ];

DTAliasRequest* ar = [[DTAliasRequest alloc]
    initWithMerchantId:YOUR_MERCHANT_ID
      cardPaymentMethod:card verifyingTransaction:NO];

DTPaymentController* pc = [DTPaymentController 
    paymentControllerWithDelegate:self aliasRequest:ar];
```

---

## 1b. Integrate on Android

**You can use the following code snippet to generate a token:**

```java
PaymentMethodCreditCard pm = new PaymentMethodCreditCard(
    PaymentMethodType.VISA,
    "4444333322221111", 
    2015, 
    12, 
    123, 
    "Max Muster");

AliasRequest ar = new AliasRequest(
    YOUR_MERCHANT_ID, 
    pm, 
    false);

PaymentProcessAndroid ppa = new PaymentProcessAndroid(dc,ar);
```

---

#### Reference

| iOS Library for iPhone, iPad, iPod touch |
| --- |
| [Release Notes](https://pilot.datatrans.biz/showcase/doc/iOS_Release_Notes.pdf) |
| [Developer Manual](https://pilot.datatrans.biz/showcase/doc/iOS_Developers_Manual.pdf) |
| [iOS Library \(zip\)](https://pilot.datatrans.biz/showcase/doc/iOS_Library.zip) |

| Android Library |
| --- |
| [Release Notes](https://pilot.datatrans.biz/showcase/doc/Android_Release_Notes.pdf) |
| [Developer Manual](https://pilot.datatrans.biz/showcase/doc/Android_Developers_Manual.pdf) |
| [Android Library \(zip\)](https://pilot.datatrans.biz/showcase/doc/Android_Library.zip) |
| [Sample application](https://github.com/datatrans/android-sample-app) |

---

> ### Congrats, Level 2 completed: Your mobile app is out of PCI scope!
>
> You have securely captured sensitive card data within your app without sensitive data touching your servers. **Your systems never record, transmit or store real credit card data, only the token.** **Thus, you are out of PCI scope.** Move on and learn how you can use stored card data. Please continue to [**Step 3**](/step-3-use-stored-data.md).
>
> ##### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



