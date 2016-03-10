---
layout: page
title: Profile on Android
permalink: /tag-mobile-sdks/0.9.8/android/profile/
---

A PowaTag user profile stores the personal user information, cards and addresses of the user. To retrieve or manage a user's profile you must first [Login]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/login/).

After logging in you can retrieve the current user's profile using <code>ManagerFactory.getInstance().getProfileManager().getCurrentProfile()</code>.

<br />

# Retrieving the Current User's Profile Information

1. The current authenticated user's profile, which reflects any successful modifications, can be retrieved using the `ManagerFactory`:

    <pre>Profile profile = ManagerFactory.getInstance().getProfileManager().getCurrentProfile();</pre>
	
	For those using RxJava, the `RxManagerFactory` is used instead:
	
	<pre>Profile profile = RxManagerFactory.getInstance().getProfileManager().getCurrentProfile();</pre>	

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

    <pre>ProfileManager profileManager = ManagerFactory.getInstance().getProfileManager();
    profileManager.getProfile(new PowaTagCallback&lt;Profile&gt;() {
     public void onSuccess(Profile latestProfile) {
       // Profile was successfully retrieved
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>

    The synchronous version of the <code>getProfile</code> method should <b>not be used in the main thread</b> to avoid performance issues

    <code> Profile latestProfile = profileManager.getProfile(); </code>
	
	<br />This can also be done using RxJava:
	
	<pre>RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
	profileManager.getProfile().subscribe(new Subscriber&lt;Profile&gt;() {
		@Override
		public void onCompleted() {
		}

		@Override
		public void onError(Throwable e) {
		}

		@Override
		public void onNext(Profile profile) {
		}
	});
	</pre>
	
<br/>

# Adding an Address

For more information on using and displaying addresses see [Addresses]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/addresses/).

1. Create a new Address object and set the address information:

	<pre>AddressDetails addressDetails = new AddressDetails();
	addressDetails.setAlias("Powa");
	addressDetails.setFirstName("Joe");
	addressDetails.setLastName("Bloggs");
	addressDetails.setLine1("110 Bishopsgate");
	addressDetails.setCity("London");
	addressDetails.setPostCode("EC2N 4AY");
	addressDetails.setCounty("London");
	Country country = new Country();
	country.setAlpha2Code("GB");
	country.setName("United Kingdom");
	addressDetails.setCountry(country);</pre>

2. Validate the address details
    
	Use <code>AddressDetailsValidator</code> to verify that all address details have been entered correctly.	

    <pre><code>AddressDetailsValidator addressDetailsValidator = new AddressDetailsValidator(CountryAwareAddressDetailContext.UK); //set the country to validate for
	List<ValidationFailure> errors = addressDetailsValidator.validate(addressDetails);
	if(errors != null){
		for (int s = 0; s < errors.size(); s++) {
			ValidationFailure validationFailure = errors.get(s);
			String property = validationFailure.getPropertyName();
			ValidationError errorCode = validationFailure.getErrorCode();
			// Display validation to user and obtain updated value
		}
	} else {
		// No issues found while validating the address details
    }</code></pre>
		
	
For more information on validators please see the [Validators]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/validators/) page. <br />
	
	
		
3. Add the address to the user profile using the ProfileManager:

    <pre>ProfileManager pm = ManagerFactory.getInstance().getProfileManager();
	pm.addAddress(address, new PowaTagCallback&lt;String&gt;() {
     public void onSuccess(Address addedAddress) {
       // Address was successfully added
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>

    The synchronous version of the <code>addAddress</code> method should <b>not be used in the main thread</b> to avoid performance issues

    <code>Address addedAddress = pm.addAddress(addressDetails);</code>
	
	<br />
	This can also be done using RxJava:
	
    <pre>RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
    profileManager.addAddresss(addressDetails).subscribe(new Subscriber&lt;Address&gt;() {
		@Override
		public void onCompleted() {
		} 
 
		@Override
		public void onError(Throwable e) {
		}

		@Override
		public void onNext(Address addedAddress) {
		}
	});</pre>

 4. The new address will also be available in the current profile:

     <pre>List&lt;Address&gt; addresses = ManagerFactory.getInstance().getProfileManager().getCurrentProfile().getAddresses();</pre>

<br />

# Updating an Address

1. Create an AddressDetails object from an existing Address and modify the address information:

    <pre>AddressDetails modifiedAddress = address.editableCopy();
   modifiedAddress.setAlias("110 Bishopsgate");</pre>

2. Validate the address details

	Use the details described in step 2 of [Adding an Address]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/profile/#adding-an-address) to verify the properties of <code>AddressDetails</code>.

3. Use the ProfileManager to update the address information:

    <pre>ProfileManager pm = ManagerFactory.getInstance().getProfileManager();
    pm.updateAddress(address, modifiedAddress, new PowaTagCallback&lt;Address&gt;() {
     public void onSuccess(Address updatedAddress) {
       // Address was successfully updated
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>

    The synchronous version of the <code>updateAddress</code> method should <b>not be used in the main thread</b> to avoid performance issues

    <code>Address updatedAddress = pm.updateAddress(address, modifiedAddress); </code>
    <br />
	
	This can also be done using RxJava:
	
	<pre>RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
	profileManager.updateAddress(address,modifiedAddressDetails).subscribe(new Subscriber&lt;Address&gt;() {
		@Override
		public void onCompleted() {
		}

		@Override
		public void onError(Throwable e) {
		}

		@Override 
		public void onNext(Address updatedAddress) {
		}
	});
	</pre>

# Deleting an Address

1. Use the ProfileManager to delete an existing address:

    <pre>ProfileManager pm = ManagerFactory.getInstance().getProfileManager();
   pm.deleteAddress(address, new PowaTagCallback&lt;Profile&gt;() {
     public void onSuccess(Profile updatedProfile) {
       // Address was successfully deleted from profile
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>

   The synchronous version of the <code>deleteAddress</code> method should <b>not be used in the main thread</b> to avoid performance issues

    <code>Profile updatedProfile = pm.deleteAddress(address) </code>
    <br/>
   	This can also be done using RxJava:
	
	<pre>RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
	profileManager.deleteAddress(address).subscribe(new Subscriber&lt;Profile&gt;() {
	@Override
	public void onCompleted() {
	}

	@Override
	public void onError(Throwable e) {
	}

	@Override
	public void onNext(Profile updatedProfile) {
	}
	});
	</pre>


# Adding a Payment Instrument

1. Create a new PaymentMethodDetails object and set the card information:

    <pre>PaymentMethodDetails paymentMethodDetails = new PaymentMethodDetails();
   paymentMethodDetails.setCardHolderName("Joe Bloggs");
   paymentMethodDetails.setCardNumber("4111111111111111");
   paymentMethodDetails.setValidFromDate(new YearMonth(2010, 1));
   paymentMethodDetails.setExpiryDate(new YearMonth(2020, 1));</pre>

2. Validate the payment method details

	Use <code>PaymentMethodDetailsValidator</code> to verify that all payment method details have been entered correctly.

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
	
	For more information on validators please see the [Validators]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/validators/) page. <br />	

3. Create a new PaymentInstrumentDetails object and set the payment instrument, billing address and other information:

    <pre>PaymentInstrumentDetails paymentInstrumentDetails = new PaymentInstrumentDetails();  paymentInstrumentDetails.setPaymentMethodDetails(paymentMethodDetails);
	paymentInstrumentDetails.setIssuer(CreditCardIssuer.VISA);
	paymentInstrumentDetails.setPaymentType(PaymentMethodType.PAYMENT_CARD);
	paymentInstrumentDetails.setPhone(01234567890);
	paymentInstrumentDetails.setEmail(customer@powa.com);
	paymentInstrumentDetails.setBillingAddressId(addressId);</pre>

4. Add the payment instrument to the user profile using the ProfileManager:

	<pre>ProfileManager pm = ManagerFactory.getInstance().getProfileManager();
	pm.addPaymentInstrument(paymentInstrument, new PowaTagCallback&lt;PaymentInstrument&gt;() {
		public void onSuccess(PaymentInstrument addedPaymentInstrument) {
		// Payment instrument was successfully added
		}
		public void onError(PowaTagException exception) {
		}
	});</pre>

	The synchronous version of the <code>addPaymentInstrument</code> method should <b>not be used in the main thread</b> to avoid performance issues.

	<pre>PaymentInstrument addedPaymentInstrument = pm.addPaymentInstrument(paymentInstrumentDetails);</pre>
<br />	
	This can also be done using RxJava:
	
	<pre>RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
	profileManager.AddPaymentInstrument(paymentInstrumentDetails).subscribe(new Subscriber&lt;PaymentInstrument&gt;() {
	 @Override
	 public void onCompleted() {
	 }
  
	 @Override
	 public void onError(Throwable e) {
	 }
 
 	 @Override 
	 public void onNext(PaymentInstrument paymentInstrument) {
	 }
	});
	</pre>
		

5. If the payment instrument needs to be activated, send an activation code to the user.

    <pre>
        ProfileManager pm = ManagerFactory.getInstance().getProfileManager();
        
        // Check whether the payment instrument requires activation
        if (paymentInstrument.activationStatus != NOT_REQUIRED)
        {
            pm.sendActivationCode(paymentInstrument);
        }
    </pre>
    
    The activation code is saved, referencing the user's profile and the payment instrument.
    
6. Once the user inputs the activation code, activate the payment instrument.

    <pre>
        string activationCode = "123456";
        pm.activatePaymentInstrument(activationCode, paymentInstrument);
    </pre>
 
7. The new payment instrument will also be available in the current profile:

    <pre>List&lt;PaymentInstrument&gt; paymentInstruments = ManagerFactory.getInstance().getProfileManager().getCurrentProfile().getPaymentInstruments();</pre>

<br />

# Updating a Payment Instrument

You can only change the billing address of a payment instrument once created.

1. Use the ProfileManager to update the billing address of a payment instrument:

    <pre>ProfileManager pm = ManagerFactory.getInstance().getProfileManager();
    pm.updatePaymentInstrument(paymentInstrument, newBillingAddress, new PowaTagCallback&lt;Address&gt;() {
     public void onSuccess(PaymentInstrument updatedPaymentInstrument) {
       // Payment instrument was successfully updated
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>

   The synchronous version of the <code>updateAddress</code> method should <b>not be used in the main thread</b> to avoid performance issues

    <code>PaymentInstrument updatedPaymentInstrument = pm.updatePaymentInstrument(paymentInstrument, newBillingAddress) </code>
	<br />	
	This can also be done using RxJava:
	
	<pre>RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
	profileManager.updatePaymentInstrument(paymentInstrument, billingAddress).subscribe(new Subscriber&lt;PaymentInstrument&gt;() {
	 @Override
	 public void onCompleted() {
	 }
  
	 @Override
	 public void onError(Throwable e) {
	 }
 
 	 @Override 
	 public void onNext(PaymentInstrument updatedPaymentInstrument) {
	 }
	});
	</pre>

<br />

# Deleting a Payment Instrument

1. Use the ProfileManager to delete an existing payment instrument:

    <pre>ProfileManager profileManager = ManagerFactory.getInstance().getProfileManager();
	profileManager.deletePaymentInstrument(paymentInstrument, new PowaTagCallback&lt;Profile&gt;() {
      public void onSuccess(Profile updatedProfile) {
        // Payment instrument was successfully deleted from profile
      }
      public void onError(PowaTagException exception) {
      }
   });</pre>

    The synchronous version of the <code>deletePaymentInstrument</code> method should <b>not be used in the main thread</b> to avoid performance issues:

    <code> Profile updatedProfile =profileManager.deletePaymentInstrument(paymentInstrument); </code>
	<br />
	This can also be done using RxJava:
	
	<pre>RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
	profileManager.deletePaymentInstrument(paymentInstrument).subscribe(new Subscriber&lt;Profile&gt;() {
	 @Override
	 public void onCompleted() {
	 }
  
	 @Override
	 public void onError(Throwable e) {
	 }
 
 	 @Override 
	 public void onNext(Profile updatedProfile) {
	 }
	});
	</pre>

<br />

# Getting the Payment Instruments Accepted by a Merchant

To obtain the list of payment instruments from the user profile that are accepted by a specified <code>Merchant</code>:

    <code>List<PaymentInstrument> acceptedPaymentInstruments = ManagerFactory.getInstance().getProfileManager().getCurrentProfile().getAcceptedPaymentInstruments(merchant);</code>

	In the case where the profile does not contain any accepted payment instruments an empty <code>List</code> is returned.

<br/>

# Checking the Profile Against a Merchant's Requirements

Before transacting with a merchant you should check if the profile contains all the information required for the merchant.

   <pre>boolean canTransact = profile.hasRequiredInfo(merchant);</pre>

<br/>


# Updating the Profile

1. Create a new ProfileDetails object and set the profile information:

    <pre>ProfileDetails profileDetails = new ProfileDetails();
    profileDetails.setTitle("M");
    profileDetails.setFirstName("Joe");
    profileDetails.setLastName("Bloggs");
    profileDetails.setEmail("jbloggs@powa.com");
    profileDetails.setMobileNumber("01234567890");
    profileDetails.setPasscode (“123456”);</pre>


2. Validate the profile details

	Use <code>ProfileDetailsValidator</code> to verify that all profile details have been entered correctly.

	<pre>ProfileDetailsValidator profileDetailsValidator = new ProfileDetailsValidator();
	List&lt;ValidationFailure&gt; errors = profileDetailsValidator.validate(profile);
	if(errors != null){
		for (int s = 0; s < errors.size(); s++) {
			ValidationFailure validationFailure = errors.get(s);
			String property = validationFailure.getPropertyName();
			ValidationError errorCode = validationFailure.getErrorCode();
			// Display validation to user and obtain an updated value
		}
	} else {
		// No issues found while validating the profile details
	}</pre>

	For more information on validators please see the [Validators]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/validators/) page. <br />	

3. Use the ProfileManager to update the current profile:

    <pre>ProfileManager pm = ManagerFactory.getInstance().getProfileManager();
    pm.updateProfile(profileDetails, new PowaTagCallback&lt;Profile&gt;) {
     public void onSuccess(Profile updatedProfile) {
       // Profile information is updated
     }
     public void onError(PowaTagException exception) {
     }
   }
   </pre>

	The synchronous version of the <code>updateProfile</code> method should <b>not be used in the main thread</b> to avoid performance issues

	<pre>Profile updatedProfile = pm.updateProfile(profileDetails);</pre>
	
	<br />
	This can also be done using RxJava:
	
	<pre>RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
	profileManager.updateProfile(profileDetails).subscribe(new Subscriber&lt;Profile&gt;() {
	 @Override
	 public void onCompleted() {
	 }
  
	 @Override
	 public void onError(Throwable e) {
	 }
 
 	 @Override 
	 public void onNext(Profile updatedProfile) {
	 }
	});
	</pre>

<br/>

4. The updated profile information will be reflected in the users current profile:

	<pre>Profile profile = ManagerFactory.getInstance().getProfileManager().getCurrentProfile();</pre>

<br/>

# Saving the Profile

1. Use the ProfileManager to save the current profile:

	Saving a temporary profile makes it permanent which will allow the user to log into the same profile at a later time or on another device.

	<pre>signUpDetails = new SignUpDetails(passwordEditText.getText().toString());
	ProfileManager pm = ManagerFactory.getInstance().getProfileManager();
	pm.saveProfile(signUpDetails, new PowaTagCallback&lt;Profile&gt;() {
		public void onSuccess(@Nullable Set<Coupon> coupons) {
		// Profile is now permanent. Display returned coupons to user
		}
		public void onError(PowaTagException exception) {
		}
	}</pre>
 <br/>

	The synchronous version of the <code>saveProfile</code> method should <b>not be used in the main thread</b> to avoid performance issues

	<code>Profile savedProfile = pm.saveProfile(password); </code>
<br/>
    This can also be done using RxJava:
	
	<pre>signUpDetails = new SignUpDetails(passwordEditText.getText().toString());
	RxProfileManager profileManager = RxManagerFactory.getInstance().getProfileManager();
	profileManager.saveProfile(signUpDetails).subscribe(new Subscriber&lt;Set&lt;Coupon&gt;&gt;() {
	 @Override
	 public void onCompleted() {
	 }
  
	 @Override
	 public void onError(Throwable e) {
	 }
 
 	 @Override 
	 public void onNext(Set<Coupon> registrationCoupons) {
	    // display coupons to user.
	 }
	});
	</pre>


