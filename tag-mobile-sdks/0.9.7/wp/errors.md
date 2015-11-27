---
layout: page
title: Windows Phone SDK Error Handling
permalink: /tag-mobile-sdks/0.9.7/wp/errors/
---

To build a robust and reliable app you want to make sure that it properly responds to errors.

This guide covers features that the PowaTag SDK provides to help you do this.

<br />

# SDK Exceptions

The SDK [Reference Docs]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/) provide the details of every method including parameters and exceptions.

As and additional aid to help identify problems during development the centralised list of exceptions you see below can also be referred to.

<br>

**[PowaTagException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_exception.html)**<br />
The base class for all exceptions indicating unexpected errors from the SDK.
Other runtime exceptions such as <code>ArgumentException</code>, <code>ArgumentNullException</code> or <code>ArgumentOutOfRangeException</code> may be thrown by the SDK to indicate serious programming errors.

<b>Classes using this exception:</b>


Class                  | Method                        | Description
-----------------------|-------------------------------|---------------------------
ActManager   		   | SubmitTransactionAsync        | If the request fails.
-----------------------|-------------------------------|---------------------------
BasketsManager         | UpdateBasketAsync             | If basket to update cannot be found.
-----------------------|-------------------------------|---------------------------
BasketsManager         | CreateInvoiceAsync            | If the basket used to create the invoice cannot be found.
-----------------------|-------------------------------|---------------------------
LoginManager		   | SignInAsGuest				   | Failure to create a profile
-----------------------|-------------------------------|---------------------------
LoginManager           | LogoutAsync				   | Failure to delete a temporary profile
-----------------------|-------------------------------|---------------------------
PaymentManager		   | PayAsync					   | If the request fails
-----------------------|-------------------------------|---------------------------
ProfileManager		   | DeletePaymentInstrumentAsync  | When the payment instrument cannot be found.
-----------------------|-------------------------------|---------------------------
AppLinkTagDetector	   | DetectAppLink				   | If there is an error parsing the AppLink data. e.g a malformed or corrupt link
-----------------------|-------------------------------|---------------------------
WorkflowManager		   | GetWorkflowAsync			   | If the request fails

<br />

**[PowaTagAuthorizationException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_authorization_exception.html)**<br />
Indicates an attempt to make an API request without proper authorization, such as trying to access a protected API before logging in.

<b>Parent:</b> PowaTagException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
LoginManager			| SignInAsGuest					| If the user is already logged in.
------------------------|-------------------------------|---------------------------
LoginManager			| GetCurrentAccessToken			| If the user is not logged in.
------------------------|-------------------------------|---------------------------
LoginManager			| LogoutAsync					| If the current profile cannot be retrieved while trying to log out.
------------------------|-------------------------------|---------------------------
BasketsManager			| UpdateBasketAsync 			| Can't obtain the access token or current basket due to user not being authorized.
------------------------|-------------------------------|---------------------------
BasketsManager			| CreateInvoiceAsync			| Can't obtain the access token or current basket due to user not being authorized.
------------------------|-------------------------------|---------------------------
Basketsmanager			| GetCurrentBaskets				| If the returned Baskets object is null.
------------------------|-------------------------------|---------------------------
PaymentManager			| PayAsync 						| Attempting to obtain the user's access token while not authorised.
------------------------|-------------------------------|---------------------------
ProfileManager			| GetCurrentProfile				|
 | AddPaymentInstrumentAsync	|
 | AddAddressAsync				|
 | UpdateProfileAsync			|
 | DeleteAddressAsync			| Attempting to obtain the current profile without user being logged in.
 | UpdateAddressAsync			|
 | UpdatePaymentInstrumentAsync	|
 | DeletePaymentInstrumentAsync	|
 | SaveProfileAsync				|
------------------------|-------------------------------|---------------------------
WorkflowManager			| GetWorkflowAsync			 	| Attempting to obtain the current profile without user being logged in.

<br />

**[PowaTagCancellationException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_cancellation_exception.html)**<br />
Indicates an asynchronous operation was cancelled.


<b>Parent:</b> PowaTagException<br />

<b>Classes using this exception:</b> None

<br />

**[PowaTagUnsupportedActDataTypeException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_unsupported_act_data_type_exception.html)**<br />
Indicates an Act campaign requires a data type that is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this Act campaign.

<b>Parent:</b> PowaTagException<br />

<b>Classes using this exception:</b> None

