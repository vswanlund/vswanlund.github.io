---
layout: page
title: Payments on Android
permalink: /tag-mobile-sdks/android/payments/
---

PowaTag supports payments for a variety of different goods and services. In order to make a payment, you first need to create an invoice for one of the supported goods or service types:

* [Baskets]({{site.baseurl}}/tag-mobile-sdks/android/baskets/) - PaymentInvoice
* [Campaigns]({{site.baseurl}}/tag-mobile-sdks/android/campaigns/) - DonationInvoice

<br />

# Paying for an Invoice

1. Create PaymentDetails with the CVV:

	<pre>PaymentDetails paymentDetails = new PaymentDetails("123");

2. Use the PaymentManager to pay for the invoice:

    <pre>PaymentManager pm = PaymentManager.getInstance();
   pm.pay(invoice, paymentDetails, new PowaTagCallback&lt;Payment&gt;() {
     public void onSuccess(Payment payment) {
       // Payment contains information such as transaction ID
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>
