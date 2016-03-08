---
layout: page
title: Validators
permalink: /tag-mobile-sdks/0.9.8/ios/validators/
---

The SDK provides validators that can be used to ensure that information entered by the user is valid.<br />

There are three types of validators:

## Model Validators

These validators are used to ensure that all properties of a model are valid (e.g. validating PTKAddressDetails). 

They adopt the `PTKModelValidator` protocol which defines the `validate` method that returns a list of `PTKValidationFailure` objects, one for each property that has an error.

The following model validators are available:

### PTKAddressDetailsValidator

This is used to validate the `PTKAddressDetails` object. Since address formats differ by country the context is set during initialisation of the validator.<br />
There are two address formats currently supported, namely UK and China.

Property validators are used to: 

* <code>PTKAliasValidator</code> - to check the alias.
* <code>PTKNameValidator</code> - to check the first name, last name and county.
* <code>PTKPostcodeValidator</code> - to check that the post code is valid for the selected country.
* <code>PTKAddressLineValidator</code> - to check the State, City, County, Country, line1 and line2 are valid for the selected country.
* <code>PTKCNPostcodeValidator</code> - to check that a Chinese postcode is valid.
* <code>PTKUKPostcodeValidator</code> - to check thet a UK postcode is valid.

The following usage example shows how to use the `PTKAddressDetailsValidator`:<br />

##Tiago to provide snippet

<pre>// addressDetails has been populated with the values obtained from the user
AddressDetailsValidator addressDetailsValidator = new AddressDetailsValidator(CountryAwareAddressDetailContext.CHINA); //set the country to validate for
List&lt;ValidationFailure&gt; errors = addressDetailsValidator.validate(addressDetails);
if(errors != null){
    for (int s = 0; s < errors.size(); s++) {
		ValidationFailure validationFailure = errors.get(s);
		String property = validationFailure.getPropertyName();
		ValidationError errorCode = validationFailure.getErrorCode();
		// Display validation to user and obtain updated value
	}
} else {
	// No issues found while validating the address details
}
</pre>

<br />


### PTKProfileDetailsValidator
		
This is used to validate the `PTKProfileDetails` object. During instantiation the country code is set so that the country specific property validators are used.<br />

Property validators are used to: 

* <code>PTKEmailValidator</code> - to check the email address.
* <code>PTKMobileNumberValidator</code> - to check that the mobile number is valid for the selected country.
* <code>PTKPasscodeValidator</code> - to check that the passcode is valid.
* <code>PTKNameValidator</code> - to check the first and last name are in a valid format.<br />
* <code>PTKTitleValidator</code> - to check if the title is valid.<br />


The following usage example shows how to use the `PTKProfileDetailsValidator`:<br />

##Tiago to provide snippet

<pre>// The user's country is obtained and set in userCountry
ProfileDetailsValidator profileDetailsValidator = new ProfileDetailsValidator(userCountry.getAlpha2Code());
// Use the profileDetails obtain in an earlier step
List&lt;ValidationFailure&gt; errors = profileDetailsValidator.validate(profileDetails);
	if(!errors.isEmpty()){
	for (int s = 0; s < errors.size(); s++) {
		ValidationFailure validationFailure = errors.get(s);
		String property = validationFailure.getPropertyName();
		ValidationError errorCode = validationFailure.getErrorCode();
		// Display validation to user and obtain an updated value
	}
} else {
	// No issues found while validating the profile details
}
</pre>		
		
<br />
		
### PTKPaymentMethodDetailsValidator
				
This is used to validate the `PTKPaymentMethodDetails` object.<br />

Property validators are used to: 

* <code>CardHolderNameValidator</code> - to check the card holder name.
* <code>PTKCreditCardNumberValidator</code> - to check that the card number is valid.
* <code>PTKExpiryDateValidator</code> - to check that the expiry date is valid.
* <code>PTKIssueNumberValidator</code> - to check the issue number based on the card issuer rules.
* <code>PTKValidFromDateValidator</code> - to check the first and last name are in a valid format.
* <code>PTKNameValidator</code> - to check if the first and last names are less that 256 characters and in the correct format


The following usage example shows how to use the `PTKPaymentMethodDetailsValidator`:<br />

##Tiago to provide snippet

<pre>PaymentMethodDetailsValidator paymentMethodDetailsValidator = new PaymentMethodDetailsValidator();
List&lt;ValidationFailure&gt; errors = paymentMethodDetailsValidator.validate(paymentMethodDetails);
if(errors != null){
	for (int s = 0; s < errors.size(); s++) {
		ValidationFailure validationFailure = errors.get(s);
		String property = validationFailure.getPropertyName();
		ValidationError errorCode = validationFailure.getErrorCode();
		// Display validation to user and obtain an updated value
	}
} else {
	// No issues found while validating the payment details
}
</pre>
<br />
For more details each of these model validators please review the [reference]({{site.baseurl}}/tag-mobile-sdks/0.9.8/refdocs/IOS/protocol_p_t_k_model_validator-p.html){:target="_blank"} documentation
	
