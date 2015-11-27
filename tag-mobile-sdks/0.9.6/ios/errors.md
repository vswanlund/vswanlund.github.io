---
layout: page
title: iOS SDK Error Handling
permalink: /tag-mobile-sdks/0.9.6/ios/errors/
---

To build a robust and reliable app you want to make sure that it properly responds to errors.

This guide covers features that the PowaTag SDK for iOS provides to help you do this.

<br />

# Error Handling and Recovery

The SDK defines a `PTKErrors.h` file which defines all error codes used by the SDK. You should display only the localized messages as errors.

Each error may have an underlying cause, this can be determined by inspecting the `userInfo` dictionary for `NSUnderlyingErrorKey`.

Additionally extra information will be available in the `userInfo` dictionary for certain errors:

Key                    | Codes                         | Description
-----------------------|-------------------------------|---------------------------
NSUnderlyingErrorKey   | Any                           | Underlying NSError, if any
-----------------------|-------------------------------|---------------------------
PTKErrorMessageKey     | Any                           | Optional error message
-----------------------|-------------------------------|---------------------------
PTKErrorDescriptionKey | Any                           | Description of the error
-----------------------|-------------------------------|---------------------------
PTKHTTPStatusCodeKey   | PTKPowaTagHttpErrorCode,      | Dictionary key for HTTP status code
                       | PTKPowaTagServiceErrorCode,   |
                       | PTKPowaTagNotFoundErrorCode,  |
                       | PTKPowaTagValidationErrorCode |
-----------------------|-------------------------------|---------------------------
PTKServiceErrorsKey    | PTKPowaTagServiceErrorCode,   | Array of PTKServiceErrors
                       | PTKPowaTagNotFoundErrorCode,  |
                       | PTKPowaTagValidationErrorCode |
-----------------------|-------------------------------|---------------------------
PTKUnsupportedTypeKey  | PTKPowaTagUnsupportedWorkflowTypeErrorCode, | The unsupported type/value as a string
                       | PTKPowaTagUnsupportedCustomValueTypeErrorCode, |
                       | PTKPowaTagUnsupportedPaymentMethodTypeErrorCode, |
                       | PTKPowaTagUnsupportedCardIssuerErrorCode |

<br />


The error codes produced by the SDK:

