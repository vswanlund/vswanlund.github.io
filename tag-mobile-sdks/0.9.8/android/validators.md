---
layout: page
title: Validators
permalink: /tag-mobile-sdks/0.9.8/android/validators/
---

The SDK provides validators that can be used to ensure that information entered by the user is valid.<br />
All validators can be found in the package <code>com.powatag.android.sdk.validators</code>

There are three types of validators:

## Model Validators

These validators are used to ensure that all properties of a model are valid (e.g. validating AddressDetails). 

They implement the `ModelValidator` interface which defines the `validate` method that returns a list of `ValidationFailure` objects, one for each property that has an error.

The following model validators are available:

### AddressDetailsValidator

This is used to validate the `AddressDetails` object. Since address formats differ by country the context is set during initialisation of the validator through the use of the `CountryAwareAddressDetailContext` which will provide country specific property validators.<br />
There are two address formats currently supported, namely UK and China.

Property validators are used to: 

* <code>AliasValidator</code> - to check the alias.
* <code>NameValidator</code> - to check the first name, last name and county.
* <code>PostcodeValidator</code> - to check that the post code is valid for the selected country.
* <code>CountryValidator</code> - to check the country.
* <code>AddressLineValidator</code> - to check the State, City, line1 and line2 are valid for the selected country.
* <code>CountyValidator</code> - to check the county is valid for the selected country.
* <code>NameValidator</code> - to check the first and last name are in a valid format.

The following usage example shows how to use the `AddressDetailsValidator`:<br />

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
	}</pre>

<br />


### ProfileDetailsValidator
		
This is used to validate the `ProfileDetails` object. During instantiation the country code is set so that the country specific property validators are used.<br />

Property validators are used to: 

* <code>EmailValidator</code> - to check the email address.
* <code>MobileNumberValidator</code> - to check that the mobile number is valid for the selected country.
* <code>PasscodeValidator</code> - to check that the passcode is valid.
* <code>NameValidator</code> - to check the first and last name are in a valid format.<br />

The following usage example shows how to use the `ProfileDetailsValidator`:<br />

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
	}</pre>		
		
<br />
		
### PaymentMethodDetailsValidator
				
This is used to validate the `PaymentMethodDetails` object.<br />

Property validators are used to: 

* <code>CardHolderNameValidator</code> - to check the card holder name.
* <code>CardNumberValidator</code> - to check that the card number is valid.
* <code>ExpiryDateValidator</code> - to check that the expiry date is valid.
* <code>IssueNumberValidator</code> - to check the issue number based on the card issuer rules.
* <code>ValidFromDateValidator</code> - to check the first and last name are in a valid format.

The following usage example shows how to use the `PaymentMethodDetailsValidator`:<br />

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
	}</pre>
	
	
<br /> <br />

##  Property Validators

These validators are used to ensure that a single property is valid, often using multiple low level validators (e.g. validating the address `line1` property).  

They implement the `PropertyValidator` interface which defines a method called `validate` which returns a single `ValidationError`.

The following property validators are available:<br />

* **TextValidator** - checks if string is greater than the minimum and less than the maximum lengths, and if it matches a specified format.<br />
* **IssueNumberValidator** - checks if the card issue number is 4 digits long and that only digits 0-9 are used. 
* **AliasValidator** - checks if the alias is less than 256 characters long. 
* **TitleValidator** - checks if title is not an empty string. 
* **EmailValidator** - checks if an email address is in the correct format. 
* **CardHolderNameValidator** - checks if card holder name is less than 256 characters and in the correct format.
* **AddressLineValidator** - checks if an address line is less than 256 characters. 
* **CountyValidator** - checks if county is less than 256 characters. 
* **CvvValidator** - checks if CVV is correct length for the card issuer and that only digits 0-9 are used.
* **NameValidator** - checks if the name is less than 256 characters and is in the correct format.
* **CountryValidator** - checks if country is 2 characters in length. 
* **PostcodeValidator** - abstract class that provides logic for country specific post code validators to check if the postcode conforms to a supplied format. 
* **UkPostcodeValidator** - checks if a UK postcode is valid based on the UK Format
* **ChinaPostcodeValidator** - checks if a UK postcode is valid based on the Chinese Format
* **CardDateValidator** - abstract class that provides logic for card date validators. checks if a YearMonth is between a specified minimum and maximum date range. 
* **ValidFromDateValidator** - checks if "Valid From" date is valid.
* **ExpiryDateValidator** - checks if expiry date is valid.
* **MobileNumberValidator** - checks if a mobile number is valid for a specific country.  
* **PasscodeValidator** - checks if the passcode is 6 digits long. 
* **CardNumberValidator** - checks if the card number is not null, is greater than the minimum and less than the maximum value and in the correct format based on the card issuer. 
* **DecimalValueValidator** - abstract class providing logic for decimal values.  checks if greater than the minimum and less than the maximum value.
* **DonationAmountValidator** - checks if donation amount is greater than zero.
* **IntValueValidator - abstract class providing logic for int values. checks if greater than the minimum and less than the maximum value. 

Here is an example of using one of the validators:<br />

	<pre>// Set the conditions for the validator
	TextValidator textValidator = new TextValidator(isRequired, minLength, maxLegnth, format);
	// Validate the the supplied card number 
	ValidationFailure error = cardNumberValidator.validate(input.getCardNumber());
	if(error != null){
		// handle error
	} else {
		// No issues found while validating the card number
	}</pre>
	
For more details on each validator please review the reference documentation.
<br /> <br />

##  Validators
These are low level validators which are used to check aspects of a data type (e.g. NotNull, MinLength).

They implement the `Validator` interface which defines methods `isValid` and `getError`.

The following property validators are available:<br />

* **FormatValidator** - checks if a input string matches the specified regular expression. 
* **MaxLengthValidator** - Checks whether the input string is not longer than the maximum length.
* **MinDecimalValueValidator** - Checks that the input value is not less than the minimum allowed decimal value. 
* **MinIntValueValidator** -  Checks that the input value is not less than the minimum allowed int value. 
* **MinLengthValidator** - Checks whether the input string is not shorter than the minimum length.
* **LuhnValidator** - Checks a credit card number using the Luhn algorithm.
* **MaxDecimalValueValidator** - Checks that an input value is not greater than the maximum allowed decimal value.
* **MaxIntValueValidator** - Checks that an input value is not greater than the maximum allowed int value.
* **NotEmptyValidator** - checks if the input is an empty string.
* **NotNullValidator** - checks if input object is not null.


Here is an example of using one of the validators:<br />

	<pre>MaxIntValueValidator maxIntValueValidator = new MaxIntValueValidator(1000);
	// Validate the the supplied int number 
	if(!maxIntValueValidator.isValid(input.getQuantity()){
		ValidationError error = maxIntValueValidator.getError();
		// handle error		
	}</pre>
	
For more details on each validator please review the reference documentation.
<br /> <br />

