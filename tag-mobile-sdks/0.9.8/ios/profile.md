---
layout: page
title: Profile on iOS
permalink: /tag-mobile-sdks/0.9.8/ios/profile/
---

A PowaTag user profile stores the personal user information, cards and addresses of the user. To retrieve or manage the users profile you must first [Login]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/login/).

After logging in you can retrieve the current user profile using `[PTKProfile currentProfile]`. You can then use PTKProfileManager to add addresses, cards or update the user profile.

<br />

# Retrieving the Current Profile Information

1. The users current profile, which reflects any successful modifications, can be retrieved using:

    <pre>PTKProfile *profile = [PTKProfileManager sharedManager].currentProfile;</pre>

2. Check whether the current profile is temporary using:

    <pre>BOOL isTemporary = profile.isTemporary;</pre>

3. Get the list of PTKAddresses currently added to the profile with:

    <pre>NSArray *addresses = profile.addresses;</pre>

4. Get the list of PTKPaymentInstruments currently added to the profile with:

    <pre>NSArray *paymentInstruments = profile.paymentInstruments;</pre>

<br />

# Adding an Address

For more information on using and displaying addresses see [Addresses]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/addresses/).

1. Create a new Address object and set the address information:

    <pre>PTKAddressDetails *addressDetails = [PTKAddressDetails addressDetailsWithAlias:@"Powa";
	firstName:@"Joe";
	lastName:@"Bloggs";
	line1:@"110 Bishopsgate";
	city:@"London";
	postCode:@"EC2N 4AY";
	county:@"London";
	country:PTKCountryUnitedKingdom];</pre>

2. Validate the address details

	Use <code>PTKAddressDetailsValidator</code> to verify that all address details have been entered correctly.
	This validator uses property validators to validate each property of <code>PTKAddressDetails</code>:

	For more information on each of these property validators please see the reference documentation included as part of the SDK.

	<pre>PTKAddressDetailsValidator *addressDetailsValidator = [PTKAddressDetailsValidator new];
	NSError *errors = [addressDetailsValidator validate:addressDetails];
	if (errors) {
		for (PTKValidationFailure *validationFailure in invalidData) {
			NSString *property = validationFailure.propertyName;
			PTKValidationError *errorCode = validationFailure.errorCode;;
			// Display validation to user and obtain updated value
		}
	} else {
		// No issues found while validating the address details
	}</pre>

	For more information on validators please see the [Validators]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/validators/) page. <br />

3. Add the address to the user profile using the PTKProfileManager:

    <pre>PTKProfileManager *profileManager = [PTKProfileManager sharedManager];
   [profileManager addAddress:addressDetails completion:^(PTKAddress *addedAddress, NSError *error) {
     if (addedAddress) {
       // Address was successfully added
     }
   }];</pre>

4. The new address will also be available in the current profile:

    <pre>NSArray *addresses = [PTKProfileManager sharedManager].currentProfile.addresses;</pre>

<br />

# Updating an Address

1. Create a PTKAddressDetails object from an existing PTKAddress and modify the address information:

    <pre>PTKAddressDetails *modifiedAddress = [address editableCopy];
   modifiedAddress.alias = @"110 Bishopsgate";</pre>

2. Validate the address details

	Use the details described in step 2 of [Adding an Address]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/profile/#adding-an-address) to verify the properties of <code>AddressDetails</code>.

3. Use PTKProfileManager to update the address information:

    <pre>PTKProfileManager *pm = [PTKProfileManager sharedManager];
   [pm updateAddress:address addressDetails:modifiedAddress completion:^(PTKAddress *updatedAddress, NSError *error) {
     if (updatedAddress) {
       // Address was successfully updated
     }
   }];</pre>

<br />

# Deleting an Address

1. Use PTKProfileManager to delete an existing address:

    <pre>PTKProfileManager *pm = [PTKProfileManager sharedManager];
   [pm deleteAddress:address, completion:^(PTKProfile *updatedProfile, NSError *error) {
     if (updatedProfile) {
       // Address was successfully deleted from profile
     }
   }];</pre>

<br />

# Adding a Payment Instrument

1. Create a new PaymentMethodDetails object and set the card information:

    <pre>PTKPaymentMethodDetails *paymentMethodDetails = [PTKPaymentMethodDetails paymentMethodDetails];
   paymentMethodDetails.cardHolderName = @"Joe Bloggs";
   paymentMethodDetails.cardNumber = @"4111111111111111";
   paymentMethodDetails.validFromDate = [PTKYearMonth yearMonthWithYear:2010 month:1];
   paymentMethodDetails.expiryDate = [PTKYearMonth yearMonthWithYear:2020 month:1];</pre>

2. Validate the payment method details

	Use <code>PTKPaymentMethodDetailsValidator</code> to verify that all payment method details have been entered correctly.

	<pre>PTKPaymentMethodDetailsValidator *paymentMethodDetailsValidator = [PTKPaymentMethodDetailsValidator new];
	NSError *errors = [paymentMethodDetailsValidator validate:paymentMethodDetails];
	if (errors) {
		for (PTKValidationFailure *validationFailure in invalidData) {
			NSString *property = validationFailure.propertyName;
			PTKValidationError *errorCode = validationFailure.errorCode;
			// Display validation to user and obtain an updated value
		}
	} else {
		// No issues found while validating the payment details
	}</pre>

	For more information on validators please see the [Validators]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/validators/) page. <br />

