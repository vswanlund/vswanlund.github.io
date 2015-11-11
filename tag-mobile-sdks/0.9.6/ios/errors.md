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
                       | PTKPowaTagUnsupportedPaymentMethodTypeErrorCode,
                       | PTKPowaTagUnsupportedCardIssuerErrorCode |

<br />



# Error Codes

The 

Error                      | Code 	| Description
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
PTKPowaTagInvalidDonationAmountErrorCode | 16 | Indicates an invalid donation amount, for instance when specifying an amount that is not one of {@link PTKCampaign#suggestedAmounts} when {@link PTKCampaign#isCustomAmountAllowed} is not true.
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
PTKPowaTagMissingRequiredActDataValueErrorCode | 24 | Indicates an attempt to submit values for an act campaign where one or more non-optional values are not present. Which values are optional is specified in {@link PTKAct#actDataKeys} and {@link PTKActDataKey#optional}.
	



 
<br />

# Error Codes
The following table lists out the errors that you might encounter when handling PTKServiceError.

Group 			| Error Code	|  Response status 	| Info
----------------|---------------|-------------------|-------
Authorization 	| 401100 		| 401 				| User is not allowed to be authorised
----------------|---------------|-------------------|-------
Authorization 	| 403100 		| 403 				| Access denied
----------------|---------------|-------------------|-------
Authorization 	| 404100 		| 404 				| Access token not found
----------------|---------------|-------------------|-------
Authorization 	| 404101 		| 404 				| User not found
----------------|---------------|-------------------|-------
Authorization 	| 409100 		| 409 				| E-mail already exists
----------------|---------------|-------------------|-------
Authorization 	| 409100 		| 409 				| Mobile Number already exists
----------------|---------------|-------------------|-------
Authorization 	| 409100 		| 409 				| Profile already registered
----------------|---------------|-------------------|-------
Merchant 		| 404400 		| 404 				| Merchant not found
----------------|---------------|-------------------|-------
Merchant 		| 404401 		| 404 				| Merchant logo not found
----------------|---------------|-------------------|-------
Merchant 		| 404402 		| 404 				| Merchant location not found
----------------|---------------|-------------------|-------
Merchant 		| 400403 		| 400 				| Merchant does not support charity
----------------|---------------|-------------------|-------
Merchant 		| 404404 		| 404 				| Geo coordinates of address not found
----------------|---------------|-------------------|-------
Merchant 		| 404405 		| 404 				| Geo coordinates of location not found
----------------|---------------|-------------------|-------
Merchant 		| 409400 		| 409 				| Merchant already exists
----------------|---------------|-------------------|-------
Workflow 		| 400500 		| 400 				| Provided tag type is not supported
----------------|---------------|-------------------|-------
Workflow 		| 400504 		| 400 				| Provided workflow type is not supported
----------------|---------------|-------------------|-------
Workflow 		| 400505 		| 400 				| Tag cannot be generated for the found Workflow type
----------------|---------------|-------------------|-------
Workflow 		| 404500 		| 404 				| Tag not found
----------------|---------------|-------------------|-------
Workflow 		| 409500 		| 409 				| Tag already exists
----------------|---------------|-------------------|-------
Workflow 		| 400501 		| 400 				| Error while generating barcode
----------------|---------------|-------------------|-------
Workflow 		| 400502 		| 400 				| Provided tag type is invalid
----------------|---------------|-------------------|-------
Workflow 		| 400503 		| 400 				| Location id provided is not found in the merchant locations list
----------------|---------------|-------------------|-------
Donation 		| 404600 		| 404 				| Campaign not found
----------------|---------------|-------------------|-------
Basket 			| 400701 		| 400 				| Basket is empty
----------------|---------------|-------------------|-------
Basket 			| 404700 		| 404 				| Basket not found
----------------|---------------|-------------------|-------
Basket 			| 404701 		| 404 				| Update parameters mismatch
----------------|---------------|-------------------|-------
Transaction 	| 404900 		| 404 				| Transaction not found
----------------|---------------|-------------------|-------
Profile 		| 400800 		| 400 				| Payment instrument hash key is invalid
----------------|---------------|-------------------|-------
Profile 		| 400801 		| 400 				| Profile passcode is invalid
----------------|---------------|-------------------|-------
Profile 		| 404800 		| 404 				| Profile not found
----------------|---------------|-------------------|-------
Profile 		| 404801 		| 404 				| Address not found
----------------|---------------|-------------------|-------
Profile 		| 404802 		| 404 				| Payment instrument not found
----------------|---------------|-------------------|-------
Profile 		| 409801 		| 409 				| Address can't be verified
----------------|---------------|-------------------|-------
Profile 		| 409803 		| 409 				| Profile already exists
----------------|---------------|-------------------|-------
Profile 		| 500800 		| 500 				| Key Generator initialization exception
----------------|---------------|-------------------|-------
Transaction 	| 403900 		| 403 				| User is not of type Merchant
----------------|---------------|-------------------|-------
Transaction 	| 404900 		| 404 				| Transaction not found
----------------|---------------|-------------------|-------
Transaction 	| 400900 		| 400 				| Transaction step type not correct
----------------|---------------|-------------------|-------
Transaction 	| 400901 		| 400 				| Transaction step body not correct
----------------|---------------|-------------------|-------
Act 			| 404210 		| 404 				| Act not found
----------------|---------------|-------------------|-------
Act 			| 500292 		| 500 				| Act transaction was not created
----------------|---------------|-------------------|-------
Act 			| 400298 		| 400 				| Act transaction values don't pass validation
----------------|---------------|-------------------|-------
Category 		| 404220 		| 404 				| Category not found
----------------|---------------|-------------------|-------
Category 		| 404221 		| 404 				| Catalog not found
----------------|---------------|-------------------|-------
Category 		| 409220 		| 409 				| Category already exists
----------------|---------------|-------------------|-------
Category 		| 409221 		| 409 				| Catalog already exists for this merchant
----------------|---------------|-------------------|-------
Sync 			| 404231 		| 404 				| Job not found
----------------|---------------|-------------------|-------
Sync 			| 404232 		| 404 				| Specified job type not found
----------------|---------------|-------------------|-------
Sync 			| 400404 		| 400 				| Google api server responded with an error status
----------------|---------------|-------------------|-------
Shipping 		| 404241 		| 404 				| Shipping option not found
----------------|---------------|-------------------|-------
Product 		| 403280 		| 403 				| Forbidden product not found
----------------|---------------|-------------------|-------
Product 		| 404280 		| 404 				| Product not found
----------------|---------------|-------------------|-------
Product 		| 409280 		| 409 				| Product already exists
----------------|---------------|-------------------|-------
Product 		| 400280 		| 400 				| Illegal product pagination
----------------|---------------|-------------------|-------
Fulfillment 	| 400290 		| 400 				| Fulfillment reference doesn't match with order reference
----------------|---------------|-------------------|-------
Fulfillment 	| 400291 		| 400 				| Transaction is not completed to be fulfilled
----------------|---------------|-------------------|-------
Fulfillment 	| 400292 		| 400 				| Invalid MerchantId. Request merchantId doesn't match with expected merchantId
----------------|---------------|-------------------|-------
Fulfillment 	| 400293 		| 400 				| Invalid product id
----------------|---------------|-------------------|-------
Fulfillment 	| 400294 		| 400 				| Fulfillment invalid quantities
----------------|---------------|-------------------|-------
Fulfillment 	| 400295 		| 400 				| Invalid check-in because there is no transaction for that user
----------------|---------------|-------------------|-------
Fulfillment 	| 400296 		| 400 				| Fulfillment is missing in order
----------------|---------------|-------------------|-------
Fulfillment 	| 400299 		| 400 				| Fulfillment option order already exists
----------------|---------------|-------------------|-------
Fulfillment 	| 400301 		| 400 				| Fulfillment options order field value exceeds maximum
----------------|---------------|-------------------|-------
Fulfillment 	| 403290 		| 403 				| Order already collected
----------------|---------------|-------------------|-------
Fulfillment 	| 404290 		| 404 				| Fulfillment order not found
----------------|---------------|-------------------|-------
Fulfillment 	| 404291 		| 404 				| Product fulfillment not found
----------------|---------------|-------------------|-------
Fulfillment 	| 404293 		| 404 				| Applicable fulfillment options for current merchant not found
----------------|---------------|-------------------|-------
Fulfillment 	| 409290 		| 409 				| Order already exits
----------------|---------------|-------------------|-------
Fulfillment 	| 400297 		| 400 				| Orders have duplicated 'orderId' fields
----------------|---------------|-------------------|-------
Fulfillment 	| 500290 		| 500 				| Check-in point internal error
----------------|---------------|-------------------|-------
Fulfillment 	| 500291 		| 500 				| The check-in point is full please try again later
----------------|---------------|-------------------|-------
Fulfillment 	| 500292 		| 500 				| Fulfillment is missing in order
----------------|---------------|-------------------|-------
Fulfillment 	| 409291 		| 409 				| Check-in point already exists
----------------|---------------|-------------------|-------
Fulfillment 	| 404292 		| 404 				| Check-in point not found
----------------|---------------|-------------------|-------
Fulfillment 	| 409295 		| 409 				| Profile already exists in the queue
----------------|---------------|-------------------|-------
General 4xx 	| 400000 		| 400 				| Bad request error
----------------|---------------|-------------------|-------
General 4xx 	| 400001 		| 400 				| Error validating against XSD schema
----------------|---------------|-------------------|-------
General 4xx 	| 400002 		| 400 				| Json mapping error
----------------|---------------|-------------------|-------
General 4xx 	| 401000 		| 401 				| Unauthorized
----------------|---------------|-------------------|-------
General 4xx 	| 404000 		| 404 				| Not found
----------------|---------------|-------------------|-------
General 4xx 	| 405000 		| 405 				| Method not allowed error
----------------|---------------|-------------------|-------
General 5xx 	| 500000 		| 500 				| Internal server error
----------------|---------------|-------------------|-------
General 5xx 	| 500001 		| 500 				| Data access error
----------------|---------------|-------------------|-------
General 5xx 	| 500002 		| 500 				| Wrong Extension error
----------------|---------------|-------------------|-------
General 5xx 	| 500003 		| 500 				| Powaim error
----------------|---------------|-------------------|-------
General 5xx 	| 500004 		| 500 				| Legacy powaim error
----------------|---------------|-------------------|-------
General 5xx 	| 500005 		| 500 				| Sending mail error



<BR />

# General Exceptions
The following exceptions can be encountered at any time.

**[PowaTagNetworkException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_network_exception.html)**<br /> 
Indicates a generic network problem.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b> This exception can be encountered at any time.

<br />		    


**[PowaTagNetworkTimeoutException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_network_timeout_exception.html)**<br /> 
Indicates the network operation took too long to complete and was aborted.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b> This exception can be encountered at any time.

<br />

**[PowaTagNoInternetConnectionException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_no_internet_connection_exception.html)**<br /> 
Indicates no internet connection is available.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b> This exception can be encountered at any time.

<br />

**IllegalStateException**<br/>
Indicates that a blocking method has been called in the main thread 


<br />