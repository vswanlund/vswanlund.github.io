---
layout: page
title: Profile on Android
permalink: /tag-mobile-sdks/android/profile/
---

A PowaTag user profile stores the personal user information, cards and addresses of the user. To retrieve or manage a user's profile you must first [Login]({{site.baseurl}}/tag-mobile-sdks/android/login/).

After logging in you can retrieve the current user's profile using <code>ProfileManager.getInstance().getCurrentProfile()</code>.

<br />

# Retrieving the Current User's Profile Information

1. The current authenticated user's profile, which reflects any successful modifications, can be retrieved using:

    <pre>Profile profile = ProfileManager.getInstance().getCurrentProfile();</pre>

2. Check whether the current profile is temporary using:

    <pre>boolean isTemporary = profile.isTemporary();</pre>

3. Get the list of addresses currently added to the profile with:

    <pre>List&lt;Address&gt; addresses = profile.getAddresses();</pre>
    
4. Get the default address with:

    <pre>Address address = profile.getDefaultAddress();</pre>

5. Get the list of payment instruments currently added to the profile with:

    <pre>List&lt;PaymentInstrument&gt; paymentInstruments = profile.getPaymentInstruments();</pre>

6. Get the default payment instrument with:

    <pre>PaymentInstrument paymentInstrument = profile.getDefaultPaymentInstrument();</pre>

7. Get the device ID associated with the profile with:

	<pre>String deviceId = profile.getDeviceId();</pre>

8. Get the profile ID with:

	<pre>String profileId = profile.getProfileId();</pre>
    
9. Check if the user profile is active and can be used:
    
    <pre>boolean activeProfile = profile.isActive();</pre>

10. Get a list of any custom data keys attached to the profile:
    
    <pre>List&lt;CustomDataValue&gt; customDataValues = profile.getCustomDataValues();</pre>
        
<br />

# Retrieving the Latest Profile for the Current User

