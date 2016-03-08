---
layout: page
title: Baskets on Android
permalink: /tag-mobile-sdks/0.9.8/android/baskets/
---

Baskets are a collection of product variants (such as small, black T Shirt). There are two different types of baskets: TemporaryBaskets and PersistentBaskets. The contents of a PersistentBasket are managed by the user and changes to the baskets are saved with the user profile, whereas the contents of a TemporaryBasket cannot be modified by the user and the basket is not saved with the user profile.

Manipulation of PersistentBaskets, such as adding or removing products and changing quantities is performed locally using the `BasketsManager`.

A TemporaryBasket can only be retrieved from a TemporaryBasketWorkflow and cannot be created or manipulated by the user -- the only action you can perform with a TemporaryBasket is to create an invoice for the basket. After 60 minutes the tag associated with the basket will expire.

<br />

# Checking if a Basket is a TemporaryBasket or PersistentBasket

1. Check the `isTemporary` property of the basket:

    <pre>if (basket.isTemporary()) {
     // Pre-set basket
     TemporaryBasket basket = (TemporaryBasket) basket;
   } else {
     // User basket
     PersistentBasket basket = (PersistentBasket) basket;
   }</pre>

<br />

# Obtaining the Baskets for a User

1. Get the list of baskets for the current user using the `BasketsManager`:

	<pre>BasketsManager basketsManager = ManagerFactory.getInstance().getBasketsManager();
	Baskets baskets = basketsManager.getCurrentBaskets();</pre>
	
	For those using RxJava, the RxManagerFactory is used to obtain the instance:
	
	<pre>RxBasketsManager basketsManager = RxManagerFactory.getInstance().getBasketsManager();
	Baskets baskets = basketsManager.getCurrentBaskets();</pre>	

2. Get the user's basket for a specific merchant:

	<pre>PersistentBasket basket = baskets.getBasket(merchant);</pre>

<br/>

# Adding a Product Variant to a Basket

1. Add a product variant to the basket for the merchant:

    <pre>ProductVariant variant = workflow.getProduct().getVariants().get(0);
	basketsManager.addVariant(workflow.getMerchant(), variant);</pre>

2. Or you can add a specific quantity of the product variant to the basket:

    <pre>basketsManager.addVariant(workflow.getMerchant(), variant, 2);</pre>

<br />

# Removing a Product Variant from a Basket

1. You can remove a single quantity of a variant (this will return true if the quantity of the variant was decreased by 1), if the remaining quantity is 0 the item will be removed from the basket:

    <pre>boolean singleQuantityRemoved = basketsManager.removeVariant(merchant, variant);</pre>

2. Or you can remove a specific quantity (in this the amount the quantity was decreased by will be returned):

    <pre>int quantityRemoved = basketsManager.removeVariant(merchant, variant, 2);</pre>

<br />

# Changing the Quantity of a Product Variant

1. Set the quantity of a variant (this will override any existing quantity, if you set the quantity to 0 the basket item for that variant will be removed):

    <pre>basketsManager.setVariantQuantity(merchant, variant, 3);</pre>

2. You can use this to remove a variant from a basket entirely, regardless of the current quantity by setting the quantity to 0 (causing the basket item for the variant to be removed from the basket):

    <pre>basketsManager.setVariantQuantity(merchant, variant, 0);</pre>

<br />

# Basket Items

1. A basket is made up of multiple line items, one for each unique product variant. An item records the quantity of each variant (the quantity will always be >= 1):

    <pre>for (BasketItem item : basket.getItems()) {
      ProductVariant variant = item.getVariant();
      int quantity = item.getQuantity();
   }</pre>

<br />

# Creating an Invoice for a Basket

Before creating an invoice you need to ensure the users [Profile]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/profile/) has all required information for the merchant.

1. Select a PaymentInstrument from the Profile that is accepted by the Merchant:

    <pre>ProfileManager profileManager = ManagerFactory.getInstance().getProfileManager();
	List<PaymentMethodAlias> acceptedPaymentInstruments = profileManager.getAcceptedPaymentInstruments(merchant);
    PaymentInstrument paymentInstrument = acceptedPaymentInstruments.get(0);</pre>

2. Select an Address to use for the shipping address from the Profile:

    <pre>Address shippingAddress = profileManager.getCurrentProfile().getAddresses().get(0);</pre>

3. Select a ShippingOption to use for delivery from the Merchant:

    <pre>ShippingOption shippingOption = basket.getMerchant().getShippingOptions.get(0);</pre>

4. Create a `PaymentInvoiceDetails` to provide payment instrument, shipping address and shipping options for creating an invoice:

	<pre> PaymentInvoiceDetails paymentInvoiceDetails = new PaymentInvoiceDetails(paymentInstrument, shippingAddress, shippingOption);

5. Use the BasketsManager to get the cost for a Basket contents delivered by a particular shipping option:

    <pre>basketsManager.createInvoice(basket, paymentInvoiceDetails, new PowaTagCallback&lt;PaymentInvoice&gt;() {
		public void onSuccess(PaymentInvoice invoice) {
			Cost cost = invoice.getCost();
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>
<br />

	This can also be done using RxJava:
	
	<pre>RxBasketsManager bm = RxManagerFactory.getInstance().getBasketsManager();
	bm.createInvoice(basket, paymentInvoiceDetails).subscribe(new Subscriber<PaymentInvoice>() {
	@Override
	public void onCompleted() {
		
	}

	@Override
	public void onError(Throwable e) {

	}

	@Override
	public void onNext(PaymentInvoice paymentInvoice) {
		Cost cost = paymentInvoice.getCost();
	}
	});</pre>
<br />

# Paying for a Payment Invoice

Once you have created an invoice for a basket you can make a [Payment]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/payments/) for that invoice.

<br />

# Saving a Basket to the Server

1. To make Basket information available to other devices or between logins you need to update the Basket on the server using the BasketsManager:

    <pre>basketsManager.updateBasket(merchant, new PowaTagCallback&lt;Basket&gt;() {
		public void onSuccess(Basket basket) {
		// Basket is now accessible from other devices
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>

	The <code>BasketManager</code> also provides a synchronous <code>updateBasket</code> method which should only be used outside of the main thread to avoid performance bottlenecks.

	<pre>Basket basket = bm.updateBasket(merchant);</pre>
	
	
	This can also be done using RxJava:
	
	<pre>basketManager.updateBasket(basket).subscribe(new Subscriber<Basket>() {
	@Override
	public void onCompleted() {
		// Basket is now accessible from other devices
	}

	@Override
	public void onError(Throwable e) {

	}

	@Override
	public void onNext(PaymentInvoice paymentInvoice) {
	}
	});</pre>
<br />

	

