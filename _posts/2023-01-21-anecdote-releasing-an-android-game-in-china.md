---
title:  "Anecdote: Releasing an Android game in China"
date:   2023-01-21 18:00:00 -0600
categories: anecdote
tags: android
---

As you probably know, China has a *very weird* Android ecosystem since we don't have anything like Google Play Store, so almost every smartphone vendor has their own Android market, with their own SDKs. You **have** to integrate those SDKs.

Also unlike in United States where a credit card can handle almost everything, we have banks, Alipay, WeChat, and other small services and normally we don't pay directly from our bank accounts.

So the whole chain looks like this:

```mermaid
graph LR
  Money((Your money)) --> Bank1
  Money --> Bank2
  Money --> Bank3
  Money --> Banks[Other Banks]

  Bank1 --> Online((Online Payment Services))
  Bank2 --> Online
  Bank3 --> Online
  Banks --> Online

  Online --> Alipay
  Online --> WeChat
  Online --> Bank1Online[Bank1 Online Pay]
  Online --> Bank2Online[Bank2 Online Pay]
  Online --> Bank3Online[Bank3 Online Pay]
  Online --> BanksOnline[Other Banks Online Pay]
  Online --> WhateverPay[Other Pay Services]

  Alipay --> Market((Android App Stores))
  WeChat --> Market
  Bank1Online --> Market
  Bank2Online --> Market
  Bank3Online --> Market
  BanksOnline --> Market
  WhateverPay --> Market

  Market --> Huawei[Huawei Vendor SDK]
  Market --> Xiaomi[Xiaomi Vendor SDK]
  Market --> Oppo[Oppo Vendor SDK]
  Market --> Vivo[Vivo Vendor SDK]
  Market --> Vendor[Other Vendor SDK]
  Market --> Tencent[Tencent App Store SDK]
  Market --> TapTap[TapTap]
  Market --> WhateverStore[Other Store SDK]

  Huawei --> Build((Vendor Specific Game Build))
  Xiaomi --> Build
  Oppo --> Build
  Vivo --> Build
  Tencent --> Build
  TapTap --> Build
  WhateverStore --> Build
```

Imagine making a build for each smartphone brand and having developers to maintain and test those builds.
{: .notice--success}

As a result we had amalgamated payment SDKs (chinese name: 聚合支付). *One SDK to rule them all*.

Then it turned out smartphone vendors didn't like those amalgamated SDKs for whatever reasons and sometimes they even forbid the use of those SDKs.
