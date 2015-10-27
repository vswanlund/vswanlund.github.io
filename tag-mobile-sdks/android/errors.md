---
layout: page
title: Android SDK Error Handling
permalink: /tag-mobile-sdks/android/errors/
---

To build a robust and reliable app you want to make sure that it properly responds to errors.

This guide covers features that the PowaTag SDK provides to help you do this.

<br />

# SDK Exceptions

The SDK [Javadoc]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/) provides the details of every method including parameters and exceptions.

As and aid to help identify problems during development this centralised list of exceptions can also be referred to. 

**[PowaTagException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_exception.html)**<br />
The base class for all exceptions indicating unexpected errors from the SDK.
Other runtime exceptions such as <code>IllegalArgumentException</code> may be thrown by the SDK to indicate serious programming errors.

<b>Classes throwing this Exception:</b>


Class                  | Method                        | Description
-----------------------|-------------------------------|---------------------------
ActManager   		   | submitTransaction             | If the request fails.
-----------------------|-------------------------------|---------------------------
BasketsManager         | updateBasket                  | If basket to update cannot be found.
-----------------------|-------------------------------|---------------------------
BasketManager          | createInvoice                 | If the basket used to create the invoice cannot be found.
-----------------------|-------------------------------|---------------------------
BlockingPowaTagExecutor| await						   | If the thread is interrupted while waiting for result.
-----------------------|-------------------------------|---------------------------
LoginManager		   | signInAsGues				   | Failure to create a profile ????????
-----------------------|-------------------------------|---------------------------
LoginManager           | logout						   | Failure to delete a temporary profile??????
-----------------------|-------------------------------|---------------------------
PaymentManager		   | pay						   | If the request fails
-----------------------|-------------------------------|---------------------------
ProfileManager		   | addPaymentInstrument		   | ???
-----------------------|-------------------------------|---------------------------
ProfileManager 		   | updateAddress				   | ????
-----------------------|-------------------------------|---------------------------
ProfileManager		   | deletePaymentInstrument	   | When the payment instrument cannot be found.
-----------------------|-------------------------------|---------------------------
ProfileManager		   | saveProfile				   | ??????
-----------------------|-------------------------------|---------------------------
AppLinkTagDetector	   | detectAppLink				   | If there is an error parsing the AppLink data. e.g a malformed or corrupt link
-----------------------|-------------------------------|---------------------------
WorkflowManager		   | getWorkflow				   | If the request fails

<br />  
    
**[PowaTagAuthorizationException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_authorization_exception.html)**<br />
Indicates an attempt to make an API request without proper authorization, such as trying to access a protected API before logging in.

<b>Parent:</b> PowaTagException<br />

<b>Classes throwing this Exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
LoginManager			| signInAsGuest					| If the user is already logged in.
------------------------|-------------------------------|---------------------------
LoginManager			| getCurrentAccessToken			| If the user is not logged in.
------------------------|-------------------------------|---------------------------
LoginManager			| logout						| If the current profile cannot be retrieved while trying to log out.
------------------------|-------------------------------|---------------------------
BasketsManager			| updateBasket 					| Can't obtain the access token or current basket due to user not being authorized.
------------------------|-------------------------------|---------------------------
BasketsManager			| createInvoice					| Can't obtain the access token or current basket due to user not being authorized.
------------------------|-------------------------------|---------------------------
Basketsmanager			| getCurrentBaskets				| If the returned Baskets object is null.
------------------------|-------------------------------|---------------------------
PaymentManager			| pay 							| Attempting to obtain the user's access token while not authorised.
------------------------|-------------------------------|---------------------------
ProfileManager			| getCurrentProfile				| 
 | addPaymentInstrument			|
 | addAddress					|
 | updateProfile					|
 | deleteAddress					| Attempting to obtain the current profile without user being logged in.
 | updateAddress					| 
 | updatePaymentInstrument		| 
 | deletePaymentInstrument		| 
 | saveProfile					| 
------------------------|-------------------------------|---------------------------
WorkflowManager			| getWorkflow				 	| Attempting to obtain the current profile without user being logged in.

<br />		

**[PowaTagCancellationException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_cancellation_exception.html)**<br />
Indicates an asynchronous operation was cancelled.


<b>Parent:</b> PowaTagException<br />

<b>Classes throwing this Exception: None</b>

<br />
	
**[PowaTagUnsupportedActDataTypeException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_unsupported_act_data_type_exception.html)**<br />
Indicates an Act campaign requires a data type that is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this Act campaign.

<b>Parent:</b> PowaTagException<br />

<b>Classes throwing this Exception: None</b>

<br />		    

**[PowaTagUnsupportedFeatureException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_unsupported_feature_exception.html)**<br />
Indicates an attempt to use a feature that is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this workflow type.

<b>Parent:</b> PowaTagException<br />

<b>Classes throwing this Exception: None</b>

<br />	

