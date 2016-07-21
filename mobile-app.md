# Collect credit cards from native mobile apps

Let us assume you offer a native mobile app to your customers where they can enter credit cards.

`Our SDKs for iOS and Android collect credit cards in native apps` and automatically store it in our secure vault. A reference number (token) is issued and sent to your systems.

*You are allowed to store the token in your system, as it is not PCI DSS relevant.*

The token can be used later on to validate, charge, forward or show credit cards.

**All SDKs assure your servers never get in touch with sensitive card data to reduce your PCI scope to the least.**

## How to start

> [Sign up](https://www.pci-proxy.com/#/signup) for a free developer test account.

Our library allows you to tokenize credit cards by using your own native forms (hidden mode). In hidden mode, you invoke our payment library with the necessary credit card data to generate an alias.

| Supported Credit Card Brands |
| -- |
| American Express, Mastercard, Visa, Mastercard|

### Integrate on iOS

| iOS Library for iPhone, iPad, iPod touch |
| -- |
| [Release Notes](https://pilot.datatrans.biz/showcase/doc/iOS_Release_Notes.pdf) |
| [Developer Manual](https://pilot.datatrans.biz/showcase/doc/iOS_Developers_Manual.pdf) |
| [iOS Library (zip)](https://pilot.datatrans.biz/showcase/doc/iOS_Library.zip) |

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

### Integrate on Android

| Android Library |
| -- |
| [Release Notes](https://pilot.datatrans.biz/showcase/doc/Android_Release_Notes.pdf) |
| [Developer Manual](https://pilot.datatrans.biz/showcase/doc/Android_Developers_Manual.pdf) |
| [Android Library (zip)](https://pilot.datatrans.biz/showcase/doc/Android_Library.zip) |
| [Sample application](https://github.com/datatrans/android-sample-app) |

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

