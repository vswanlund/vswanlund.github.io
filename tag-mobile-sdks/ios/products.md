---
layout: page
title: Products on iOS
permalink: /tag-mobile-sdks/ios/products/
---

A product is an individual item for sale in a PowaTag store. Products can be physical goods which are shipped to your customers. You can also list digital download products or a service.

Variants are the individual styles of a product. If you have a product customers can choose in a different size, colour, or with other options then your product would have multiple variants specifying which combination of options are available. If a product has no options it will still have a single variant.

<br />

# Checking if a Product has Multiple Variants

1. Check to see whether the product has option choices (multiple variants), if it does not no selection is required:

    <pre>PTKProduct *product = workflow.product;
   if ([product hasOptionChoices]) {
     // Need to provide functionality to the user to select a variant
   } else {
     // The product only has a single variant
     PTKProductVariant *selectedVariant = [product.variants objectAtIndex:0];
   }</pre>

<br />

# Selecting a Product Variant

1. If the product has multiple variants, create a `PTKProductVariantPicker` and get the choices for the product. Each choice such as size or color has a number of options (such as Red and Blue options for color) and each option has a state indicating whether it is currently chosen or whether it can be chosen (some options may not be chosen in combination with others):

    <pre>PTKProductVariantPicker *picker = [PTKProductVariantPicker productVariantPickerWithProduct:product];
   NSArray *optionChoices = picker.optionChoices;
   // Display the choices in some manner
   [self displayChoices:optionChoices];</pre>

2. To choose a specific option call the pickers `chooseOption` which will update the state of the options in the choices list based on the currently chosen options. The list is updated in-place so there is no need to get the list from the picker again:

    <pre>NSArray *chosenOptions = picker.chosenOptions;</pre>

3. If you want to know what the currently chosen options are, you can find this out quickly using the `getChosenOptions` method. Like the list of option choices, when changes are made this list is updated in-place: 
   
	<b> &lt;CODE SNIPPET&gt;</b>
   
4. You can find out which variants match your currently choices using the `variants` method of the picker:

    <pre>NSArray *variants = [picker variants];</pre>

5. Once a desired option has been selected for each choice, the number of variants returned will either be `1` (the desired variant) or `0` (no variants available that match the current selection).

6. If you want to deselect an already chosen option, use the pickers `unchooseOption` or `reset` methods to remove one or all previously chosen option(s):

    <pre>// Unchoose a single option
   [picker unchooseOption:option];
   [self displayChoices:optionChoices];

   // Unchoose all options
   [picker reset];
   [self displayChoices:optionChoices];</pre>


<br />

# Checking if User Has Picked a Variant

1. To check if the user has picked a variant, check whether they have a picked an option for each choice:

    [picker isOptionChosenForEveryChoice];

<br />

# Saving and Restoring the Picker State

1. To save the picker state when your Activity is rotated, using the `saveInstanceState` picker method:
<b> &lt;CODE SNIPPET&gt;</b>
    <pre>@Override
   public void onSaveInstanceState(Bundle outState) {
     super.onSaveInstanceState(outState);
     outState.putParcelable("picker", picker.saveInstanceState());
    }
   </pre>

2. You can restore the picker state using the `restoreInstanceState` method:
<b> &lt;CODE SNIPPET&gt;</b>
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
<b> &lt;CODE SNIPPET&gt;</b>
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
<b> &lt;CODE SNIPPETS&gt;</b>
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

To explore this topic in detail, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/ios/start/#importing-the-sample-app) app and review the <code>ProductController</code> class.

<br />

# Adding a Product to a Basket

Add a variant to the users [Baskets]({{site.baseurl}}/tag-mobile-sdks/ios/baskets/) then check out to get shipping and taxes.
