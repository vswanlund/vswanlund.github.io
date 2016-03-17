---
layout: page
title: Payments on Android
permalink: /tag-mobile-sdks/0.9.8/android/payments/
---

PowaTag provides the mechanism to pay for the user's selected goods and services. In order to make a payment, you first need to create an invoice which can be one of the following types:

* [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/baskets/) - Create a `PaymentInvoice`
* [Appeals]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/appeal/) - Create a `DonationInvoice`
* [POS Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/posbaskets/) - Create a `PosInvoice`

<br />
The steps for making a payment can be found below. 

## Authorize the invoice

Depending on thresholds set by the merchant, an invoice may require authorization from the end user before payment can be made. The user provides authorization by entering their passcode.  <br />

````
PaymentManager paymentManager = ManagerFactory.getInstance().getPaymentManager();
if (invoice.isAuthorizationRequired()){
	// prompt user for their passcode
	paymentManager().authorize(invoice, passcodeEditText.getText().toString(), new PowaTagCallback<Void>() {
		@Override
		public void onSuccess(@Nullable Void aVoid) {
		}
			
		@Override
		public void onError(@NonNull PowaTagException e) {
		}
	});
}
````	
<br />
	



The synchronous version of the <code>authorize</code> method should <b>not be used in the main thread</b> to avoid performance issues

<code>paymentManager.authorize(invoice, passcodeEditText.getText().toString());</code>

<br />
This can also be done using RxJava:

<pre>RxManagerFactory.getInstance().getProfileManager().authorize(invoice, passcodeEditText.getText().toString()).subscribe(new Subscriber&lt;Void&gt;() {
	@Override
	public void onCompleted() {
	} 

	@Override
	public void onError(Throwable e) {
	}

	@Override
	public void onNext(Address addedAddress) {
	}
});</pre>   


## Paying for an Invoice using CVV

1. Create PaymentDetails with the CVV:

	<pre>PaymentDetails paymentDetails = new PaymentDetails("123");

3. Use the PaymentManager to pay for the invoice:

	<pre>PaymentManager paymentManager = ManagerFactory.getInstance().getPaymentManager();
	if (invoice.isAuthorizationRequired()){
		// obtain passcode from user
		paymentManager().authorize(invoice, passcodeEditText.getText().toString(), new PowaTagCallback<Void>() {
			@Override
			public void onSuccess(@Nullable Void aVoid) {
				paymentManager.pay(invoice, paymentDetails, new PowaTagCallback&lt;Payment&gt;() {
					public void onSuccess(Payment payment) {
					
					}
					public void onError(PowaTagException exception) {
					}
				}

			@Override
			public void onError(@NonNull PowaTagException e) {

			}
	});
	}</pre>
<br />	

    
	The synchronous version of the <code>addAddress</code> method should <b>not be used in the main thread</b> to avoid performance issues

    <code>paymentManager.authorize(invoice,) addedAddress = pm.addAddress(addressDetails);</code>
	
	<br />
	This can also be done using RxJava:
	
    <pre>RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
    profileManager.addAddresss(addressDetails).subscribe(new Subscriber&lt;Address&gt;() {
		@Override
		public void onCompleted() {
		} 
 
		@Override
		public void onError(Throwable e) {
		}

		@Override
		public void onNext(Address addedAddress) {
		}
	});</pre>   


   <pre>paymentManager.pay(invoice, paymentDetails, new PowaTagCallback&lt;Payment&gt;() {
		public void onSuccess(Payment payment) {
		
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>
	
	
					paymentManager.pay(invoice, paymentDetails, new PowaTagCallback&lt;Payment&gt;() {
					public void onSuccess(Payment payment) {
					
					}
					public void onError(PowaTagException exception) {
					}
				}


	The <code>PaymentManager</code> also provides a synchronous <code>pay</code> method which should only be used outside of the main thread to avoid performance bottlenecks.

	<pre>Payment payment = pm.pay(invoice, paymentDetails);</pre>
	
	
	This can also be done using RxJava:
	
    <pre>RxPaymentManager paymentManager = RxManagerFactory.getInstance().getPaymentManager();
    paymentManager.pay(invoice,paymentDetails).subscribe(new Subscriber&lt;Payment&gt;() {
		@Override
		public void onCompleted() {
		} 
 
		@Override
		public void onError(Throwable e) {
		}

		@Override
		public void onNext(Payment payment) {
			// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
	});</pre>


<br/>

## Paying for an Invoice Using an Encrypted CVV

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
	
	
	This can also be done using RxJava:
	
    <pre>RxPaymentManager paymentManager = RxManagerFactory.getInstance().getPaymentManager();
    paymentManager.pay(invoice,encryptedCvv).subscribe(new Subscriber&lt;Payment&gt;() {
		@Override
		public void onCompleted() {
		} 
 
		@Override
		public void onError(Throwable e) {
		}

		@Override
		public void onNext(Payment payment) {
			// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
	});</pre>

## Paying for an Invoice Using an Encrypted CVV

1. Use the PaymentManager to pay for the invoice:

	<pre>Profile profile = ManagerFactory.getInstance().getProfileManager().getCurrentProfile();
	PaymentInstrument paymentInstrument = profile.getDefaultPaymentInstrument();
	if(!paymentInstrument.isCvvRequired(){
		PaymentManager pm = ManagerFactory.getInstance().getPaymentManager();
		pm.pay(invoice, new PowaTagCallback&lt;Payment&gt;() {
		public void onSuccess(Payment payment) {
		// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>

	The <code>PaymentManager</code> also provides a synchronous <code>pay</code> method which should only be used outside of the main thread to avoid performance bottlenecks.

	<pre>Payment payment = pm.pay(invoice);</pre>
	
	
	This can also be done using RxJava:
	
    <pre>RxPaymentManager paymentManager = RxManagerFactory.getInstance().getPaymentManager();
    paymentManager.pay(invoice).subscribe(new Subscriber&lt;Payment&gt;() {
		@Override
		public void onCompleted() {
		} 
 
		@Override
		public void onError(Throwable e) {
		}

		@Override
		public void onNext(Payment payment) {
			// Payment contains information such as the PowaTag payment ID, Merchant payment ID and the invoice that was paid for.
		}
	});</pre>	

	
## POS Basket Payments

----------17 Feb------------------
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


