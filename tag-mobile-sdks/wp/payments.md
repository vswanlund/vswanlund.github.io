---
layout: page
title: Payments on Windows Phone
permalink: /tag-mobile-sdks/wp/payments/
---

PowaTag supports payments for a variety of different goods and services. In order to make a payment, you first need to create an invoice for one of the supported goods or service types:

* [Baskets]({{site.baseurl}}/tag-mobile-sdks/wp/baskets/) - PaymentInvoice
* [Campaigns]({{site.baseurl}}/tag-mobile-sdks/wp/campaigns/) - DonationInvoice

<br />

# Paying for an Invoice using <code>PaymentDetails</code>

1. Create PaymentDetails with the CVV:

	<pre>PaymentDetails paymentInvoiceDetails = new PaymentDetails("123");

2. Use the PaymentManager to pay for the invoice:

    <pre>PaymentManager pm = PaymentManager.GetInstance();
   Payment payment = await pm.PayAsync(invoice, paymentDetails);
   // Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for</pre>
