---
layout: page
title: Payments on iOS
permalink: /tag-mobile-sdks/0.9.8/ios/payments/
---

PowaTag supports payments for a variety of different goods and services. In order to make a payment, you first need to create an invoice which can be one of the following types:

* [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/baskets/) - Create a `PTKPaymentInvoice`
* [Appeals]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/appeal/) - Create a `PTKDonationInvoice`
* [POS Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/pospayments/) - Create a `PTKPosInvoice`

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
