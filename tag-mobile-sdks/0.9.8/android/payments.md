---
layout: page
title: Payments on Android
permalink: /tag-mobile-sdks/0.9.8/android/payments/
---

PowaTag supports payments for a variety of goods and services. In order to make a payment, you first need to create an invoice which can be one of the following types:

* [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/baskets/) - Create a `PaymentInvoice`
* [Appeals]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/appeal/) - Create a `DonationInvoice`
* [POS Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/posbaskets/) - Create a `PosInvoice`

<br />
Making a payment for a Basket or a Donation is handled using the same set of step wheras paying for a POS basket requires a few additional steps.

## Basket and Donation Payments

### Paying for an Invoice using CVV

1. Create PaymentDetails with the CVV:

	<pre>PaymentDetails paymentDetails = new PaymentDetails("123");

2. Use the PaymentManager to pay for the invoice:

    <pre>PaymentManager paymentManager = ManagerFactory.getInstance().getPaymentManager();
	paymentManager.pay(invoice, paymentDetails, new PowaTagCallback&lt;Payment&gt;() {
		public void onSuccess(Payment payment) {
		// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>

	The <code>PaymentManager</code> also provides a synchronous <code>pay</code> method which should only be used outside of the main thread to avoid performance bottlenecks.

	<pre>Payment payment = pm.pay(invoice, paymentDetails);</pre>

<br/>

### Paying for an Invoice Using an Encrypted CVV

1. Create EncryptedCVV with the CVV:

	<pre>Profile profile = ManagerFactory.getInstance().getProfileManager().getCurrentProfile();
	PaymentInstrument paymentInstrument = profile.getDefaultPaymentInstrument();
	EncryptedCVV encryptedCvv = EncryptedCvvStorage.getInstance().getCvv(paymentInstrument);

2. Use the PaymentManager to pay for the invoice:

	<pre>PaymentManager pm = ManagerFactory.getInstance().getPaymentManager();
	pm.pay(invoice, encryptedCvv, new PowaTagCallback&lt;Payment&gt;() {
		public void onSuccess(Payment payment) {
		// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>

	The <code>PaymentManager</code> also provides a synchronous <code>pay</code> method which should only be used outside of the main thread to avoid performance bottlenecks.

	<pre>Payment payment = pm.pay(invoice, encryptedCvv);</pre>


## POS Payments

----------17 Feb------------------
Pay at Pos 6:33
    scan tag, obtain workflow of type posbasket
	triggered coupons
	pos basket includes list of available coupons that match the pos basket
	SDK retrieves possible coupon combinations
	couponmamanger.getpossiblediscounts()  (services return the possible combinations)
	CouponPicker is provided to app developer (this component automatically refreshes display based on couponstate objects )
	POSManager.createInvoice (posinvoicedetails, )           -posinvoicedetails contains (20:00)
	POSINvoice object is returned (including terminal id,)
	if authorizationrequires = true then PaymentMethod.authorise(posinvoice) (24:00 - 28:30)   (two authorise methods, one for posinvoice and one for posinvoice + cvv)
	encrypting CVV(30:50)
	payment operation returns payment (including transaction ID for tracing transaction)



### Paying for an Invoice using CVV

1. Create PaymentDetails with the CVV:

	<pre>PaymentDetails paymentDetails = new PaymentDetails("123");

2. Use the PaymentManager to pay for the invoice:

    <pre>PaymentManager paymentManager = ManagerFactory.getInstance().getPaymentManager();
	paymentManager.pay(invoice, paymentDetails, new PowaTagCallback&lt;Payment&gt;() {
		public void onSuccess(Payment payment) {
		// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>

	The <code>PaymentManager</code> also provides a synchronous <code>pay</code> method which should only be used outside of the main thread to avoid performance bottlenecks.

	<pre>Payment payment = pm.pay(invoice, paymentDetails);</pre>

<br/>

### Paying for an Invoice Using an Encrypted CVV

1. Create EncryptedCVV with the CVV:

	<pre>Profile profile = ManagerFactory.getInstance().getProfileManager().getCurrentProfile();
	PaymentInstrument paymentInstrument = profile.getDefaultPaymentInstrument();
	EncryptedCVV encryptedCvv = EncryptedCvvStorage.getInstance().getCvv(paymentInstrument);

2. Use the PaymentManager to pay for the invoice:

	<pre>PaymentManager pm = ManagerFactory.getInstance().getPaymentManager();
	pm.pay(invoice, encryptedCvv, new PowaTagCallback&lt;Payment&gt;() {
		public void onSuccess(Payment payment) {
		// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>

	The <code>PaymentManager</code> also provides a synchronous <code>pay</code> method which should only be used outside of the main thread to avoid performance bottlenecks.

	<pre>Payment payment = pm.pay(invoice, encryptedCvv);</pre>


