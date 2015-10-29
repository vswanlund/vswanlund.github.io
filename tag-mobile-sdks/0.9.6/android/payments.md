---
layout: page
title: Payments on Android
permalink: /tag-mobile-sdks/0.9.6/android/payments/
---

PowaTag supports payments for a variety of different goods and services. In order to make a payment, you first need to create an invoice for one of the supported goods or service types:

* [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.6/android/baskets/) - PaymentInvoice
* [Campaigns]({{site.baseurl}}/tag-mobile-sdks/0.9.6/android/campaigns/) - DonationInvoice

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





