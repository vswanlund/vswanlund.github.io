---
layout: page
title: Validators on Android
permalink: /tag-mobile-sdks/0.9.8/android/validators/
---

The SDK provides validators that should be used to ensure that the information entered by the user is valid.



Low level validators (e.g. not null, too long)
Second layer property validators (e.g. address line1) made up of multiple low level validators, return a single error
Model validators (e.g. Address) made up of multiple property validators, returns a list of all properties that have errors

The validators can be found at com.powatag.android.sdk.validators


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





