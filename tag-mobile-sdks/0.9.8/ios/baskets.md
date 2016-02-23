---
layout: page
title: Baskets on iOS
permalink: /tag-mobile-sdks/0.9.7/ios/baskets/
---

Baskets are a collection of a product variants (such as a small, black T Shirt). There are two different types of baskets: TemporaryBaskets and PersistentBaskets. The contents of a PersistentBasket are managed by the user and changes to the baskets are saved with the user profile, whereas the contents of a TemporaryBasket cannot be modified by the user and the basket is not saved with the user profile.

Manipulation of PersistentBaskets, such as adding or removing products and changing quantities is performed locally using the `BasketsManager`.

A TemporaryBasket can only be retrieved from a TemporaryBasketWorkflow and cannot be created or manipulated by the user -- the only action you can perform with a TemporaryBasket is to create an invoice for the basket. After 60 minutes the tag associated with the basket will expire.

<br />

# Creating a Basket

1. Create a <code>TemporaryBasket</code>:

	<pre>- (void)myMethod
	{
		PTKTemporaryBasket *tempBasket = [PTKTemporaryBasket temporarybasketWithId:@"basketId"
			items:@[item1, item2 ...]
			merchant:merchantObject];
	}</pre>

2. Creating a <code>PersistentBasket</code>:

	<pre>- (void)myMethod
	{
		PTKPersistentBasket *persistentBasket = [PTKPersistentBasket persistentBasketWithId:@"basketId"
			profileId:@"profileId"
			items:@[item1, item2 ...]
			merchant:merchantObject];
	}

<br />

# Adding a Product Variant to a Basket

1. Add a product variant to the basket for the merchant:

	<pre>PTKProductVariant *variant = [workflow.product.variants firstObject];
	PTKBasketsManager *bm = [PTKBasketsManager sharedManager];
	[bm addVariantWithMerchant:workflow.merchant productVariant:variant];</pre>

<br />

# Removing a Product Variant from a Basket

1. You can remove a single quantity of a variant (this will return true if the quantity of the variant was decreased by 1), if the remaining quantity is 0 the item will be removed from the basket:

    <pre>boolean singleQuantityRemoved = [bm removeVariantWithMerchant:workflow.merchant variant:variant];</pre>

2. Or you can remove a specific quantity (in this the amount the quantity was decreased by will be returned):

    <pre>int quantityRemoved = [bm removeVariantWithMerchant:workflow.merchant, variant:variant quantity: 2];</pre>

<br />

# Changing the Quantity of a Product Variant

1. Set the quantity of a variant (this will override any existing quantity, if you set the quantity to 0 the basket item for that variant will be removed):

    <pre>[bm setVariantQuantityWithMerchant:workflow.merchant variant:variant quantity:3];</pre>

2. You can use this to remove a variant from a basket entirely, regardless of the current quantity by setting the quantity to 0 (causing the basket item for the variant to be removed from the basket):

    <pre>[bm setVariantQuantityWithMerchant:workflow.merchant variant:variant quantity:0];</pre>

<br />

# Basket Items

1. A basket is made up of multiple line items, one for each unique product variant. An item records the quantity of each variant (the quantity will always be >= 1):

	<pre>for (PTKBasketItem *item in basket.items) {
		PTKProductVariant *variant = item.variant;
		int quantity = item.quantity;
	}</pre>

<br />

# Creating an Invoice for a Basket

Before creating an invoice you need to ensure the users [Profile]({{site.baseurl}}/tag-mobile-sdks/0.9.7/ios/profile/) has all required information for the merchant.

1. Select a PaymentInstrument from the Profile that is accepted by the Merchant:

	<pre>NSArray *acceptedPaymentInstruments = [[PTKProfile currentProfile] acceptedPaymentInstrumentsForMerchant:merchant];
	PTKPaymentInstrument *paymentInstrument = acceptedPaymentInstruments[0];</pre>

2. Select an AddressAlias to use for the shipping address from the Profile:

    <pre>PTKAddress *shippingAddress = [PTKProfileManager sharedManager].currentProfile.addresses[0];</pre>

3. Select a ShippingOption to use for delivery from the Merchant:

    <pre>PTKShippingOption *shippingOption = basket.merchant.shippingOptions[0];</pre>

4. Create payment invoice details object with all necessary data:
	<pre>PTKPaymentInvoiceDetails *paymentInvoiceDetails = [PTKPaymentInvoiceDetails
	paymentInvoiceDetailsWithPaymentInstrument:paymentInstrument shippingAddress:shippingAddress shippingOption:shippingOption]</pre>

5. Use the BasketsManager to get the cost for a Basket contents delivered by a particular shipping option:

	<pre>PTKBasketsManager *bm = [PTKBasketsManager sharedManager];
	[bm createInvoiceWithBasket:basket paymentInvoiceDetails:paymentInvoiceDetails completion:^(PTKPaymentInvoice *invoice, NSError *error) {
		if (invoice) {
			PTKCost *cost = invoice.cost;
		}
	}];</pre>

<br />

# Paying for a Payment Invoice

1. Once you have created an invoice for a basket you can make a [Payment]({{site.baseurl}}/tag-mobile-sdks/0.9.7/ios/payments/) for that invoice.

	<pre>PTKPaymentDetails *paymentDetails = [PTKPaymentDetails paymentDetailsWithCvv:@"123"];
	PTKPaymentManager *paymentManager = [PTKPaymentManager sharedManager];
	[paymentManager payForInvoice:invoice
		paymentDetails:paymentDetails
			completion:^(PTKPayment *__nullable payment, NSError *__nullable  error) {
		if (!error)
			// success
		} else {
			// error
		}
	}];</pre>

<br />

# Saving a Basket to the Server

1. To make Basket information available to other devices or between logins you need to update the Basket on the server using the BasketsManager:

	<pre>PTKBasketsManager *bm = [PTKBasketsManager sharedManager];
	[bm updateBasketWithMerchant:merchant completion:^(PTKBasket *basket, NSError *error) {
		// Basket is now accessible from other devices
	}];</pre>
