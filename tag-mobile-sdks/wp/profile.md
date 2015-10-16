---
layout: page
title: Profile on Windows Phone
permalink: /tag-mobile-sdks/wp/profile/
---

A PowaTag user profile stores the personal user information, cards and addresses of the user. To retrieve or manage the users profile you must first [Login]({{site.baseurl}}/tag-mobile-sdks/wp/login/).

After logging in you can retrieve the current user profile using `Profile.CurrentProfile`. You can then use ProfileManager to add addresses, cards or update the user profile.

<br />

# Retrieving the Current User's Profile Information

1. The users current profile, which reflects any successful modifications, can be retrieved using:

    <pre>Profile profile = Profile.GetCurrentProfile();</pre>

2. Check whether the current profile is temporary using:

    <pre>boolean isTemporary = profile.IsTemporary;</pre>

3. Get the list of addresses currently added to the profile with:

    <pre>IReadonlyCollection&lt;Address&gt; addresses = profile.Addresses;</pre>
	
4. Get the default address with:

	<pre> Address defaultAddress = profile.DefaultAddress;</pre>

5. Get the list of payment instruments currently added to the profile with:

    <pre>IReadonlyCollection&lt;PaymentInstrument&gt; paymentInstruments = profile.PaymentInstruments;</pre>
	
6. Get the default payment instrument with:

    <pre>PaymentInstrument defaultPaymentInstrument = profile.DefaultPaymentInstrument;</pre>

7. Get the device ID associated with the profile with:

	<pre>string deviceId = profile.DeviceId;</pre>

8. Get the profile ID with:

	<pre>string profileId = profile.ProfileId;</pre>
    
9. Check if the user profile is active and can be used:
    
    <pre>boolean activeProfile = profile.IsActive;</pre>

10. Get a list of any custom data keys attached to the profile:
    
    <pre>List&lt;CustomDataValue&gt; customDataValues = profile.CustomDataValues;</pre>


<br />

# Adding an Address

For more information on using and displaying addresses see [Addresses]({{site.baseurl}}/tag-mobile-sdks/wp/addresses/).

1. Create a new Address object and set the address information:

	<pre>Address address = new Address();
	address.Alias = "Powa";
	address.FirstName = "Dan";
	address.LastName = "Wagner";
	address.Line1 = "110 Bishopsgate";
	address.City = "London";
	address.PostCode = "EC2N 4AY";
	address.County = "London";
	address.Country = Country.UnitedKingdom;</pre>
	
2. Validate the address details

	Use <code>AddressDetailsValidator</code> to verify that all address details have been entered correctly. 
	This validator uses property validators to validate each property of <code>AddressDetails</code>:
	
	* <code>AliasValidator</code> - to check the alias.
	* <code>NameValidator</code> - to check the first name, last name and county.
	* <code>UkPostcodeValidator</code> - to check the post code.
	* <code>AddressLineValidator</code> - to check all remaining address lines for checking all address lines.
	
	
	For more information on each of these property validators please see the reference documentation.
	
	<pre>AddressDetailsValidator addressDetailsValidator = new AddressDetailsValidator();
	List&lt;ValidationFailure&gt; errors = addressDetailsValidator.Validate(address);
	if (errors != null)
	{
		foreach (ValidationFailure validationFailure in errors)
		{
			String property = validationFailure.PropertyName;
			ValidationErrors errorCode = validationFailure.ErrorCode;
			// Display validation to user and obtain updated value
		}
	}
	else
	{
    // No issues found while validating the address details
	}</pre>	
	
3. Add the address to the user profile using the ProfileManager:

	<pre>ProfileManager pm = ProfileManager.Instance;
	Address addedAddress = await pm.AddAddressAsync(address);
	// Address was successfully added</pre>

4. The new address will also be available in the current profile:

    <pre>IReadonlyCollection&lt;Address&gt; addresses = ProfileManager.GetInstance().GetCurrentProfile().Addresses;</pre>

<br />

# Updating an Address

1. Create an AddressDetails object from an existing Address and modify the address information:

    <pre>AddressDetails modifiedAddress = address.EditableCopy();
   modifiedAddress.Alias = "110 Bishopsgate";</pre>