Error                      | Code 	| Description
---------------------------|--------|--------------
PTKPowaTagGenericErrorCode | 1 		| Generic error.
---------------------------|--------|--------------
PTKPowaTagNetworkErrorCode | 2 		| Indicates a generic network problem.
---------------------------|--------|--------------
PTKPowaTagHttpErrorCode    | 3 | Indicates an HTTP error response was received from the server.
---------------------------|--------|--------------
PTKPowaTagServiceErrorCode | 4 | Service specific error.
---------------------------|--------|--------------
PTKPowaTagNetworkTimeoutErrorCode | 8 | Indicates the network operation took too long to complete and was aborted.
---------------------------|--------|--------------
PTKPowaTagNoInternetConnectionErrorCode | 9 | Indicates no internet connection is available.
---------------------------|--------|--------------
PTKPowaTagAuthorizationErrorCode | 10 | Indicates an attempt to make an API request without proper authorization such as trying to access a protected API before logging in.
---------------------------|--------|--------------
PTKPowaTagInvalidTagFormatErrorCode | 11 | Indicates that the host name is not a supported host for QR format tags.
---------------------------|--------|--------------
PTKPowaTagNotFoundErrorCode | 12 | Indicates a resource could not be found.
---------------------------|--------|--------------
PTKPowaTagServiceValidationErrorCode | 13 | Indicates a validation issue with a request sent to a service.
---------------------------|--------|--------------
PTKPowaTagCancellationErrorCode | 14 | Indicates an asynchronous operation was cancelled.
---------------------------|--------|--------------
PTKPowaTagSerializationErrorCode | 15 |	Indicates a generic issue serializing or deserializing data.
---------------------------|--------|--------------
PTKPowaTagInvalidDonationAmountErrorCode | 16 | Indicates an invalid donation amount, for instance when specifying an amount that is not one of <code>PTKCampaign.suggestedAmounts</code> when <code>PTKCampaign.isCustomAmountAllowed</code> is not true.
---------------------------|--------|--------------
PTKPowaTagUndefinedPropertySerializationErrorCode | 17 | Indicates a response could not be deserialized because a required property is undefined.
---------------------------|--------|--------------
PTKPowaTagUnsupportedWorkflowTypeErrorCode | 18 | Indicates a workflow type is not supported in the current version of the SDK. You should check for upgrades to the SDK to enable support for this workflow type.
---------------------------|--------|--------------
PTKPowaTagUnsupportedCustomValueTypeErrorCode | 19 | Indicates a merchant requires a custom value type that is not supported in the current version of the SDK. You should check for upgrades to the SDK to enable support for this merchant.
---------------------------|--------|--------------
PTKPowaTagUnsupportedPaymentMethodTypeErrorCode | 20 | Indicates a payment method type that is not supported in the current version of the SDK.   You should check for upgrades to the SDK to enable support for this payment method type.
---------------------------|--------|--------------
PTKPowaTagUnsupportedCardIssuerErrorCode | 21 | Indicates a card issuer that is not supported in the current version of the SDK.   You should check for upgrades to the SDK to enable support for this card issuer.
---------------------------|--------|--------------
PTKPowaTagOutOfStockErrorCode | 22 | Indicates a product is out of stock.
---------------------------|--------|--------------
PTKPowaTagUnsupportedActValueTypeErrorCode | 23 | Indicates an Act campaign requires a data type that is not supported in the current version of the SDK.   You should check for upgrades to the SDK to enable support for this Act campaign.
---------------------------|--------|--------------
PTKPowaTagMissingRequiredActDataValueErrorCode | 24 | Indicates an attempt to submit values for an act campaign where one or more non-optional values are not present. Which values are optional is specified in <code>PTKAct.actDataKeys</code> and <code>PTKActDataKey.optional</code>.
	
<br />

The following code snippet provided an example of handling an error:

	<pre>PTKProfileManager *profileManager = [PTKProfileManager sharedManager];
	PTKSignUpDetails *signUpDetails = [PTKSignUpDetails signUpDetailsWithPassword:suppliedPassword];

	[profileManager saveProfileWithPassword:signUpDetails
								 completion:^(PTKProfile *__nullable profile, NSError *__nullable error)
	 {
		 // Check for errors
		if (error != nil) {
			// Check for authorization error
			if (error.code == PTKPowaTagAuthorizationErrorCode) {
				// Obtain API errors
				NSArray *array = error.userInfo[PTKServiceErrorsKey];

				for (PTKServiceError *serviceError in array) {
					// Check if email address is already used by an existing profile
					if (serviceError.code == 409100) {
						// obtain new email address from user
					}
				}
			}	
		}
	 }];</pre>

	
<br />

# Error Codes

The following table lists out the errors that you might encounter when handling PTKServiceError.

