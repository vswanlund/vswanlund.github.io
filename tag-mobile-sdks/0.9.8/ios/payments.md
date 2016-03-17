---
layout: page
title: Payments on iOS
permalink: /tag-mobile-sdks/0.9.8/ios/payments/
---

PowaTag provides the mechanism to pay for the user's selected goods and services. In order to make a payment, you first need to create an invoice which can be one of the following types:

* [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/baskets/) - Create a `PTKPaymentInvoice`
* [Appeals]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/appeal/) - Create a `PTKDonationInvoice`
* [POS Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/pospayments/) - Create a `PTKPosInvoice`

<br />

## Authorize the Invoice

Depending on thresholds set by the merchant, an invoice may require authorization from the end user before payment can be made. The user provides authorization by entering their passcode.  <br />
	
	<pre>if(invoice.authorizationRequired){
		PTKPaymentManager *pm = [PTKPaymentManager sharedManager];
		[pm authorizeForInvoice:invoice passcode:passcode completion:^(NSError *error) {
		 if (!error) {
		   // Invoice has been authorized
		 }
		}];
	}</pre>

## Paying for an Invoice

The invoice has been authorized and payment can now be made using either the CVV, encrypted CVV or no CVV.  
Use the `paymentInstrument.isCvvRequired()` method to determine if the CVV is required.


### Paying for an Invoice using CVV

1. Create PaymentDetails with the CVV:

	<pre>PTKPaymentDetails *paymentDetails = [PTKPaymentDetails paymentDetailsWithCvv:@"123"];</pre>

2. Use the PTKPaymentManager to pay for the invoice:

    <pre>PTKPaymentManager *pm = [PTKPaymentManager sharedManager];
   [pm payForInvoice:invoice paymentDetails:paymentDetails completion:^(PTKPayment *payment, NSError *error) {
     if (!error) {
       // Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for
     }
   }];</pre>
   
   
 ### Paying for an Invoice Using Encrypted CVV

1. Create EncryptedCVV with the CVV:

	<pre>PaymentInstrument paymentInstrument = PTKProfileManagerFactory.getInstance().getProfileManager().getCurrentProfile()getDefaultPaymentInstrument();
	EncryptedCVV encryptedCvv = EncryptedCvvStorage.getInstance().getCvv(paymentInstrument);</pre>
	
2. Use the PaymentManager to pay for the invoice:

	<pre>PTKPaymentManager *pm = [PTKPaymentManager sharedManager];
	[pm payForInvoice:invoice encryptedCvv:encryptedCvv completion:^(NSError *error) {
     if (!error) {
       // Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for
     }
	}];</pre>
   
   
### Paying for an Invoice Without CVV

1. Use the PaymentManager to pay for the invoice: 
   
	<pre>PTKPaymentManager *pm = [PTKPaymentManager sharedManager];
	[pm payForInvoice:invoice completion:^(PTKPayment *payment, NSError *error) {
	 if (!error) {
       // Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for
     }
	}];</pre>