**[PowaTagUnsupportedWorkflowTypeException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_unsupported_workflow_type_exception.html)**<br />
Indicates a workflow type is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this workflow type.

<b>Parent: </b>PowaTagUnsupportedFeatureException<br />

<b>Classes throwing this Exception:</b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
WorkflowManager			| getWorkflow					| If the workflow type is unsupported.

<br />
	
	
**[PowaTagUnsupportedCustomDataTypeException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_unsupported_custom_data_type_exception.html)**<br />
Indicates a merchant requires a custom data type that is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this merchant.

<b>Parent: </b>PowaTagUnsupportedFeatureException<br />

<b>Classes throwing this Exception: </b>  ??


<br />

**[PowaTagValidationException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_validation_exception.html)**<br />
Indicates a generic validation issue with data provided to an SDK component.

<b>Parent: </b>PowaTagException<br />

<b>Classes throwing this Exception: </b>None

<br />


**[PowaTagMissingRequiredActDataValuesException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_missing_required_act_data_values_exception.html)**<br />
Indicates an attempt to submit values for an act campaign "act" but one or more non-optional values, as specified by <code>getActDataKeys</code> and <code>isOptional</code>, were not present.

<b>Parent: </b>PowaTagValidationException<br />

<b>Classes throwing this Exception: </b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------		    
ActManager				| submitTransaction				| When missing one or more required act data values

<br />

**[PowaTagSerializationException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_serialization_exception.html)**<br />
Indicates a generic issue serializing or deserializing data.

<b>Parent: </b>PowaTagException<br />

<b>Classes throwing this Exception: </b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------		    
BasketsManager			| createInvoice					| If the invoice has an incorrect invoice type. The only type acceptable is PAYMENT. 
------------------------|-------------------------------|---------------------------		    
CampaignManager			| createInvoice					| If the invoice has an incorrect invoice type. The only type acceptable is DONATION. 

<br />		  
 

**[PowaTagUndefinedPropertySerializationException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_undefined_property_serialization_exception.html)**<br /> 
Indicates a response could not be deserialized because a required property is undefined.

<b>Parent: </b>PowaTagSerializationException<br />

<b>Classes throwing this Exception: </b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------	
BasketsManager			| createInvoice					| If the invoice is missing the required property: invoiceType
------------------------|-------------------------------|---------------------------	
CampaignManager			| createInvoice					| If the invoice is missing the required property: invoiceType
------------------------|-------------------------------|---------------------------	
WorkflowManager			| toWorkflow					| If a workflow is missing a reuired property type
------------------------|-------------------------------|---------------------------	
WorkflowManager			| getProfile					| If the profile payment instrument is missing the properties: paymentType or issuer

<br />									 

**[PowaTagInvalidApiKeyException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_invalid_api_key_exception.html)**<br /> 
Indicates an attempt to initialize the SDK without a valid api key.

<b>Parent: </b>PowaTagException<br />

<b>Classes throwing this Exception: </b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------			  
PowaTagKit				| initializeSdk					| If the api key used to initialize the SDK is either null or an empty string.

<br />

**[PowaTagInvalidDonationAmountException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_invalid_donation_amount_exception.html)**<br /> 
Indicates an invalid donation amount, for instance when specifying an amount that is not one of <code>getSuggestedAmounts</code> when <code>isCustomAmountAllowed()</code> is not true.

<b>Parent: </b>PowaTagException<br />

<b>Classes throwing this Exception: </b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------			  
CampaignManager			| createInvoice					| Indicates an invalid donation amount

<br />

**[PowaTagInvalidTagFormatException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_invalid_tag_format_exception.html)**<br /> 
Indicates an attempt to create a <code>Tag</code> from an invalid label. You should use <code>Tag.isValidQrFormatUrl</code> to check if a string is a valid label before attempting to create a tag from it.

<b>Parent: </b>PowaTagException<br />

<b>Classes throwing this Exception: </b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
Tag						| parseQrUrl					| If the tag label is invalid
 | | If the host name is not supported for QR tags
 | | Invalid QR URL
------------------------|-------------------------------|--------------------------- 
Tag						| parseAudio 					| If the audio reference is invalid

<br />