Group 			| Error Code	|  Response status 	| Error Message | Info
----------------|---------------|-------------------|---------------|---------
Authorization 	| 401100 		| 401 				| User is not allowed to be authorised. | Occurs if the user credentials don't exist in DB or auth token expired.
----------------|---------------|-------------------|---------------|---------
Authorization 	| 403100 		| 403 				| Access denied | 
----------------|---------------|-------------------|---------------|---------
Authorization 	| 404100 		| 404 				| Access token not found. | Occurs when provided credentials are checked and user token doesn't exist in DB.
----------------|---------------|-------------------|---------------|---------
Authorization 	| 404101 		| 404 				| User not found | 
----------------|---------------|-------------------|---------------|---------
Authorization 	| 409100 		| 409 				| E-mail already exists. | An Attempt to save a temp profile using an email that already exists for a permanent profile will receive this error.
----------------|---------------|-------------------|---------------|---------
Authorization 	| 409100 		| 409 				| Profile already registered. | 
----------------|---------------|-------------------|---------------|---------
Merchant 		| 404400 		| 404 				| Merchant not found. | Most likely encountered when trying to obtain the workflow after a trigger or while making a payment.
----------------|---------------|-------------------|---------------|---------
Merchant 		| 404401 		| 404 				| Merchant logo not found | 
----------------|---------------|-------------------|---------------|---------
Merchant 		| 404402 		| 404 				| Merchant location not found | 
----------------|---------------|-------------------|---------------|---------
Merchant 		| 400403 		| 400 				| Merchant does not support charity. | Thrown when attempt to create new Donation for Merchant that has the 'charity'  flag set to false.
----------------|---------------|-------------------|---------------|---------
Merchant 		| 404405 		| 404 				| Geo coordinates of location not found | 
----------------|---------------|-------------------|---------------|---------
Workflow 		| 400500 		| 400 				| Provided tag type is not supported | 
----------------|---------------|-------------------|---------------|---------
Workflow 		| 400504 		| 400 				| Provided workflow type is not supported | 
----------------|---------------|-------------------|---------------|---------
Workflow 		| 400505 		| 400 				| Tag cannot be generated for the found Workflow type | 
----------------|---------------|-------------------|---------------|---------
Workflow 		| 404500 		| 404 				| Tag not found | 
----------------|---------------|-------------------|---------------|---------
Workflow 		| 409500 		| 409 				| Tag already exists.  | Occurs if and attempt is made to create a workflow and using an existing workflow ID in the request
----------------|---------------|-------------------|---------------|---------
Workflow 		| 400501 		| 400 				| Error while generating barcode | 
----------------|---------------|-------------------|---------------|---------
Workflow 		| 400502 		| 400 				| Provided tag type is invalid | 
----------------|---------------|-------------------|---------------|---------
Donation 		| 404600 		| 404 				| Campaign not found | 
----------------|---------------|-------------------|---------------|---------
Basket 			| 400701 		| 400 				| Basket is empty | 
----------------|---------------|-------------------|---------------|---------
Basket 			| 404700 		| 404 				| Basket not found | 
----------------|---------------|-------------------|---------------|---------
Basket 			| 404701 		| 404 				| Update parameters mismatch | 
----------------|---------------|-------------------|---------------|---------
Transaction 	| 404900 		| 404 				| Transaction not found | 
----------------|---------------|-------------------|---------------|---------
Profile 		| 400800 		| 400 				| Payment instrument hash key is invalid | 
----------------|---------------|-------------------|---------------|---------
Profile 		| 400801 		| 400 				| Profile passcode is invalid.  | Every profile has a ‘passcode’ field that can be updated by updateProfile. This passcode is used for authorizing invoice.
----------------|---------------|-------------------|---------------|---------
Profile 		| 404800 		| 404 				| Profile not found | 
----------------|---------------|-------------------|---------------|---------
Profile 		| 404801 		| 404 				| Address not found | 
----------------|---------------|-------------------|---------------|---------
Profile 		| 404802 		| 404 				| Payment instrument not found | 
----------------|---------------|-------------------|---------------|---------
Profile 		| 409801 		| 409 				| Address can't be verified | 
----------------|---------------|-------------------|---------------|---------
Profile 		| 409803 		| 409 				| Profile already exists | 
----------------|---------------|-------------------|---------------|---------
Profile 		| 500800 		| 500 				| Key Generator initialization exception | 
----------------|---------------|-------------------|---------------|---------
Transaction 	| 403900 		| 403 				| User is not of type Merchant | 
----------------|---------------|-------------------|---------------|---------
Transaction 	| 400900 		| 400 				| Transaction step type not correct | 
----------------|---------------|-------------------|---------------|---------
Transaction 	| 400901 		| 400 				| Transaction step body not correct | 
----------------|---------------|-------------------|---------------|---------
Act 			| 404210 		| 404 				| Act not found | 
----------------|---------------|-------------------|---------------|---------
Act 			| 500292 		| 500 				| Act transaction was not created | 
----------------|---------------|-------------------|---------------|---------
Act 			| 400298 		| 400 				| Act transaction values don't pass validation | 
----------------|---------------|-------------------|---------------|---------
Category 		| 404220 		| 404 				| Category not found.  | Can occur when:
 |   |  |   |  - Creating a workflow for non-existing categoryId
 |   |  |   |  - Getting a category by ID
 |   |  |   |  - Getting a category workflow by ID
