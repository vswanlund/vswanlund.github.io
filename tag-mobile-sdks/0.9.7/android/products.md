---
layout: page
title: Products on Android
permalink: /tag-mobile-sdks/0.9.7/android/products/
---

A product is an individual item for sale in a PowaTag store. Products can be physical goods which are shipped to your customers. You can also list digital download products or a service.

Variants are the individual styles of a product. If you have a product customers can choose in a different size, colour, or with other options then your product would have multiple variants specifying which combination of options are available. If a product has no options it will still have a single variant.

<br />

# Checking if a Product has Multiple Variants

1. Check to see whether the product has option choices (multiple variants), if it does not no selection is required:

    <pre>Product product = workflow.getProduct();
   if (product.hasOptionChoices()) {
     // Need to provide functionality to the user to select a variant
   } else {
     // The product only has a single variant
     ProductVariant selectedVariant = product.getVariants().get(0);
   }</pre>

<br />

# Selecting a Product Variant

1. If the product has multiple variants, create a `ProductVariantPicker` and get the choices for the product. Each choice such as size or color has a number of options (such as Red and Blue options for color) and each option has a state indicating whether it is currently chosen or whether it can be chosen (some options may not be chosen in combination with others):

	<pre>ProductVariantPicker picker = new ProductVariantPicker(product);
	List&lt;ProductOptionChoice&gt; optionChoices = picker.getOptionChoices();
	// Display the choices in some manner
	displayChoices(optionChoices);</pre>

2. To choose a specific option call the pickers `chooseOption` method which will update the state of the options in the choices list based on the currently chosen options. The list is updated in-place so there is no need to get the list from the picker again:

	<pre>picker.chooseOption(productOption);
	displayChoices(optionChoices);</pre>

3. If you want to know what the currently chosen options are, you can find this out quickly using the `getChosenOptions` method. Like the list of option choices, when changes are made this list is updated in-place:

	<pre>List<ProductOption> chosenOptions = picker.getChosenOptions();</pre>

4. You can find out which variants match the current option choices:

    <pre>List&lt;ProductVariant&gt; variants = picker.getVariants();</pre>

5. Once a desired option has been selected for each choice, the number of variants returned will either be `1` (the desired variant) or `0` (no variants available that match the current selection).

6. If you want to deselect an already chosen option, use the pickers `unchooseOption` or `reset` methods to remove one or all previously chosen option(s):

    <pre>// Unchoose a single option
	picker.unchooseOption(productOption);
	displayChoices(optionChoices);

   // Unchoose all options
	picker.reset();
	displayChoices(optionChoices);</pre>

<br />

# Checking if User Has Picked a Variant

1. To check if the user has picked a variant, check whether they have picked an option for each choice:

    <pre>picker.isOptionChosenForEveryChoice();</pre>

<br />

# Saving and Restoring the Picker State

1. To save the picker state when your Activity is destroyed, using the `saveInstanceState` picker method:

    <pre>@Override
   public void onSaveInstanceState(Bundle outState) {
     super.onSaveInstanceState(outState);
     outState.putParcelable("picker", picker.saveInstanceState());
    }
   </pre>

2. You can restore the picker state using the `restoreInstanceState` method:

    <pre>@Override
   public void onCreate(Bundle savedInstanceState) {
     super.onCreate(savedInstanceState);
     picker = new ProductVariantPicker(product);
   }
   @Override
   public void onRestoreInstanceState(Bundle savedInstanceState) {
     super.onRestoreInstanceState(savedInstanceState);
     picker.restoreInstanceState(savedInstanceState.getParcelable("picker"));
   }</pre>

3. Or when instantiating your picker if you know the saved state is not null:

    <pre>@Override
   public void onCreate(Bundle savedInstanceState) {
     super.onCreate(savedInstanceState);
     if (savedInstanceState != null) {
       picker = new ProductVariantPicker(product, savedInstanceState.getParcelable("picker"));
     } else {
       picker = new ProductVariantPicker(product);
     }
   }</pre>

<br />

# Useful Product Methods

1. The following methods can be used to obtian useful product information:

	<pre>// Get the ID of the product.
	String productId = product.getProductId();

	// Get the ID of the merchant which this product is from.
	String merchantId = product.getMerchantId();

    // Get The Global Trade Item Number (GTIN) that uniquely identifies the product globally, if it has one.
    String gtin = product.getGtin();

    // Get the product title
    String title = product.getTitle();

    // Get the product description.
    String productDescription = product.getDescription();

    // Get the brand associated with the product.
    String brand = product.getBrand();

    // Get the product condition. e.g. new, refurbished, used or unknown
    ProductCondition condition = product.getCondition();

    // Get a URL to view more information about the product. The URL is optional
    URI productLink = product.getLink();

    // Get the list of categories this product is in.
    List&lt;String&gt; categories = product.getCategories();</pre>

<br />


# Sample

To explore this topic in detail, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/0.9.7/android/start/#importing-the-sample-app) app and review the <code>ProductDetailsActivity</code> class.

<br />


# Adding a Product to a Basket

Add a variant to the users [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.7/android/baskets/) then check out to to get shipping and taxes.


