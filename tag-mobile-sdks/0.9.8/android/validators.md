---
layout: page
title: Validators
permalink: /tag-mobile-sdks/0.9.8/android/validators/
---

The SDK provides validators that can be used to ensure that information entered by the user is valid.

There are three types of validators:

* **Validators** - low level validators that check aspects of a data type (e.g. NotNull, MinLength etc.)
* **Property validators** - check that a property is valid, often using multiple low level validators (e.g. validating address line1).  
* **Model validators** - validate a model by using multiple property validators and return a list<ValidationFailure> of all properties that have errors(e.g. validating AddressDetails) 

The validators can be found in the package <code>com.powatag.android.sdk.validators</code>


####? UKAddressValidator - checks if line1, county, city are less than 256char and that postcode is in correct format


The following classes implement the <code>ModelValidator<T><\code> interface which defines one method <code>validate(T input)<\code>:

DESCIBE AddressDetailsValidator, CountryAwareCardNumberValidator,CountryAwareAddressDetailValidators, CreditCardValidator, ProfileValidator

* AddressDetailsValidator - .Class implements ModelValidator<AddressDetails>. Returns a list of ValidationFailure and if there were none it is an empty list.
			Uses the CountryAwareAddressDetailContext to obtain the country specific validators for the AddressDetail 
			validators:
				CountryValidator
				AliasValidator 
				PostcodeValidator (country specific)
				AddressLineValidator (country specific) to validate state, city, line1 and line2 )
				CountyValidator (country specific)
				NameValidator (country specific) to validate firstName and lastName
				
				
* ProfileDetailsValidator - validates a ProfileDetails object. This class extends ModelValidator<ProfileDetails>.   
			Uses 
				nameValidator for firstname,lastname. 
				emailvalidator for email, 
				mobilenumbervalidator for mobile number 
				passcodevalidator for passcode
* PaymentMethodDetailsValidator - validates a PaymentMethodDetails object. Class implements ModelValidator<PaymentMethodDetails>. 
			uses 
				CreditCardCardHolderNameValidator for cardHolderName 
				CardNumberValidator for cardNumber 
				ExpiryDateValidator for expiryDate
				IssueNumberValidator for issueNumber
				ValidFromDateValidator for validFrom date


				
The classes implement the PropertyValidator interface providing one method 'validate' returns validationError:

* TextValidator - checks if a string is withing a min max length and conforms to a (optional) format. Extends PropertyValidator<String>
* UkPostcodeValidator - checks if a UK postcode is valid based on UK Format.  This class extends PostcodeValidator 
* ChinaPostcodeValidator - checks for Chinese postcode format.Class extends PostcodeValidator
* PostcodeValidator - checks if postcode is a valid format, Class extends TextValidator
* MobileNumberValidator - checks if a mobile number is valid (!null and correct format) for a specific country. The countr code is set during instantiation of the object. This class extends PropertyValidator<String>
* PasscodeValidator - checks if the passcode is digitsonly, length = 6. class implements PropertyValidator<String>
* IssueNumberValidator - checks if issue number is 4 digits long and only digits 0-9 used. class extends TextValidator
* ValidFromDateValidator - checks if validFrom date is between -80 years and this month of this year. Class extends CardDateValidator
* ExpiryDateValidator - checks if expiryDate is between this month and 20years from now   .Class extends CardDateValidator
* CardDateValidator - checks if yearmonth is between a min and max range. Class extends PropertyValidator<YearMonth>
* AliasValidator - checks if Alisa is less than 256 characters long. Class extends TextValidator
* TitleValidator - checks if title is valid. class extends TextValidator
* EmailValidator - check if email address conforms to valid pattern. Class extends TextValidator
* CardHolderNameValidator - checks if cardholdername is less than 256 chars and text pattern    .Class extends TextValidator
* AddressLineValidator - checks if address line is less than 256 chars. Class extends TextValidator.
* CardNumberValidator - checks if card number is not null, min length, max length, format based on card issuer. Class implements PropertyValidator<String>
* CountyValidator - checks if county is between 0 and 256 chars.Class extends TextValidator
* CvvValidator - checks if CVV is correct length for issuer and that only digits 0-9 are used. Class extends TextValidator
* DecimalValueValidator - abstract class providing logic for decimal values.  required, and between min max range.. Class implements PropertyValidator<Double> 
* DonationAmountValidator - checks if donation amount is >= 0. Class extends DecimalValueValidator
* IntValueValidator - abstract class providing logic for int values. required, minval, maxval. Class implements PropertyValidator<Integer>
* NameValidator - checks if name is less than 256 char and has correct format. Class extends TextValidator
* CountryValidator - checks if country has a 2 char length alpha2code. class extends TextValidator






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




The following example 

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

	<pre>CountryAwareAddressDetailContext countryAwareContext
	AddressDetailsValidator addressDetailsValidator = new AddressDetailsValidator();
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