<br />

**[PowaTagUnsupportedFeatureException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_unsupported_feature_exception.html)**<br />
Indicates an attempt to use a feature that is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this workflow type.

<b>Parent:</b> PowaTagException<br />

<b>Classes using this exception:</b> None

<br />

**[PowaTagUnsupportedWorkflowTypeException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_unsupported_workflow_type_exception.html)**<br />
Indicates a workflow type is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this workflow type.

<b>Parent: </b>PowaTagUnsupportedFeatureException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
WorkflowManager			| GetWorkflowAsync				| If the workflow type is unsupported.

<br />


**[PowaTagUnsupportedCustomDataTypeException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_unsupported_custom_data_type_exception.html)**<br />
Indicates a merchant requires a custom data type that is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this merchant.

<b>Parent: </b>PowaTagUnsupportedFeatureException<br />

<b>Classes using this exception:</b>


<br />

**[PowaTagValidationException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_validation_exception.html)**<br />
Indicates a generic validation issue with data provided to an SDK component.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b> None

<br />


**[PowaTagMissingRequiredActDataValuesException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_missing_required_act_data_value_exception.html)**<br />
Indicates an attempt to submit values for an act campaign "act" but one or more non-optional values, as specified by <code>Act.ActDataKeys</code> and <code>ActDataKey.IsOptional</code>, were not present.

<b>Parent: </b>PowaTagValidationException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
ActManager				| SubmitTransactionAsync		| When missing one or more required act data values

<br />

**[PowaTagSerializationException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_serialization_exception.html)**<br />
Indicates a generic issue serializing or deserializing data.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
BasketsManager			| CreateInvoiceAsync			| If the invoice has an incorrect invoice type. The only type acceptable is PAYMENT.
------------------------|-------------------------------|---------------------------
CampaignManager			| CreateInvoiceAsync			| If the invoice has an incorrect invoice type. The only type acceptable is DONATION.

<br />


**[PowaTagUndefinedPropertySerializationException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_undefined_property_serialization_exception.html)**<br />
Indicates a response could not be deserialized because a required property is undefined.

<b>Parent: </b>PowaTagSerializationException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
BasketsManager			| CreateInvoiceAsync			| If the invoice is missing the required property: invoiceType
------------------------|-------------------------------|---------------------------
CampaignManager			| CreateInvoiceAsync			| If the invoice is missing the required property: invoiceType
------------------------|-------------------------------|---------------------------
WorkflowManager			| toWorkflow					| If a workflow is missing a reuired property type


<br />

**[PowaTagInvalidApiKeyException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_invalid_api_key_exception.html)**<br />
Indicates an attempt to initialize the SDK without a valid api key.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
PowaTagKit				| InitializeSdk					| If the api key used to initialize the SDK is either null or an empty string.

<br />

**[PowaTagInvalidDonationAmountException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_invalid_donation_amount_exception.html)**<br />
Indicates an invalid donation amount, for instance when specifying an amount that is not one of <code>SuggestedAmounts</code> when <code>IsCustomAmountAllowed</code> is not true.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
CampaignManager			| CreateInvoiceAsync			| Indicates an invalid donation amount

<br />

**[PowaTagInvalidTagFormatException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_invalid_tag_format_exception.html)**<br />
Indicates an attempt to create a <code>Tag</code> from an invalid label. You should use <code>Tag.IsValidQrFormatUrl</code> to check if a string is a valid label before attempting to create a tag from it.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
Tag						| ParseQrUrl					| If the tag label is invalid
 | | If the host name is not supported for QR tags
 | | Invalid QR URL
------------------------|-------------------------------|---------------------------
Tag						| ParseAudio 					| If the audio reference is invalid

<br />

**[PowaTagInvalidWorkflowTypeException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_invalid_workflow_type_exception.html)**<br />
Indicates an attempt to convert a workflow object to an incorrect specific workflow type, e.g. attempting to convert a workflow object of type <code>WorkflowType.BASKET</code> to a <code> ProductWorkflow</code>.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
WorkflowType			| AsProductWorkflow |
 | AsTemporaryBasketWorkflow |
 | AsCampaignWorkflow |
 | AsActWorkflow |


<br />

**[PowaTagKitNotInitializedException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/)**<br /> LINK NEEDED
Indicates an attempt to use an SDK component before properly initializing the SDK. Call PowaTagKit <code>InitializeSdk</code> when your application loads, before using any of the other SDK components.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
PowaTagKit				| IsSdkInitialized  			|
 | DeviceId |
 | GetApiKey |
 | GetSecret |

