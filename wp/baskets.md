---
layout: page
title: Baskets on Windows Phone
permalink: /tag-mobile-sdks/wp/baskets/
---

Baskets are a collection of a product variants (such as a small, black T Shirt). There are two different types of baskets: TemporaryBaskets and PersistentBaskets. The contents of a PersistentBasket are managed by the user and changes to the baskets are saved with the user profile, whereas the contents of a TemporaryBasket cannot be modified by the user and the basket is not saved with the user profile.

Manipulation of PersistentBaskets, such as adding or removing products and changing quantities is performed using the `BasketsManager`.

A TemporaryBasket can only be retrieved from a TemporaryBasketWorkflow and cannot be created or manipulated by the user -- the only action you can perform with a TemporaryBasket is to create an invoice for the basket. After 60 minutes the tag associated with the basket will expire.

<br />

# Checking if a Basket is a TemporaryBasket or PersistentBasket

1. Check the `isTemporary` property of the basket:

    <pre>if (basket.isTemporary()) {
     // Preset basket
     TemporaryBasket basket = (TemporaryBasket) basket;
   } else {
     // User basket
     PersistentBasket basket = (PersistentBasket) basket;
   }</pre>

<br />

# Adding a Product Variant to a Basket

1. Add a product variant to the basket for the merchant:

    <pre>ProductVariant variant = product.Variants[0];
   BasketsManager bm = BasketsManager.GetInstance();
   bm.AddVariant(workflow.Merchant, variant);</pre>

2. Retrieve updated pricing information using the BasketsManager:

    <pre>BasketsManager bm = BasketsManager.GetInstance();
   // Basket now contains pricing information
   Basket basket = await bm.UpdateBasketAsync(basket);</pre>

3. The updated information is also available in the users Baskets:

    <pre>Baskets baskets = BasketsManager.GetInstance().GetCurrentBaskets();
   // Same information as received in the BasketManager callback
   Basket basket = baskets.GetBasket(workflow.Merchant);</pre>

<br />

# Removing a Product Variant from a Basket

1. You can remove a single quantity of a variant (this will return true if the quantity of the variant was decreased by 1), if the remaining quantity is 0 the item will be removed from the basket:

    <pre>boolean singleQuantityRemoved = bm.RemoveVariant(workflow.Merchant, variant);</pre>

2. Or you can remove a specific quantity (in this the amount the quantity was decreased by will be returned):

    <pre>int quantityRemoved = bm.RemoveVariant(workflow.Merchant, variant, 2);</pre>

<br />

# Changing the Quantity of a Product Variant

1. Set the quantity of a variant (this will override any existing quantity, if you set the quantity to 0 the basket item for that variant will be removed):

    <pre>bm.SetVariantQuantity(workflow.Merchant, variant, 3);</pre>

2. You can use this to remove a variant from a basket entirely, regardless of the current quantity by setting the quantity to 0:

    <pre>bm.SetVariantQuantity(workflow.Merchant, variant, 0);</pre>

<br />

# Basket Items

1. A basket is made up of multiple line items, one for each unique product variant. An item records the quantity of each variant (the quantity will always be >= 1):

    <pre>foreach (BasketItem item in basket.Items) 
   {
      ProductVariant variant = item.Variant
      int quantity = item.Quantity;
   }</pre>

<br />

# Creating an Invoice for a Basket

Before creating an invoice you need to ensure the users [Profile]({{site.baseurl}}/tag-mobile-sdks/wp/profile/) has all required information for the merchant.

1. Select a PaymentInstrument from the Profile that is accepted by the Merchant:

    <pre>List&lt;PaymentInstrument&gt; acceptedPaymentInstruments = Profile.CurrentProfile.GetAcceptedPaymentInstruments(merchant);
   PaymentInstrument paymentInstrument = acceptedPaymentInstruments[0];</pre>

2. Select an Address to use for the shipping address from the Profile:

    <pre>Address shippingAddress = Profile.CurrentProfile.Addresses[0];</pre>

3. Select a ShippingOption to use for delivery from the Merchant:

    <pre>ShippingOption shippingOption = basket.Merchant.ShippingOptions[0];</pre>

4. Use the BasketsManager to get the cost for a Basket contents delivered by a particular shipping option:

    <pre>BasketsManager bm = BasketsManager.GetInstance();
   PaymentInvoiceDetails paymentInvoiceDetails = new PaymentInvoiceDetails(paymentInstrument, shippingAddress, shippingOption);
   PaymentInvoice invoice = await bm.CreateInvoiceAsync(basket, paymentInvoiceDetails);
   Cost cost = invoice.Cost;</pre>

<br />

# Paying for a Payment Invoice

Once you have created an invoice for a basket you can make a [Payment]({{site.baseurl}}/tag-mobile-sdks/wp/payments/) for that invoice.

<br />

# Saving a Basket to the Server

1. To make Basket information available to other devices or between logins you need to update the Basket on the server using the BasketsManager:

    <pre>BasketsManager bm = BasketsManager.GetInstance();
   Basket basket = await bm.UpdateBasketAsync(merchant);</pre>

<br />

**Manually Synchronizing Baskets**

Baskets tracks operations in the SDK to ensure the users baskets are up to date. However, if you wish to manually synchronize the baskets, you can do so by calling `BasketsManager.GetAllBasketsAsync`.
