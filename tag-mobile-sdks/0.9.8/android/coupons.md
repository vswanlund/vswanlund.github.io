---
layout: page
title: Coupons on Android
permalink: /tag-mobile-sdks/0.9.8/android/coupons/
---

The coupon functionality allows a user to receive, store and redeem coupons in the app. They can then use these coupons when making purchases to get a discount from a specific merchant. 

Coupons are delivered to the user via event triggers. The two events that trigger the delivery of coupons are scanning a PowaTag or completing a POS payment. 

## Triggered Coupons while Obtaining the POS Basket

Merchants have the ability to create coupons that can be automatically delivered when a [POSBasket]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/posbaskets/) is retrieved. The coupons are not necessarily applicable to the current basket and it is not mandatory for the user to redeem any coupons during the current purchase.

The SDK enables the following steps:

* Obtain the `POSBasket` from the [workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/workflow/) associated with the scanned tag.
* Obtain all triggered coupons from the `PosBasketWorkflow` and display to the user.
* Obtain all coupons that can be redeemed against the current POS basket.
* Calculate the possible discounts using the `CouponManager`.

For detailed examples of each of these steps please review the [POS Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/posbaskets/) page 

<br/>## Triggered Coupons after Paying for a POS Invoice

Once the `PosInvoice` has been paid any triggered coupons are returned as part of the `Payment` response. Please see the [Payments]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/payments/) page for an example of how this is done.

<br />