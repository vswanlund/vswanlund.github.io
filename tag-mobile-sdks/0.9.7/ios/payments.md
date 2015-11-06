---
layout: page
title: Payments on iOS
permalink: /tag-mobile-sdks/0.9.7/ios/payments/
---

PowaTag supports payments for a variety of different goods and services. In order to make a payment, you first need to create an invoice for one of the supported goods or service types:

* [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.7/ios/baskets/) - PTKPaymentInvoice
* [Campaigns]({{site.baseurl}}/tag-mobile-sdks/0.9.7/ios/campaigns/) - PTKDonationInvoice

<br />

# Paying for an Invoice using PaymentDetails

1. Create PaymentDetails with the CVV:

	<pre>PTKPaymentDetails *paymentDetails = [PTKPaymentDetails paymentDetailsWithCvv:@"123"];</pre>

2. Use the PTKPaymentManager to pay for the invoice:

    <pre>PTKPaymentManager *pm = [PTKPaymentManager sharedManager];
   [pm payForInvoice:invoice paymentDetails:paymentDetails completion:^(PTKPayment *payment, NSError *error) {
     if (!error) {
       // Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for
     }
   }];</pre>
