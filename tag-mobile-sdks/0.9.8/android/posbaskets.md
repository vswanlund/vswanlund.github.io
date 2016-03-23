---
layout: page
title: Payments at a POS
permalink: /tag-mobile-sdks/0.9.8/android/posbaskets/
---

Pay at POS allows the user to pay for goods in-store at a POS terminal with the app via a PowaTag [trigger]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/tiggers/). 

The PowaTag enabled POS terminal generates a `POSBasket` in PowaTag which is a collection of `BasketItem` which stores the product variant and quantity. The contents of a POSBasket cannot be modified by the user and the only actions that can be performed is to apply [coupons]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/coupons/) and to create an invoice for the basket. 


In order to make a POS payment, the following steps should be completed first:

* The user presents a basket of goods to the cashier at the POS.
* Cashier rings up the goods and generates a `POSBasket`.
* User scans the PowaTag [trigger]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/triggers/) (QR or NFC) associated with the POS terminal.
* The App retrieves the `POSBasket` from the [workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/workflow/) associated with the tag.

The following steps can then be followed:


## Obtaining Triggered Coupons

The merchant has the ability to create coupons for use by their customers and can set them to be automatically delivered when the POSBasket is retrieved. It is not mandatory for the coupons to be redeemed by the user during the current purchase as they are stored for later use. It is also not a given that any of the coupons will be applicable to the current basket.

1. Obtain all triggered coupons for the merchant by using the `PosBasketWorkflow`

<pre>Set&lt;Coupon&gt; coupons = workflow.getTriggeredCoupons();
if(!coupons.isEmpty()){
	for (for (Coupon coupon : coupons){
		//obtain coupon details and display coupon list to user.
	}
}</pre>

<br/>


## Calculating Possible Discounts

The POSBasket contains the set of all coupons that can be redeemed against the current basket. These coupons need to be combined to provide the user with the distinct possible discounts that can be applied to the basket.

1. Calculate the possible discounts using the `CouponManager`

<pre>ManagerFactory.getInstance().getCouponManager().getAvailableDiscounts(posBasket, new PowaTagCallback&lt;List&lt;Discount&gt;&gt;() {
	@Override
	public void onSuccess(@NonNull Set&lt;Discount&gt; possibleDiscounts) {
		// Display the discounts to the user and use discount.getSavings() to show the savings.
		// Let the user select one.
	}

	@Override
	public void onError(@NonNull PowaTagException e) {
	}
});</pre>

The synchronous version of the <code>getAvailableDiscounts</code> method is available but should not be used in the main thread to avoid performance issues

<code>List&lt;Discount&gt; possibleDiscounts = ManagerFactory.getInstance().getCouponManager().getAvailableDiscounts(posBasket);</code>
	
<br />  
	

This can also be done using RxJava:
	
<pre>RxManagerFactory.getInstance().getCouponManager().getAvailableDiscounts(posBasket).subscribe(new Subscriber&lt;List&lt;Discount&gt;&gt;() {
	@Override
	public void onCompleted() {
	} 
	@Override
	public void onError(Throwable e) {
	}

	@Override
	public void onNext(List&lt;Discount&gt; possibleDiscounts) {
		// Display the discounts to the user and use discount.getSavings() to show the savings.
		// Let the user select one.
	}
});  </pre>

<br />

## Creating an Invoice for the PosBasket

Once the user clicks the 'Pay' button, a `POSInvoice` needs to be created before the payment can be processed.

1. Create a `PosInvoiceDetails` to provide the payment instrument, posBasket and selected coupons to apply to the the invoice:

<pre>// Obtain the coupons for the discount the user selected
List&lt;Coupon&gt; selectedCoupons = selectedDiscount.getAppliedCoupons();
PosInvoiceDetails posInvoiceDetails = new PosInvoiceDetails(posBasket, paymentInstrument, selectedCoupons);

2. Use the `PosManager` to create the invoice:

<pre>ManagerFactory.getInstance().getPosManager().createInvoice(posInvoiceDetails, new PowaTagCallback&lt;PosInvoice&gt;() {
	public void onSuccess(PosInvoice posInvoice) {
		// The PosInvoice contains information such as the POS terminal ID, basket items, total , discount and the coupons that were applied.
	}
	public void onError(PowaTagException exception) {
	}
});</pre>
	
<br />

The synchronous version of the <code>createInvoice</code> method is available but should not be used in the main thread to avoid performance issues

<code>PosInvoice posInvoice = ManagerFactory.getInstance().getPosManager().createInvoice(posInvoiceDetails);</code>
	
<br />  
This can also be done using RxJava:
	
<pre>RxManagerFactory.getInstance().getPosManager().createInvoice(posInvoiceDetails).subscribe(new Subscriber&lt;PosInvoice&gt;() {
	@Override
	public void onCompleted() {
	}

	@Override
	public void onError(Throwable e) {
	}

	@Override
	public void onNext(PosInvoice posInvoice) {
		// The PosInvoice contains information such as the POS terminal ID, basket items, discount, total the coupons that were applied.
	}
}); </pre>

<br/>  

## Paying the PosInvoice

Once you have created an invoice for the POS basket you can make a [Payment]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/payments/).

<br />