**[PowaTagInvalidWorkflowTypeException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_invalid_workflow_type_exception.html)**<br /> 
Indicates an attempt to convert a workflow object to an incorrect specific workflow type, e.g. attempting to convert a workflow object of type {@link WorkflowType#BASKET} to a {@link ProductWorkflow}.

<b>Parent: </b>PowaTagException<br />

<b>Classes throwing this Exception: </b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
WorkflowType			| asProductWorkflow |
 | asBasketWorkflow |
 | asCampaignWorkflow | 
 | asActWorkflow |


<br />
 
**[PowaTagKitNotInitializedException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_kit_not_initialized_exception.html)**<br /> 
Indicates an attempt to use an SDK component before properly initializing the SDK. Call PowaTagKit <code>initializeSdk</code> when your application loads, before using any of the other SDK components.

<b>Parent: </b>PowaTagException<br />

<b>Classes throwing this Exception: </b>

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
PowaTagKit				| checkSdkInitialized 			|
 | getDeviceId |
 | getApiKey |
 | getSecret |

<br />

**[PowaTagHttpException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_http_exception.html)**<br /> 
Indicates an HTTP error response was received from the server. You can retrieve the response status code using {@code #getStatus()}.

<b>Parent: </b>PowaTagException<br />

<b>Classes throwing this Exception: </b> None
		
		
<br />


# Handling PowaTag Service Exceptions

<br />
**[PowaTagServiceException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_service_exception.html)**<br /> 
Indicates an error from a PowaTag API service in response to a request.

<b>Parent: </b>PowaTagHttpException<br />

<b>Classes throwing this Exception: </b> None

To obtain additional information for the exceptions you use the <code>PowaTagServiceException.getErrors()</code> to retrieve a list of <code>ServiceException</code> that can be interrogated:

	<pre>List<ServiceError> errorList = ((PowaTagServiceException) exception).getErrors();
	for (ServiceError serviceError: errorList) {
		// A code uniquely identifying the error condition.
		Integer errrorCode = serviceError.getCode();
		
		// The action to be taken as a result of this error.
		String action = serviceError.getAction();

		// Optional error message for the application developer. Should not be displayed to the user.
		String devMsg =  serviceError.getDeveloperMessage();

		// Optional localized error message that may be displayed to the user.
		String userMsg = serviceError.getUserMessage();

		// An optional URL containing more information about the error.
		URI moreInfoUrl = serviceError. getMoreInfoUrl ();

		// Error debugging information.
		String debugInfo = serviceError. getDebugInfo ();

		// A Map<String,String> of additional error fields.
		Map<String,String> additionalFields = serviceError. getAdditionalFields ();
	}</pre>

<br />


**[PowaTagServiceValidationException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_service_validation_exception.html)**<br /> 
Indicates a validation issue with a request sent to a service.						  

<b>Parent: </b>PowaTagServiceException<br />

<b>Classes throwing this Exception: </b> 

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
ProfileManager			| addPaymentInstrument			| If payment instrument details were invalid
------------------------|-------------------------------|---------------------------
ProfileManager			| addAddress					| If address details were invalid.
------------------------|-------------------------------|---------------------------
ProfileManager			| updateAddress					| If address details provided were invalid.

<br />


**[PowaTagOutOfStockException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_out_of_stock_exception.html)**<br /> 
Indicates a product is out of stock.

<b>Parent: </b>PowaTagServiceException<br />

<b>Classes throwing this Exception: </b> 

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
PaymentManager			| makePayment					| If the item is out of stock

<br />

**[PowaTagNotFoundException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_not_found_exception.html)**<br /> 
Indicates an HTTP error response was received from the server. You can retrieve the response status code using <code>getStatus()</code>.

<b>Parent: </b>PowaTagServiceException<br />

<b>Classes throwing this Exception: </b> 

Class                   | Method                        | Description
------------------------|-------------------------------|---------------------------
BasketsManager			| updateBasket					| Basket not found during update
------------------------|-------------------------------|---------------------------
 | createInvoice	| Basket not found during invoice creation
------------------------|-------------------------------|---------------------------
ProfileManager			| addPaymentInstrument			| If profile or billing address not found
------------------------|-------------------------------|---------------------------
 | updatePaymentInstrument |
 | addAddress | 
 | getProfile | 
 | updateProfile |  - if the profile can not be found.
 | updateAddress | 
 | deleteAddress | 
 | deletePaymentInstrument | 
WorkflowManager		| getWorkflow					| If the workflow for the tag cannot be found.				

 
<br />


# Error Handling and Recovery

LIST THE DIFF CATEGORY OF EXCEPTIONS AND SHOW SNIPPETS FOR INTERROGATING.<BR />
E.G. SERVICEEXCEPTION.GETCODE()....

<br />


General Exceptions
The following exceptions can be encountered at any time.
1.	PowaTagNetworkException
	Indicates a generic network problem.
	  
	Classes throwing this Exception: NONE
		    
1.1	PowaTagNetworkTimeoutException
Indicates the network operation took too long to complete and was aborted.
				  
Classes throwing this Exception: None. 
					
1.2	PowaTagNoInternetConnectionException
Indicates no internet connection is available.
				  
Classes throwing this Exception: None

2.	IllegalStateException
Indicates that a blocking method has been called in the main thread 


<br />

# Error Codes


Key                    | Codes                         | Description
-----------------------|-------------------------------|---------------------------
NSUnderlyingErrorKey   | Any                           | Underlying NSError, if any
-----------------------|-------------------------------|---------------------------
PTKErrorMessageKey     | Any                           | Optional error message
-----------------------|-------------------------------|---------------------------
PTKErrorDescriptionKey | Any                           | Description of the error
-----------------------|-------------------------------|---------------------------