----------------|---------------|-------------------|---------------|---------
Shipping 		| 404241 		| 404 				| Shipping option not found | 
----------------|---------------|-------------------|---------------|---------
Product 		| 403280 		| 403 				| Forbidden product not found. | If during a basket update a product SKU is no longer found.
----------------|---------------|-------------------|---------------|---------
Product 		| 404280 		| 404 				| Product not found | 
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 400293 		| 400 				| Invalid product id | 
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 400294 		| 400 				| Fulfillment invalid quantities | 
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 400299 		| 400 				| Fulfillment option order already exists | 
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 400301 		| 400 				| Fulfillment options order field value exceeds maximum. | Each fulfillment order has an order field with determines position in queue. If this exceeds the max value you will encounter this error. Max is currently set to 21474836747
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 403290 		| 403 				| Order already collected | 
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 404290 		| 404 				| Fulfillment order not found | 
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 404291 		| 404 				| Product fulfillment not found. |  When trying to fulfill products and passing product ID that does not exists in specified fulfillment order.
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 404293 		| 404 				| Applicable fulfillment options for current merchant not found.  | Can occur when a basket cost is calculated and the provided fulfillment option ID does not exist.
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 409290 		| 409 				| Order already exits | 
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 400297 		| 400 				| Orders have duplicated 'orderId' fields.  | Occurs when storing fulfillment orders and there are multiple orders with an identical orderId in orders list.
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 500292 		| 500 				| Fulfillment is missing in order | 
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 404292 		| 404 				| Check-in point not found.  | When trying to check-in and the provided check-in point does not exist.
----------------|---------------|-------------------|---------------|---------
Fulfillment 	| 409295 		| 409 				| Profile already exists in the queue.  | When an attempt is made to check-in twice
----------------|---------------|-------------------|---------------|---------
General 4xx 	| 400000 		| 400 				| Bad request error | 
----------------|---------------|-------------------|---------------|---------
General 4xx 	| 400001 		| 400 				| Error validating against XSD schema | 
----------------|---------------|-------------------|---------------|---------
General 4xx 	| 400002 		| 400 				| Json mapping error | 
----------------|---------------|-------------------|---------------|---------
General 4xx 	| 401000 		| 401 				| Unauthorized | 
----------------|---------------|-------------------|---------------|---------
General 4xx 	| 404000 		| 404 				| Not found | 
----------------|---------------|-------------------|---------------|---------
General 4xx 	| 405000 		| 405 				| Method not allowed error | 
----------------|---------------|-------------------|---------------|---------
General 5xx 	| 500000 		| 500 				| Internal server error | 
----------------|---------------|-------------------|---------------|---------
General 5xx 	| 500001 		| 500 				| Data access error | 
----------------|---------------|-------------------|---------------|---------
General 5xx 	| 500002 		| 500 				| Wrong Extension error | 
----------------|---------------|-------------------|---------------|---------
General 5xx 	| 500003 		| 500 				| Powaim error | 
----------------|---------------|-------------------|---------------|---------
General 5xx 	| 500004 		| 500 				| Legacy powaim error | 
----------------|---------------|-------------------|---------------|---------
General 5xx 	| 500005 		| 500 				| Sending mail error | 



<BR />