<br /> <br />

##  Property Validators

These validators are used to ensure that a single property is valid, often using multiple low level validators (e.g. validating the address `line1` property).  

They adopt the `PTKPropertyValidator` protocol which defines a method called `validateValue` which returns a single `PTKValidationError`.

The following property validators are available:<br />

* **PTKTextValidator** - checks if string is greater than the minimum and less than the maximum lengths, and if it matches a specified format.<br />
* **PTKIssueNumberValidator** - checks if the card issue number is 4 digits long and that only digits 0-9 are used. 
* **PTKAliasValidator** - checks if the alias is less than 256 characters long. 
* **PTKTitleValidator** - checks if title is not an empty string. 
* **PTKEmailValidator** - checks if an email address is in the correct format. 
* **PTKCardHolderNameValidator** - checks if card holder name is less than 256 characters and in the correct format.
* **PTKAddressLineValidator** - checks if an address line is less than 256 characters. 
* **PTKCvvValidator** - checks if CVV is correct length for the card issuer and that only digits 0-9 are used.
* **PTKNameValidator** - checks if the name is less than 256 characters and is in the correct format.
* **PTKPostcodeValidator** - abstract class that provides logic for country specific post code validators to check if the postcode conforms to a supplied format. 
* **PTKUkPostcodeValidator** - checks if a UK postcode is valid based on the UK Format
* **PTKCardDateValidator** - abstract class that provides logic for card date validators. checks if a YearMonth is between a specified minimum and maximum date range. 
* **PTKValidFromDateValidator** - checks if "Valid From" date is valid.
* **PTKExpiryDateValidator** - checks if expiry date is valid.
* **PTKMobileNumberValidator** - checks if a mobile number is valid for a specific country.  
* **PTKCreditCardNumberValidator** - checks if the card number is not null, is greater than the minimum and less than the maximum value and in the correct format based on the card issuer. 
* **PTKDecimalValueValidator** - abstract class providing logic for decimal values.  checks if greater than the minimum and less than the maximum value.
* **PTKDonationAmountValidator** - checks if donation amount is greater than zero.
* **PTKIntValueValidator** - abstract class providing logic for int values. checks if greater than the minimum and less than the maximum value. 

Here is an example of using one of the validators:<br />

##Tiago provide snippet

<pre>// Set the conditions for the validator
TextValidator textValidator = new TextValidator(isRequired, minLength, maxLegnth, format);
// Validate the the supplied card number 
ValidationFailure error = cardNumberValidator.validate(input.getCardNumber());
if(error != null){
	// handle error
} else {
	// No issues found while validating the card number
}
</pre>
	
For more details on each validator please review the [reference]({{site.baseurl}}/tag-mobile-sdks/0.9.8/refdocs/IOS/protocol_p_t_k_property_validator-p.html){:target="_blank"} documentation.
<br /> <br />

##  Validators
These are low level validators which are used to check aspects of a data type (e.g. NotNull, MinLength).

They implement the `Validator` interface which defines methods `isValid` and `getError`.

The following property validators are available:<br />

* **PTKFormatValidator** - checks if a input string matches the specified regular expression. 
* **PTKMaxLengthValidator** - Checks whether the input string is not longer than the maximum length.
* **PTKMinDecimalValueValidator** - Checks that the input value is not less than the minimum allowed decimal value. 
* **PTKMinIntValueValidator** -  Checks that the input value is not less than the minimum allowed int value. 
* **PTKMinLengthValidator** - Checks whether the input string is not shorter than the minimum length.
* **PTKLuhnValidator** - Checks a credit card number using the Luhn algorithm.
* **PTKMaxDecimalValueValidator** - Checks that an input value is not greater than the maximum allowed decimal value.
* **PTKMaxIntValueValidator** - Checks that an input value is not greater than the maximum allowed int value.
* **PTKNotEmptyValidator** - checks if the input is an empty string.
* **PTKNotNullValidator** - checks if input object is not null.


Here is an example of using one of the validators:<br />

##Tiago to provide snippet

<pre>MaxIntValueValidator maxIntValueValidator = new MaxIntValueValidator(1000);
// Validate the the supplied int number 
if(!maxIntValueValidator.isValid(input.getQuantity()){
	ValidationError error = maxIntValueValidator.getError();
	// handle error		
}
</pre>
<br /><br />	
For more details on the validators please review the [reference]({{site.baseurl}}/tag-mobile-sdks/0.9.8/refdocs/IOS/interface_p_t_k_validator.html){:target="_blank"} documentation.

<br /> <br />

