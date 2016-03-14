---
layout: page
title: Payments at a POS
permalink: /tag-mobile-sdks/0.9.8/android/pospayments/
---

. 
In order to make a POS payment, the following steps should be followed:

1. Scan the PowaTag QR code or NFC tag
Use the tag to obtain the workflow and POSBasket
Get the list of all POS_PAIRING triggered coupons 
obtain all coupon combinations    (couponmamanger.getpossiblediscounts()  (services return the possible combinations))
use coupon picker to present valid discounts to the user and allow them to pick valid discounts (combinations of coupons) (this component automatically refreshes display based on couponstate objects )
user clicks pay, and you create an POS Invoice (	POSManager.createInvoice (posinvoicedetails, )           -posinvoicedetails contains (20:00)
POSINvoice object is returned (including terminal id,)
if authorizationrequires = true then PaymentMethod.authorise(posinvoice) (24:00 - 28:30)   (two authorise methods, one for posinvoice and one for posinvoice + cvv)
encrypting CVV(30:50)
payment operation returns payment (including transaction ID for tracing transaction)




PowaTag supports payments for goods at an PowaTag enabled POS terminal. In order to make a payment, you first need to create an invoice for one of the supported goods or service types:

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





