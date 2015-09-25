---
layout: page
title: Windows Phone SDK Change Log
permalink: /tag-mobile-sdks/wp/changelog/
---

Change log and release notes for the PowaTag SDK for Windows Phone.

<br />

# 0.9.0 - Sep 7th, 2015

**Added**

* Simple value validators.
* Property validators.
* SDK build SHA available through PowaTagKit.
* Added InvoiceBasket to represent unmodifiable basket.
* API keys.

**Modified**

* Renamed BasketWorkflow to TemporaryBasketWorkflow.
* Improved PowaTagUnsupportedCustomDataTypeException error message.
* Manager parameters are now supplied through a Details object.
* PowaTagQrCode is no longer parcelable/serializable.
* Renamed Touch2BuyTagDetector to AppLinkTagDetector.

<br />

# 0.8.5 - Aug 11th, 2015

**Added**

* Added PowaTagOutOfStockException to indicate stock issues on payment.
* Added Gift Aid and recurring options to CampaignManager.
* Added support for Diners Club International issuer.
* Added product metadata including condition, brand and categories.
* Added YearMonth class to represent credit card dates.

**Fixed**

* Fixed multiple minor issues in the sample app.
* Payment for TemporaryBasket.
* Added handling for unknown/invalid required enum parameters.
* Unknown issuer correctly returns 12 and 19 for min/max card lengths.
* Address state not properly saved.
* Custom data key and value for custom profile values.
* Fixed issue where product variant attributes were always empty.

**Modified**

* When logging out, all ongoing requests are now immediately cancelled.
* PaymentMethodType is renamed to PaymentType.
* ShippingOption shippingPrice is renamed to price.
* Invoice now stores objects rather than just IDs.
* Country is now a class rather than an enum.
* CreditCardIssuer is now a class rather than an enum.
* Credit card holder name now allows lowercase.

<br />

# 0.8.0 - Aug 11th, 2015

**Added**

* Added phone number validation to ProfileValidator.
* Added support to PaymentManager for making a payment for a DonationInvoice.
* Added support to BasketManager for creating an invoice for a temporary basket.
* Added Profile.HasRequiredInfo(Merchant) to check if profile has all information needed by merchant.
* Added Profile.EditableCopy to allow easily editing the current profile details.
* Added Product title and description.
* Added HelloPowaTagSample Donation workflow.
* Added HelloPowaTagSample TemporaryBasket workflow.

**Fixed**

* CampaignManager allows providing the amount in correct format.
* DonationInvoice contains correct amount information.

**Modified**

* ProfileManager saveProfile now accepts user password.
* Workflow is now split into subclasses ProductWorkflow, CampaignWorkflow and BasketWorkflow.
* Country is now an enumeration of available countries.
* PresetBasket renamed to TemporaryBasket and UserBasket renamed to PersistentBasket.
* Profile ID property has been moved from Basket to PersistentBasket subclass.

**Removed**

* Country name has been removed.

**Known Issues**

* Payment for TemporaryBasket does not work correctly.

<br />

# 0.7.0 - July 28th, 2015

**Added**

* Added custom values to Profile.
* Added Basket Workflow.
* Added Campaign & CampaignManager for Donations.
* Added PaymentManager support for donations.
* Added ProfileManager save profile functionality.
* Added ProfileManager updateAddress.
* Added ProfileManager deleteAddress.
* Added ProfileManager updatePaymentInstrument.
* Added ProfileManager deleteAddress.
* Added Discover, Maestro and China UnionPay credit card issuers.
* Added Unknown CreditCardIssuer.
* Added CreditCardValidator card security code validation.
* Added CreditCardIssuer card length properties.
* Added CreditCardValidator general year and month validation.
* Added PowaTagNotFoundException.
* Added PowaTagValidationException.

**Fixed**

* First address or payment instrument added should become the default address or payment instrument for the user profile.
* Fixed audio tag detection issue with tags starting 0.

**Modified**

* Basket is now split into PresetBasket and UserBasket, with common Basket superclass.
* BasketsManager methods accept/return a UserBasket.
* Invoice is now split into PaymentInvoice and DonationInvoice, with common Invoice superclass.
* Invoice shippingAddress, shippingOption, basketId and items have been moved to PaymentInvoice class.
* HelloPowaTagSample is portrait only.
* Profile getAcceptedPaymentMethods renamed to getAcceptedPaymentInstruments.
* AcceptedPaymentMethod renamed to AcceptedPaymentInstrument.
* Merchant paymentMethods property renamed to paymentInstruments.
* CreditCardValidator issuer methods return Unknown issuer instead of null.
* Credit card holder name validation updated, lowercase chars are no longer valid.
* Email validation updated so "test@test." is no longer valid.
* Validators moved from Sdk.Validator namespace to Sdk namespace.

**Removed**

* Removed ProductVariant merchantId property.

<br />

# 0.6.0 - July 14th, 2015

**Added**

* Merchant required profile information.
* Added PosManager for POS terminals to generate basket QRs.
* Added validation routines for email, first name and last name.
* Added Tag parse method for audio tags.

**Fixed**

* Nuspec generation.

**Modified**