<br />

**[PowaTagHttpException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_http_exception.html)**<br />
Indicates an HTTP error response was received from the server. You can retrieve the response status code using <code>HttpStatusCode</code>.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b> None


<br />


# Handling PowaTag Service Exceptions

<br />
**[PowaTagServiceException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_service_exception.html)**<br />
Indicates an error from a PowaTag API service in response to a request.

<b>Parent: </b>PowaTagHttpException<br />

<b>Classes using this exception:</b> None

To obtain additional information for the exceptions you use the <code>PowaTagServiceException.Errors</code> to retrieve a list of <code>ServiceException</code> that can be interrogated:

	try
	{
		// do something that throws exception
	}
	catch (PowaTagServiceException ex)
	{
		List<ServiceError> errorList = ex.Errors;
		foreach (ServiceError serviceError in errorList)
		{
			// Optional code uniquely identifying the error condition.
			int errrorCode = serviceError.Code;

			// Optional action to be taken as a result of this error.
			String action = serviceError.Action;

			// Optional error message for the application developer. Should not be displayed to the user.
			String devMsg = serviceError.DeveloperMessage;

			// Optional localized error message that may be displayed to the user.
			String userMsg = serviceError.UserMessage;

			// Optional URL containing more information about the error.
			String moreInfoUrl = serviceError.MoreInfoUrl;

			// Optional error debugging information.
			String debugInfo = serviceError.DebugInfo;

			// Optional additional error information.
			Dictionary<String, String> additionalFields = serviceError.AdditionalFields;
		}
	}

<br />

**[PowaTagServiceValidationException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_service_validation_exception.html)**<br />
Indicates a validation issue with a request sent to a service.

<b>Parent: </b>PowaTagServiceException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
ProfileManager			| AddPaymentInstrumentAsync		| If payment instrument details were invalid
------------------------|-------------------------------|---------------------------
ProfileManager			| AddAddressAsync				| If address details were invalid.
------------------------|-------------------------------|---------------------------
ProfileManager			| UpdateAddressAsync			| If address details provided were invalid.

<br />


**[PowaTagOutOfStockException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_out_of_stock_exception.html)**<br />
Indicates a product is out of stock.

<b>Parent: </b>PowaTagServiceException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
PaymentManager			| PayAsync						| If the item is out of stock

<br />

**[PowaTagNotFoundException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_not_found_exception.html)**<br />
Indicates an HTTP error response was received from the server. You can retrieve the response status code using <code>HttpStatusCode</code>.

<b>Parent: </b>PowaTagServiceException<br />

<b>Classes using this exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
BasketsManager			| UpdateBasketAsync				| Basket not found during update
------------------------|-------------------------------|---------------------------
 | CreateInvoiceAsync	| Basket not found during invoice creation
------------------------|-------------------------------|---------------------------
ProfileManager			| AddPaymentInstrumentAsync		| If profile or billing address not found
------------------------|-------------------------------|---------------------------
 | UpdatePaymentInstrumentAsync |
 | AddAddressAsync |
 | GetCurrentProfile |
 | UpdateProfileAsync |  if the profile can not be found.
 | UpdateAddressAsync |
 | DeleteAddressAsync |
 | DeletePaymentInstrumentAsync |
WorkflowManager		| GetWorkflowAsync				| If the workflow for the tag cannot be found.


<br />

# Error Codes
The following table lists out the errors that you might encounter when handling PowaTagServiceException exceptions.

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

# General Exceptions
The following exceptions can be encountered at any time.

**[PowaTagNetworkException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_network_exception.html)**<br />
Indicates a generic network problem.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b> This exception can be encountered at any time.

<br />


**[PowaTagNetworkTimeoutException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_network_timeout_exception.html)**<br />
Indicates the network operation took too long to complete and was aborted.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b> This exception can be encountered at any time.

<br />

**[PowaTagNoInternetConnectionException]({{site.baseurl}}/tag-mobile-sdks/0.9.7/refdocs/windows_phone/class_powa_tag_1_1_windows_phone_1_1_sdk_1_1_powa_tag_no_internet_connection_exception.html)**<br />
Indicates no internet connection is available.

<b>Parent: </b>PowaTagException<br />

<b>Classes using this exception:</b> This exception can be encountered at any time.

<br />