1. The latest profile information for the current user can be retrieved using:

    <pre>ProfileManager pm = ProfileManager.getInstance();
   pm.getProfile(new PowaTagCallback&lt;Profile&gt;() {
     public void onSuccess(Profile latestProfile) {
       // Profile was successfully retrieved 
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>
    
    The synchronous version of the <code>getProfile</code> method should not be used in the main thread to avoid performance issues 
    
    <code> Profile latestProfile = pm.getProfile(); </code>

<br/>

# Adding an Address

For more information on using and displaying addresses see [Addresses]({{site.baseurl}}/tag-mobile-sdks/android/addresses/).

1. Create a new Address object and set the address information:

	<pre>AddressDetails address = new AddressDetails();
	address.setAlias("Powa");
	address.setFirstName("Dan");
	address.setLastName("Wagner");
	address.setLine1("110 Bishopsgate");
	address.setCity("London");
	address.setPostCode("EC2N 4AY");
	address.setCounty("London");
	Country country = new Country();
	country.setAlpha2Code("GB");
	country.setName("United Kingdom");
	address.setCountry(country);</pre>
	
2. Validate the address details

	Use <code>AddressDetailsValidator</code> to verify that all address details are set correctly. 
	This validator uses property validators to validate each property of <code>AddressDetails</code>:

	The property validators used:
	
* <code>AliasValidator</code>: for checking the alias.
	* <code>NameValidator</code: for checking the first name, last name and county.
	* <code>UkPostcodeValidator</code>: for checking the post code.
	* <code>AddressLineValidator</code> for checking all address lines (line1, city,country).
	
	For more information on each of these property validators please refer to the reference documentation.
	
	<pre>AddressDetailsValidator addressDetailsValidator = new AddressDetailsValidator();
	
	
	    
    /**
     * {@inheritDoc}
     */
    @Nullable
    @Override
    public List<ValidationFailure> validate(@Nullable final AddressDetails input) {
        List<ValidationFailure> validationFailures = new ArrayList<>();

        addValidationFailure(validationFailures, "alias", aliasValidator.validate(input.getAlias()));
        addValidationFailure(validationFailures, "firstName", nameValidator.validate(input.getFirstName()));
        addValidationFailure(validationFailures, "lastName", nameValidator.validate(input.getLastName()));
        addValidationFailure(validationFailures, "state", addressLineValidator.validate(input.getState()));
        ValidationError countryError = addressLineValidator.validate(input.getCountry() == null ? null : input.getCountry().getAlpha2Code());
        addValidationFailure(validationFailures, "country", countryError);
        addValidationFailure(validationFailures, "postCode", ukPostcodeValidator.validate(input.getPostCode()));
        addValidationFailure(validationFailures, "line1", addressLineValidator.validate(input.getLine1()));
        addValidationFailure(validationFailures, "line2", addressLineValidator.validate(input.getLine2()));
        addValidationFailure(validationFailures, "county", nameValidator.validate(input.getCounty()));


3. Add the address to the user profile using the ProfileManager:

    <pre>ProfileManager pm = ProfileManager.getInstance();
   pm.addAddress(address, new PowaTagCallback&lt;String&gt;() {
     public void onSuccess(Address addedAddress) {
       // Address was successfully added
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>
    
    The synchronous version of the <code>addAddress</code> method should not be used in the main thread to avoid performance issues 
    
    <code> Address addedAddress = pm.addAddress(addressDetails); </code>

 4. The new address will also be available in the current profile:

     <pre>List&lt;Address&gt; addresses = ProfileManager.getInstance().getCurrentProfile().getAddresses();</pre>

<br />

# Updating an Address

1. Create an AddressDetails object from an existing Address and modify the address information:

    <pre>AddressDetails modifiedAddress = address.editableCopy();
   modifiedAddress.setAlias("110 Bishopsgate");</pre>

2. Use the ProfileManager to update the address information:

    <pre>ProfileManager pm = ProfileManager.getInstance();
   pm.updateAddress(address, modifiedAddress, new PowaTagCallback&lt;Address&gt;() {
     public void onSuccess(Address updatedAddress) {
       // Address was successfully updated
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>
   
    The synchronous version of the <code>updateAddress</code> method should not be used in the main thread to avoid performance issues 
    
    <code>Address updatedAddress = pm.updateAddress(address, modifiedAddress); </code>
   

<br />

# Deleting an Address

1. Use the ProfileManager to delete an existing address:

    <pre>ProfileManager pm = ProfileManager.getInstance();
   pm.deleteAddress(address, new PowaTagCallback&lt;Profile&gt;() {
     public void onSuccess(Profile updatedProfile) {
       // Address was successfully deleted from profile
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>
   
   The synchronous version of the <code>deleteAddress</code> method should not be used in the main thread to avoid performance issues 
    
    <code>Profile updatedProfile = pm.deleteAddress(address) </code>
   
   <br/>
   

# Adding a Payment Instrument

1. Create a new PaymentMethodDetails object and set the card information:

    <pre>PaymentMethodDetails paymentMethodDetails = new PaymentMethodDetails();
   paymentMethodDetails.setCardHolderName("Dan Wagner");
   paymentMethodDetails.setCardNumber("4111111111111111");
   paymentMethodDetails.setValidFromDate(new YearMonth(2010, 1));
   paymentMethodDetails.setExpiryDate(new YearMonth(2020, 1));</pre>

2. Create a new PaymentInstrumentDetails object and set the payment instrument, billing address and other information:

    <pre>PaymentInstrumentDetails paymentInstrumentDetails = new PaymentInstrumentDetails();
   paymentInstrumentDetails.setIssuer(CreditCardIssuer.VISA);
   paymentInstrumentDetails.setPaymentMethodDetails(paymentMethodDetails);
   paymentInstrumentDetails.setPaymentType(PaymentMethodType.PAYMENT_CARD);
   paymentInstrumentDetails.setBillingAddressId(addressId);</pre>

3. Add the payment instrument to the user profile using the ProfileManager:

    <pre>ProfileManager pm = ProfileManager.getInstance();
   pm.addPaymentInstrument(paymentInstrument, new PowaTagCallback&lt;PaymentInstrument&gt;() {
     public void onSuccess(PaymentInstrument addedPaymentInstrument) {
       // Payment instrument was successfully added
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>

The synchronous version of the <code>addPaymentInstrument</code> method should not be used in the main thread to avoid performance issues 

	<code> PaymentInstrument addedPaymentInstrument = pm.addPaymentInstrument(paymentInstrumentDetails); </code>


 4. The new payment instrument will also be available in the current profile:

    <pre>List&lt;PaymentInstrument&gt; paymentInstruments = ProfileManager.getInstance().getCurrentProfile().getPaymentInstruments();</pre>

<br />

# Updating a Payment Instrument

You can only change the billing address of a payment instrument once created.

1. Use the ProfileManager to update the billing address of a payment instrument:

    <pre>ProfileManager pm = ProfileManager.getInstance();
   pm.updatePaymentInstrument(paymentInstrument, newBillingAddress, new PowaTagCallback&lt;Address&gt;() {
     public void onSuccess(PaymentInstrument updatedPaymentInstrument) {
       // Payment instrument was successfully updated
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>
   
   The synchronous version of the <code>updateAddress</code> method should not be used in the main thread to avoid performance issues 
    
    <code>PaymentInstrument updatedPaymentInstrument = pm.updatePaymentInstrument(paymentInstrument, newBillingAddress) </code>

<br />

# Deleting a Payment Instrument

1. Use the ProfileManager to delete an existing payment instrument:

    <pre>ProfileManager pm = ProfileManager.getInstance();
   pm.deletePaymentInstrument(paymentInstrument, new PowaTagCallback&lt;Profile&gt;() {
     public void onSuccess(Profile updatedProfile) {
       // Payment instrument was successfully deleted from profile
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>
    
    The synchronous version of the <code>deletePaymentInstrument</code> method should not be used in the main thread to avoid performance issues:
    
    <code> Profile updatedProfile =pm.deletePaymentInstrument(paymentInstrument); </code>

<br />

# Getting the Payment Instruments Accepted by a Merchant

To obtain the payment instruments from the profile that are accepted by a specified <code>Merchant</code>:
	
	<pre>Profile profile = ProfileManager.getInstance().getCurrentProfile();
	List&lt;PaymentInstrument&gt; acceptedPaymentInstruments = profile.getAcceptedPaymentInstruments(merchant);</pre>
    
In the case where the profile does not contain any accepted payment instruments an empty <code>List</code> is returned.

<br/>


# Checking the Profile Against a Merchant's Requirements
 
Before transacting with a merchant you should check if the profile contains all the information required for the merchant.
		
   <pre>boolean canTransact = profile.hasRequiredInfo(merchant);</pre>

<br/>


# Updating the Profile

1. Create a new ProfileDetails object and set the profile information:

    <pre>ProfileDetails profile = new ProfileDetails();
   profile.setTitle("CEO");
   profile.setFirstName("Dan");
   profile.setLastName("Wagner");
   profile.setEmail("support@powa.com");
   profile.setMobileNumber("01234567890");</pre>

2. Use the ProfileManager to update the current profile:

    <pre>ProfileManager pm = ProfileManager.getInstance();
   pm.updateProfile(profile, new PowaTagCallback&lt;Profile&gt;) {
     public void onSuccess(Profile updatedProfile) {
       // Profile information is updated
     }
     public void onError(PowaTagException exception) {
     }
   }
   </pre>

	The synchronous version of the <code>updateProfile</code> method should not be used in the main thread to avoid performance issues 

	<pre>Profile updatedProfile = pm.updateProfile(profileDetails);</pre>
    
<br/>

3. The updated profile information will be reflected in the users current profile:

	<pre>Profile profile = ProfileManager.getInstance().getCurrentProfile();</pre>

<br/>
	
# Saving a Temporary Profile

1. Use the ProfileManager to save the current profile:

	Saving a temporary profile makes it permanent which will allow the user to log into the same profile at a later time or on another device.
	
	<pre>ProfileManager pm = ProfileManager.getInstance();
	pm.saveProfile(new PowaTagCallback&lt;Profile&gt;() {
		public void onSuccess(Profile savedProfile) {
		// Profile is no longer temporary
		}
		public void onError(PowaTagException exception) {
		}
	}</pre>
 <br/>
 
	The synchronous version of the <code>saveProfile</code> method should not be used in the main thread to avoid performance issues 

	<code>Profile savedProfile = pm.saveProfile(password); </code>
<br/>