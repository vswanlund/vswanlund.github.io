---
layout: page
title: Validators on Android
permalink: /tag-mobile-sdks/0.9.8/android/validators/
---

The SDK provides validators that can be used to ensure that the information entered by the user is valid.

There are three types of validators available for use:
* Low level validators - used for validating a aspects of a data type (e.g. not null, too long)
* Property validators - validate a property by using multiple low level validators and returning a single error (e.g. address line1) 
* Model validators - validates a model by using multiple property validators and returns a list of all properties that have errors(e.g. Address) 

The validators can be found in the package <code>com.powatag.android.sdk.validators</code>


* [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/baskets/) - PaymentInvoice
* [Campaigns]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/campaigns/) - DonationInvoice

<br />

# Paying for an Invoice using CVV

1. Create PaymentDetails with the CVV:

	<pre>PaymentDetails paymentDetails = new PaymentDetails("123");

2. Use the PaymentManager to pay for the invoice:

    <pre>PaymentManager pm = PaymentManager.getInstance();
	pm.pay(invoice, paymentDetails, new PowaTagCallback&lt;Payment&gt;() {
		public void onSuccess(Payment payment) {
		// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>

	The <code>PaymentManager</code> also provides a synchronous <code>pay</code> method which should only be used outside of the main thread to avoid performance bottlenecks.

	<pre>Payment payment = pm.pay(invoice, paymentDetails);</pre>

<br/>

# Paying for an Invoice Using an Encrypted CVV

1. Create EncryptedCVV with the CVV:

	<pre>Profile profile = ProfileManager.getInstance().getCurrentProfile();
	PaymentInstrument paymentInstrument = profile.getDefaultPaymentInstrument();
	EncryptedCVV encryptedCvv = EncryptedCvvStorage.getInstance().getCvv(paymentInstrument);

2. Use the PaymentManager to pay for the invoice:

	<pre>PaymentManager pm = PaymentManager.getInstance();
	pm.pay(invoice, encryptedCvv, new PowaTagCallback&lt;Payment&gt;() {
		public void onSuccess(Payment payment) {
		// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>

	The <code>PaymentManager</code> also provides a synchronous <code>pay</code> method which should only be used outside of the main thread to avoid performance bottlenecks.

	<pre>Payment payment = pm.pay(invoice, encryptedCvv);</pre>





