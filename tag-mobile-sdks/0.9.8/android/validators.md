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

The following usage example shows how to use the `AddressDetailsValidator`:


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
<br />

##  Property Validators

These validators are used to ensure that a single property is valid, often using multiple low level validators (e.g. validating the address line1 property).  

They implement the `PropertyValidator` interface which defines a method called `validate` which returns a single `ValidationError`.

The following property validators are available:<br />

* TextValidator - checks if a string is withing a min max length and conforms to a (optional) format. Extends PropertyValidator<String>

### TextValidator
Checks if a string is withing a min max length and conforms to a (optional) format. Extends PropertyValidator<String>

* PostcodeValidator - checks if postcode is a valid format, Class extends TextValidator
* UkPostcodeValidator - checks if a UK postcode is valid based on UK Format.  This class extends PostcodeValidator 
* ChinaPostcodeValidator - checks for Chinese postcode format.Class extends PostcodeValidator
* IssueNumberValidator - checks if issue number is 4 digits long and only digits 0-9 used. class extends TextValidator
* AliasValidator - checks if Alisa is less than 256 characters long. Class extends TextValidator
* TitleValidator - checks if title is valid. class extends TextValidator
* EmailValidator - check if email address conforms to valid pattern. Class extends TextValidator
* CardHolderNameValidator - checks if cardholdername is less than 256 chars and text pattern    .Class extends TextValidator
* AddressLineValidator - checks if address line is less than 256 chars. Class extends TextValidator.
* CountyValidator - checks if county is between 0 and 256 chars.Class extends TextValidator
* CvvValidator - checks if CVV is correct length for issuer and that only digits 0-9 are used. Class extends TextValidator
* NameValidator - checks if name is less than 256 char and has correct format. Class extends TextValidator
* CountryValidator - checks if country has a 2 char length alpha2code. class extends TextValidator
* CardDateValidator - checks if yearmonth is between a min and max range. Class extends PropertyValidator<YearMonth>
* ValidFromDateValidator - checks if validFrom date is between -80 years and this month of this year. Class extends CardDateValidator
* ExpiryDateValidator - checks if expiryDate is between this month and 20years from now   .Class extends CardDateValidator
* MobileNumberValidator - checks if a mobile number is valid (!null and correct format) for a specific country. The countr code is set during instantiation of the object. This class extends PropertyValidator<String>
* PasscodeValidator - checks if the passcode is digitsonly, length = 6. class implements PropertyValidator<String>
* CardNumberValidator - checks if card number is not null, min length, max length, format based on card issuer. Class implements PropertyValidator<String>
* DecimalValueValidator - abstract class providing logic for decimal values.  required, and between min max range.. Class implements PropertyValidator<Double> 
* DonationAmountValidator - checks if donation amount is >= 0. Class extends DecimalValueValidator
* IntValueValidator - abstract class providing logic for int values. required, minval, maxval. Class implements PropertyValidator<Integer>






##  Validators
These low level validators are used to check aspects of a data type (e.g. NotNull, MinLength)



				





The following classes implement the Validator<T> interface with one method 'isValid' low level validators are available:

* FormatValidator - checks if input is in specified regular expression. Class implements Validator<String> 
* MaxLengthValidator - set the max length during isntatiation and then use isValid (string) to check if string legnth is less than maxLength. class implements Validator<String>
* MinDecimalValueValidator - checks that the input is not less thatn the min allowed value (which is set during instantiation). Class implements Validator<Double> 
* MinIntValueValidator -  checks whether the input is not lower than the min value (which is set during instantiation). Class implements Validator<Integer> 
* MinLengthValidator - checks whether the input is not shorter than the minimum length (set during instantiation). Class implements Validator<String>
* LuhnValidator - uses Luhn algorithm to verify . class implements Validator<String>
* MaxDecimalValueValidator - Checks that an input is not greater than the maximum allowed value. Class implements Validator<Double>
* MaxIntValueValidator - Checks whether the input is not greater than the maximum value. Class implements Validator<Integer>
* NotEmptyValidator - checks if the input is an empty string. Class implements Validator<String> 
* NotNullValidator - checks if input object is not null. Class implements Validator<Object>


public ValidationFailure
constructor ValidationFailure(String propertyName , ValidationError validationError)


public enum ValidationError {

    /**     * Is null or empty.     */
    IS_NULL_OR_EMPTY,

    /**     * Too short.     */
    TOO_SHORT,

    /**     * Too long.     */
    TOO_LONG,

    /**     * Too low.     */
    TOO_LOW,

    /**     * Too high.     */
    TOO_HIGH,

    /**     * Invalid format.     */
    INVALID_FORMAT,

    /**     * Invalid Luhn checksum.     */
    INVALID_CHECKSUM,

    /**     * Is null.     */
    IS_NULL,

    /**     * Before the minimum date.     */
    BEFORE_MIN_DATE,

    /**     * After the maximum date.     */
    AFTER_MAX_DATE,

    /** Credit card issuer is not one of the supported issuers. */
    ISSUER_NOT_SUPPORTED

}







	For more information on each of these property validators please see the reference documentation included as part of the SDK.









####? UKAddressValidator - checks if line1, county, city are less than 256char and that postcode is in correct format
DESCIBE CountryAwareCardNumberValidator, CreditCardValidator 