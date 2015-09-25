---
layout: page
title: Products on Windows Phone
permalink: /tag-mobile-sdks/wp/products/
---

A product is an individual item for sale in a PowaTag store. Products can be physical goods which are shipped to your customers. You can also list digital download products or a service.

Variants are the individual styles of a product. If you have a product customers can choose in a different size, colour, or with other options then your product would have multiple variants specifying which combination of options are available. If a product has no options it will still have a single variant.

<br />

# Checking if a Product has Multiple Variants

1. Check to see whether the product has multiple variants, if it does not no selection is required:

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

2. To choose a specific option call the pickers `Choose` method which will update the state of the options in the choices list based on the currently chosen options. The list is updated in-place so there is no need to get the list from the picker again:

    <pre>picker.Choose(option);
   DisplayChoices(optionChoices);</pre>

3. You can find out which variants match your currently choices:

    <pre>ReadOnlyObservableCollection&lt;ProductVariant&gt; variants = picker.Variants;</pre>

4. Once a desired option has been selected for each choice, the number of variants returned will either be `1` (the desired variant) or `0` (no variants available that match the current selection).

5. If you want to deselect an already chosen option, use the pickers `Unchoose` or `Clear` methods to remove one or all previously chosen option(s):

    <pre>// Unchoose a single option
   picker.Unchoose(option);
   DisplayChoices(optionChoices);

   // Unchoose all options
   picker.Clear();
   DisplayChoices(optionChoices);</pre>

<br />

# Checking if User Has Picked a Variant

1. To check if the user has picked a variant, check whether they have a picked an option for each choice:

    picker.IsOptionChosenForEveryChoice();

<br />

**Currently Chosen Options**

If you want to know what the currently chosen options are, you can find this out quickly using the `ChosenOptions` property. Like the list of option choices, when changes are made this list is updated in-place:

    IReadOnlyList<ProductOption> chosenOptions = picker.ChosenOptions;

<br />

# Adding a Product to a Basket

Add a variant to the users [Baskets]({{site.baseurl}}/tag-mobile-sdks/wp/baskets/) then check out to get shipping and taxes.