* Managers from api package to sdk.
* ProfileManager add address and card methods return address and cards objects.
* Address renamed to AddressDetails and AddressAlias renamed to Address.
* PaymentMethod renamed to PaymentInstrumentDetails and PaymentMethodAlias renamed to PaymentInstrument.
* PaymentInstrument renamed to PaymentMethodDetails.
* ProfileUpdate renamed to ProfileDetails.
* Baskets methods for managing baskets moved to BasketsManager.
* Renamed TagFormat members to be clearer.
* PowaTagEndpoint uses URL objects instead of strings.
* Current AccessToken, Basket and Profile methods to Managers.
* Current AccessToken, Basket and Profile methods throw an authorization exception instead of returning null.
* Renamed Tag parseLabel method to parseQrUrl for clarity.
* Updated ZXING dependency.

<br />

# 0.5.4 - July 8th, 2015

**Fixed**

* Issue making payments with MasterCard or AMEX.

<br />

# 0.5.3 - July 3rd, 2015

**Fixed**

* Fixed formatting of expiry month and year.
* Fixed encoding of encrypted payment instrument data.

<br />

# 0.5.1 - June 29, 2015

**Added**

* Added LoginManager.LogoutAsync to remove user profile.
* Added ProfileManager.UpdateProfileAsync to update user profile.
* Added ToString descriptions for models.

**Fixed**

* PowaTagClient checks content type of empty responses.
* If the profileId changes during the execution of an asynchronous operation the results will be discarded for security reasons.
* If an attempt is made to access a Manager before the SDK has been initialized an appropriate exception will be thrown.
* HelloPowaTagSample rotation bug.

**Modified**

* PowaTagKit.isInitialized renamed to isSdkInitialized.
* PowaTagEndpoint.defaultEndpointPorts throws an exception if the host contains a port.
* HelloPowaTagSample Checkout screen prevents a temporary user adding more than one address or card.

<br />

# 0.5.0 - June 19, 2015

**Added**

* Added BasketManager Invoice.
* Added PaymentManager.
* Added Basket and BasketItem price and pre-tax prices.
* Added Merchant shipping options.
* Added Profile.GetAcceptedPaymentMethods to return the intersection of the payment methods attached to a profile and those accepted by a merchant.
* Added issuer and type information to PaymentMethodAlias.
* Added ProductVariantPicker.IsOptionChosenForEveryChoice to determine whether an option has been chosen for each different option choice.
* Added interfaces to Managers for mocking.
* Added Product.HasOptionChoices to determine whether a product has options that need to be chosen.
* Added ProductOptionChoice.IsChosen and ProductOptionChoice.ChosenOption.
* Added Add Address Screen to HelloPowaTagSample.
* Added Add Payment Method Screen to HelloPowaTagSample.
* Added Checkout Screen to HelloPowaTagSample.
* Added Invoice Screen to HelloPowaTagSample.
* Added Noda Money dependency.

**Fixed**

* Fixed focus not working in Barcode trigger.
* Fixed HashCode calculations for mutable Basket and BasketItem types.
* Added missing documentation to public classes.
* AudioSample correctly stops detection when a tag is detected.

**Modified**

* Modified Address and PaymentMethod models.
* Updated PaymentMethodType enum to support only PaymentCard.
* Replaced Money data type with Noda Money implementation.
* ProfileManager now encrypts Address and PaymentMethod information before transmission.
* PowaTagKit.InitializeSdk now accepts a PowaTagEndpoint instance which includes host name and port information for each service.
* Touch2Buy trigger now correctly handles v1 and v3 format PowaTag URLs.
* Simplified the Touch2Buy trigger AppLink class.
* Product.GetOptionChoices now returns an already chosen option choice if the choice only has a single option.

**Removed**

* Address and PaymentMethod order.

**Known Issues**

* PaymentManager does not work.

<br />

# 0.4.0 - May 29, 2015

**Added**

* Added ProductVariantPicker to improve variant selection.
* Added Profile and ProfileManager.
* Added Basket costs.
* Added simple Credit Card validation.
* Added UK Address validation.
* Added AccessToken, Baskets and Profile changed events.

**Modified**

* Improved HelloPowaTagSample.

**Removed**

* ProductVariantFilter, an equivalent API is now exposed by Product.

<br />

# 0.3.0 - May 15, 2015

**Added**

* Added Login API surfaced as LoginManager.
* Added BasketManager synchronization.
* Added Merchant T&Cs and logo.
* Added ProductVariantFilter to assist in picking a variant.
* Added PowaTagNoInternetConnectionException.

**Modifed**

* Full merchant information available in Workflow.
* ProductOption now has a single value.
* Baskets are now manipulated through Baskets, instead of Basket.

<br />

# 0.2.0 - May 1, 2015

**Added**

* Added Workflows API surfaced as WorkflowManager.
* Added Baskets API surfaced as BasketManager and Baskets.

**Known Issues**

* You must manually set a current access token with the desired user/consumer ID before using BasketManager because login functionality is missing.

    <pre>if (AccessToken.CurrentAccessToken == null) {
    AccessToken.CurrentAccessToken = new AccessToken("3451231");
    // Set a set of empty baskets for the user.
    Baskets.CurrentBaskets = new Baskets();
  }</pre>