3. Create a new PaymentInstrumentDetails object and set the payment instrument, billing address and other information:

	<pre>[PTKPaymentInstrumentDetails *paymentInstrument = [PTKPaymentInstrumentDetails paymentInstrumentDetailsWithPaymentType:PTKCreditCardIssuerVisa
	paymentMethod:paymentMethodDetails
	paymentType:PTKPaymentMethodTypeCard
	billingAddressId:addressId];</pre>

4. Add the payment instrument to the user profile using the PTKProfileManager:

    <pre>PTKProfileManager *pm = [PTKProfileManager sharedManager];
   [pm addPaymentInstrument:paymentInstrument completion:^(PTKPaymentInstrument *addedPaymentInstrument, NSError *error) {
     if (addedPaymentInstrument) {
       // Payment instrument was successfully added
     }
   }];</pre>

5. If the payment instrument needs to be activated, send an activation code to the user.

	<strong> TODO: </strong> this is a Swift code sample, need to get an Objective-C from Tiago.

	<pre>if (paymentInstrument.activationStatus != PTKActivationStatusNotRequired) {
                [[PTKProfileManager sharedManager] sendActivationCodeForPaymentInstrument:paymentInstrument completion:^(NSError * _Nullable error) {
                    if (error != nil) {
                        // Handle error
                    } else {
                        // Inform user that activation code has been sent
                    }
                }];
            }
     </pre>

6. Once the user inputs the activation code, activate the payment instrument.

	<pre>[[PTKProfileManager sharedManager] activatePaymentInstrument:paymentInstrument withActivationCode:activationCode completion:^(PTKPaymentInstrument  _Nullable paymentInstrument, NSError  _Nullable error) {
        if (error != nil) {
            // Handle error
        } else {
            // Activation successful
        }
    }];
	</pre>
	<br />
	
7. The new payment method will also be available in the current profile:

    <pre>NSArray *paymentInstruments = [PTKProfileManager sharedManager].currentProfile.paymentInstruments;</pre>

<br />

# Updating a Payment Instrument

You can only change the billing address of a payment instrument once created.

1. Use PTKProfileManager to update the billing address of a payment instrument:

    <pre>PTKProfileManager *pm = [PTKProfileManager sharedManager];
   [pm updatePaymentInstrument:paymentInstrument billingAddress:newBillingAddress, completion:^(PTKPaymentInstrument *updatedPaymentInstrument, NSError *error) {
     if (updatedPaymentInstrument) {
       // Payment instrument was successfully updated
     }
   }];</pre>

<br />

# Deleting a Payment Instrument

1. Use PTKProfileManager to delete an existing payment instrument:

    <pre>PTKProfileManager *pm = [PTKProfileManager sharedManager];
   [pm deletePaymentInstrument:paymentInstrument, completion:^(PTKProfile *updatedProfile, NSError *error) {
     if (updatedProfile) {
       // Payment instrument was successfully deleted from profile
     }
   }];</pre>

<br />

# Updating the Profile

1. Create a new ProfileDetails object and set the profile information:

	<pre>PTKProfileDetails *profileDetails = [PTKProfileDetails profileDetailsWithTitle:@"M"
	firstName:@"Joe"
	lastName:@"Bloggs"
	email:@"joebloggs@powa.com"
	mobileNumber:@"01234567890"
	defaultAddress:defaultAddress
	defaultPaymentInstrument:paymentInstrument
	customDataValues:@[customDataValue, customDataValue2]];</pre>

2. Validate the profile details

	Use <code>PTKProfileDetailsValidator</code> to verify that all profile details have been entered correctly.

	<pre>PTKProfileDetailsValidator *profileDetailsValidator = [PTKProfileDetailsValidator new];
	NSError *errors = [profileDetailsValidator validate:profileDetails];
	if (errors) {
		for (PTKValidationFailure *validationFailure in invalidData) {
			NSString *property = validationFailure.propertyName;
			PTKValidationError *errorCode = validationFailure.errorCode;
			// Display validation to user and obtain an updated value
		}
	} else {
		// No issues found while validating the profile details
	}</pre>

	For more information on validators please see the [Validators]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/validators/) page. <br />
	
3. Use the PTKProfileManager to update the current profile:

    <pre>PTKProfileManager *pm = [PTKProfileManager sharedManager];
   [pm updateProfileWithProfileDetails:profile completion:^(PTKProfile *updatedProfile, NSError *error) {
     if (!error) {
       // Profile information is updated
     }
   }];</pre>

4. The updated profile information will be reflected in the users current profile:

    <pre>PTKProfile *profile = [PTKProfileManager sharedManager].currentProfile;</pre>

# Saving the Profile

1. Use the PTKProfileManager to save the current profile:

	<pre>PTKProfileManager *pm = [PTKProfileManager sharedManager];
	[pm saveProfileWithPassword:@"password"
	completion:^(PTKProfile *savedProfile, NSError *error) {
		if (savedProfile) {
			// Profile is no longer temporary
		}
	}];</pre>

