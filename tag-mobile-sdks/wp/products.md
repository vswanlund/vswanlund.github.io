---
layout: page
title: Products on Windows Phone
permalink: /tag-mobile-sdks/wp/products/
---

A product is an individual item for sale in a PowaTag store. Products can be physical goods which are shipped to your customers. You can also list digital download products or a service.

Variants are the individual styles of a product. If you have a product customers can choose in a different size, colour, or with other options then your product would have multiple variants specifying which combination of options are available. If a product has no options it will still have a single variant.

<br />

# Checking if a Product has Multiple Variants

1. Check to see whether the product has option choices (multiple variants), if it does not no selection is required:

    <pre>Product product = workflow.getProduct();
   if (product.HasOptionChoices()) {
     // Need to provide functionality to the user to select a variant
   } else {
     // The product only has a single variant
     ProductVariant selectedVariant = product.Variants[0];
   }</pre>

<br />

# Selecting a Product Variant

1. If the product has multiple variants, create a `ProductVariantPicker` and get the choices for the product. Each choice such as size or color has a number of options (such as Red and Blue options for color) and each option has a state indicating whether it is currently chosen or whether it can be chosen (some options may not be chosen in combination with others):

    <pre>ProductVariantPicker picker = new ProductVariantPicker(product);
    ReadOnlyObservableCollection&lt;ProductOptionChoice&gt; optionChoices = picker.OptionChoices;
   // Display the choices in some manner
   DisplayChoices(optionChoices);
   </pre>

2. To choose a specific option call the pickers `ChooseOption` method which will update the state of the options in the choices list based on the currently chosen options. The list is updated in-place so there is no need to get the list from the picker again:

    <pre>picker.ChooseOption(productOption);
   DisplayChoices(optionChoices);</pre>

3. If you want to know what the currently chosen options are, you can find this out quickly using the `ChosenOptions` method. Like the list of option choices, when changes are made this list is updated in-place:

	<pre>IReadOnlyList&lt;ProductOption&gt; chosenOptions = picker.ChosenOptions;</pre>

4. You can find out which variants match your currently choices:

    <pre>ReadOnlyObservableCollection&lt;ProductVariant&gt; variants = picker.Variants;</pre>

5. Once a desired option has been selected for each choice, the number of variants returned will either be `1` (the desired variant) or `0` (no variants available that match the current selection).

6. If you want to deselect an already chosen option, use the pickers `UnchooseOption` or `Reset` methods to remove one or all previously chosen option(s):

    <pre>// Unchoose a single option
   picker.UnchooseOption(productOption);
   DisplayChoices(optionChoices);

   // Unchoose all options
   picker.Reset();
   DisplayChoices(optionChoices);</pre>

<br />

# Checking if User Has Picked a Variant

1. To check if the user has picked a variant, check whether they have a picked an option for each choice:

    <pre>picker.IsOptionChosenForEveryChoice();</pre>

<br />

# Useful Product Methods

1. The following methods can be used to obtian useful product information:

	<pre>// Get the ID of the product.
	string productId = product.ProductId;
	
	// Get the ID of the merchant which this product is from.
	string merchantId = product.MerchantId;
	
    // Get The Global Trade Item Number (GTIN) that uniquely identifies the product globally, if it has one.
    string gtin = product.Gtin;

    // Get the product title
    string title = product.Title;
	
    // Get the product description.
    string productDescription = product.Description;
	
    // Get the brand associated with the product.
    string brand = product.Brand;

    // Get the product condition. e.g. new, refurbished, used or unknown
    ProductCondition condition = product.Condition;

    // Get a URL to view more information about the product. The URL is optional
    URI productLink = product.Link;

    // Get the list of categories this product is in.
    List&lt;string&gt; categories = product.Categories;</pre>
		
<br />


# Sample

To explore this topic in detail, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/wp/start/#importing-the-sample-app) app and review the <code>ProductPageViewModel</code> class.

<br />
		

# Adding a Product to a Basket

Add a variant to the users [Baskets]({{site.baseurl}}/tag-mobile-sdks/wp/baskets/) then check out to get shipping and taxes.
