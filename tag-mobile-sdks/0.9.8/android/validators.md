---
layout: page
title: Validators
permalink: /tag-mobile-sdks/0.9.8/android/validators/
---

The SDK provides validators that can be used to ensure that the information entered by the user is valid.

There are three types of validators available for use:

* Low level validators - used for validating a aspects of a data type (e.g. not null, too long)
* Property validators - validate a property by using multiple low level validators and returning a single error (e.g. address line1) 
* Model validators - validates a model by using multiple property validators and returns a list of all properties that have errors(e.g. Address) 

The validators can be found in the package <code>com.powatag.android.sdk.validators</code>


* [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/baskets/) - PaymentInvoice
* [Campaigns]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/campaigns/) - DonationInvoice

<br />

# Paying for an Invoice using CVV

1. Validate the address details

	Use <code>AddressDetailsValidator</code> to verify that all address details have been entered correctly.
	This validator uses property validators to validate each property of <code>AddressDetails</code>:

	* <code>AliasValidator</code> - to check the alias.
	* <code>NameValidator</code> - to check the first name, last name and county.
	* <code>UkPostcodeValidator</code> - to check the post code.
	* <code>AddressLineValidator</code> - to check all remaining address lines for checking all address lines.


	For more information on each of these property validators please see the reference documentation included as part of the SDK.

	<pre>AddressDetailsValidator addressDetailsValidator = new AddressDetailsValidator();
	List&lt;ValidationFailure&gt; errors = addressDetailsValidator.validate(address);
	if(errors != null){
		for (int s = 0; s < errors.size(); s++) {
			ValidationFailure validationFailure = errors.get(s);
			String property = validationFailure.getPropertyName();
			ValidationError errorCode = validationFailure.getErrorCode();
			// Display validation to user and obtain updated value
		}
	} else {
		// No issues found while validating the address details
	}</pre>