2. Validate the address details

	Use the details described in step 2 of [Adding an Address]({{site.baseurl}}/tag-mobile-sdks/wp/profile/#adding-an-address) to verify the properties of <code>AddressDetails</code>.
   
3. Use the ProfileManager to update the address information:

    <pre>ProfileManager pm = ProfileManager.GetInstance();
   Address updatedAddress = pm.UpdateAddressAsync(address, modifiedAddress);
   // Address was successfully updated</pre>

<br />

# Deleting an Address

1. Use the ProfileManager to delete an existing address:

    <pre>ProfileManager pm = ProfileManager.GetInstance();
   Profile updatedProfile = await pm.DeleteAddressAsync(address);
   // Address was successfully deleted from profile</pre>

<br />

# Adding a Payment Instrument

1. Create a new PaymentInstrument object and set the card information:

    <pre>PaymentMethodDetails paymentMethod = new PaymentMethodDetails();
   paymentMethod.CardHolderName = "Dan Wagner";
   paymentMethod.CardNumber = "4111111111111111";
   paymentMethod.ValidFromDate = new YearMonth(2010, 1);
   paymentMethod.ExpiryDate = new YearMonth(2020, 1);</pre>

2. Validate the payment method details

	Use <code>PaymentMethodDetailsValidator</code> to verify that all payment method details have been entered correctly. 
	This validator uses property validators to validate each property of <code>PaymentMethodDetails</code>:
	
	* <code>CardHolderNameValidator</code> - to check the card holder name.
	* <code>CardNumberValidator</code> - to check the card number.
	* <code>ExpiryDateValidator</code> - to check the expiry date.
	* <code>ValidFromDateValidator</code> - to check valid from date.
		
	For more information on each of these property validators please see the reference documentation.
	
	<pre>PaymentMethodDetailsValidator paymentMethodDetailsValidator = new PaymentMethodDetailsValidator();
	List&lt;ValidationFailure&gt; errors = paymentMethodDetailsValidator.Validate(address);
	if (errors != null)
	{
		foreach (ValidationFailure validationFailure in errors)
		{
			String property = validationFailure.PropertyName;
			ValidationErrors errorCode = validationFailure.ErrorCode;
			// Display validation to user and obtain updated value
		}
	}
	else
	{
    // No issues found while validating the payment method details
	}</pre>
   
3. Create a new PaymentMethod object and set the payment instrument, billing address and other information:

    <pre>PaymentInstrumentDetails paymentInstrument = new PaymentInstrumentDetails();
   paymentInstrument.Issuer = CreditCardIssuer.Visa;
   paymentInstrument.PaymentMethod = paymentMethod;
   paymentInstrument.Alias = "Powa";
   paymentInstrument.PaymentType = PaymentMethodType.PaymentCard;
   paymentInstrument.BillingAddressId = addressId;</pre>

4. Add the payment instrument to the user profile using the ProfileManager:

    <pre>ProfileManager pm = ProfileManager.GetInstance();
   PaymentInstrument addedPaymentInstrument = await pm.AddPaymentInstrumentAsync(paymentInstrument);
   // Payment method was successfully added</pre>

5. The new payment instrument will also be available in the current profile:

    <pre>IReadonlyCollection&lt;PaymentInstrument&gt; paymentInstruments = ProfileManager.GetInstance().GetCurrentProfile().PaymentInstruments;</pre>

<br />

# Updating a Payment Instrument

You can only change the billing address of a payment instrument once created.

1. Use the ProfileManager to update the billing address of a payment instrument:

    <pre>ProfileManager pm = ProfileManager.GetInstance();
   PaymentInstrument updatedPaymentInstrument = pm.UpdatePaymentInstrumentAsync(paymentInstrument, newBillingAddress);
   // Payment instrument was successfully updated</pre>

<br />

# Deleting a Payment Instrument

1. Use the ProfileManager to delete an existing payment instrument:

    <pre>ProfileManager pm = ProfileManager.GetInstance();
   Profile updatedProfile = await pm.DeletePaymentInstrumentAsync(paymentInstrument);
   // Payment instrument was successfully deleted from profile</pre>

<br />

# Getting the Payment Instruments Accepted by a Merchant

1. To obtain the payment instruments from the profile that are accepted by a specified <code>Merchant</code> use:
	
	<pre>Profile profile = ProfileManager.getInstance().getCurrentProfile();
	IReadOnlyList&lt;PaymentInstrument&gt; acceptedPaymentInstruments = profile.GetAcceptedPaymentMethods(merchant); </pre>
    
In the case where the profile does not contain any accepted payment instruments an empty <code>IReadOnlyList</code> will be returned.

<br/>


# Checking the Profile Against a Merchant's Requirements
 
1. Before transacting with a merchant you should check if the profile contains all the information required for the merchant.
		
	<pre>bool canTransact = profile.HasRequiredInfo(merchant);</pre>

<br/>

# Updating the Profile

1. Create a new ProfileUpdate object and set the profile information:

    <pre>ProfileDetails profile = new ProfileDetails();
   profile.Title = "CEO";
   profile.FirstName = "Dan";
   profile.LastName = "Wagner";
   profile.Email = "support@powa.com";
   profile.MobileNumber = "01234567890";</pre>

2. Validate the profile details

	Use <code>ProfileDetailsValidator</code> to verify that all profile details have been entered correctly. 
	This validator uses property validators to validate each property of <code>ProfileDetails</code>:
	
	* <code>NameValidator</code> - to check the title, first and last names.
	* <code>EmailValidator</code> - to check the email address.
	* <code>MobileNumberValidator</code> - to check the mobile number.
			
	For more information on each of these property validators please see the reference documentation.
	
	<pre>ProfileDetailsValidator profileDetailsValidator = new ProfileDetailsValidator();
	List&lt;ValidationFailure&gt; errors = profileDetailsValidator.Validate(address);
	if (errors != null)
	{
		foreach (ValidationFailure validationFailure in errors)
		{
			String property = validationFailure.PropertyName;
			ValidationErrors errorCode = validationFailure.ErrorCode;
			// Display validation to user and obtain updated value
		}
	}
	else
	{
    // No issues found while validating the profile details
	}</pre>	
	
   
3. Use the ProfileManager to update the current profile:

    <pre>ProfileManager pm = ProfileManager.GetInstance();
   Profile updatedProfile = await pm.UpdateProfileAsync(profile);
   // Profile information is updated</pre>

4. The updated profile information will be reflected in the users current profile:

    <pre>Profile profile = ProfileManager.GetInstance().GetCurrentProfile();</pre>

# Saving the Profile

1. Use the ProfileManager to save the current profile:

    <pre>ProfileManager pm = ProfileManager.GetInstance();
   Profile savedProfile = await pm.SaveProfileAsync(string password);
   // Profile is no longer temporary</pre>
