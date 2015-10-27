---
layout: page
title: Android SDK Error Handling
permalink: /tag-mobile-sdks/android/errors/
---

To build a robust and reliable app you want to make sure that it properly responds to errors.

This guide covers features that the PowaTag SDK provides to help you do this.

<br />

# Error Handling and Recovery

LIST THE DIFF CATEGORY OF EXCEPTIONS AND SHOW SNIPPETS FOR INTERROGATING.<BR />
E.G. SERVICEEXCEPTION.GETCODE()....

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
ProfileManager			| getCurrentProfile				| Attempting to obtain the current profile without user being logged in.
						| addPaymentInstrument			|
						| addAddress					|
						| updateProfile					|
						| deleteAddress					|
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

		
**[PowaTagMissingRequiredActDataValuesException]({{site.baseurl}}/tag-mobile-sdks/0.9.6-javadoc/Android/classcom_1_1powatag_1_1android_1_1sdk_1_1_powa_tag_unsupported_custom_data_type_exception.html)**<br />
Indicates an attempt to submit values for an act campaign "act" but one or more non-optional values, as specified by {@link Act#getActDataKeys} and {@link ActDataKey#isOptional}, were not present.
Classes throwing this Exception:
 ActManager: 
submitTransaction - when missing one or more required act data values

1.6	PowaTagSerializationException
 Indicates a generic issue serializing or deserializing data.
		  
	Classes throwing this Exception:
	BasketsManager: 
createInvoice - if the created invoice has an incorrect invoice type. The only type acceptable is PAYMENT. 
	CampaignManager: 
createInvoice - if the created invoice has an incorrect invoice type. The only type acceptable is DONATION. 
		
1.6.1	PowaTagUndefinedPropertySerializationException
Indicates a response could not be deserialized because a required property is undefined.
				  
	       Classes throwing this Exception:
	       BasketsManager: 
createInvoice - if the invoice is missing the required property: invoiceType
       CampaignManager: 
createInvoice - if the invoice is missing the required property: invoiceType
       WorkflowManager: 
toWorkflow - if a workflow is missing a reuired property type
		getProfile - if the profile payment instrument is missing the properties: paymentType or issuer
									 
									 
									 
1.7	PowaTagInvalidApiKeyException
Indicates an attempt to initialize the SDK without a valid api key.
		  
	Classes throwing this Exception:
PowaTagKit: 
initializeSdk - if the api key used to initialize the SDK is either null or an empty string.

1.8	PowaTagInvalidDonationAmountException
Indicates an invalid donation amount, for instance when specifying an amount that is not one of {@link Campaign#getSuggestedAmounts()} when {@link Campaign#isCustomAmountAllowed()} is not true.
		  
	Classes throwing this Exception:
CampaignManager: 
createInvoice

1.9	PowaTagInvalidTagFormatException
Indicates an attempt to create a {@link Tag} from an invalid label. You should use {@link Tag#isValidQrFormatUrl} to check if a string is a valid label before attempting to create a tag from it.
	  
	 Classes throwing this Exception:
Tag: 
parseQrUrl - 	If the tag label is invalid
If the host name is not supported for QR tags
					Invalid QR URL
			 parseAudio - 	If the audio reference is invalid

1.10	PowaTagInvalidWorkflowTypeException
Indicates an attempt to convert a workflow object to an incorrect specific workflow type, e.g. attempting to convert a workflow object of type {@link WorkflowType#BASKET} to a {@link ProductWorkflow}.
		  
		Classes throwing this Exception:
WorkflowType: 
Thrown in methods asProductWorkflow, asBasketWorkflow, asCampaignWorkflow and asActWorkflow

1.11	PowaTagKitNotInitializedException
Indicates an attempt to use an SDK component before properly initializing the SDK. Call {@link PowaTagKit#initializeSdk} when your application loads, before using any of the other SDK components.
		Classes throwing this Exception:
PowaTagKit: 
Thrown in methods checkSdkInitialized, getDeviceId, getApiKey and getSecret
1.12	PowaTagHttpException
Indicates an HTTP error response was received from the server. You can retrieve the response status code using {@code #getStatus()}.
		Classes throwing this Exception: NONE		    
		
1.12.1	PowaTagServiceException
		Indicates an error from a PowaTag API service in response to a request.
Information for each error reported by the service can be found in the list of errors provided by getErrors() method.
Classes throwing this Exception: NONE 
To obtain additional information for all sub classes you can use the PowaTagServiceException.getErrors() method to return a list of <code>ServiceException</code> that can be interrogated:
List<ServiceError> errorList = ((PowaTagServiceException) exception).getErrors();		
for (ServiceError serviceError: errorList) {
// A code uniquely identifying the error condition.
			 Integer errrorCode = serviceError.getCode();
					 
			 // The action to be taken as a result of this error.
			 String action = serviceError.getAction();
				 
			 // Optional error message for the application developer. Should not be displayed to the 
user.
String devMsg =  serviceError.getDeveloperMessage();
					 
			 // Optional localized error message that may be displayed to the user.
			String userMsg = serviceError.getUserMessage();
					 
			 // An optional URL containing more information about the error.
			URI moreInfoUrl = serviceError. getMoreInfoUrl ();
					 
			 // Error debugging information.
			 String debugInfo = serviceError. getDebugInfo ();
				 
			 // A Map<String,String> of additional error fields.
			 Map<String,String> additionalFields = serviceError. getAdditionalFields ();
		  }
					 
					 
1.12.1.1	PowaTagServiceValidationException
Indicates a validation issue with a request sent to a service.						  
		Use the getErrors(powatagexception) method to obtain a list of PowaTagServiceExceptions
						  
		Classes throwing this Exception:
		ProfileManager: 
addPaymentInstrument - if payment instrument details were invalid
			addAddress - if address details were invalid.
			updateAddress - if address details provided were invalid.
											
											
1.12.1.2	PowaTagOutOfStockException
Indicates a product is out of stock.
						  
		Classes throwing this Exception:
PaymentManager: 
makePayment - item out of stock
			
1.12.1.3	PowaTagNotFoundException
Indicates an HTTP error response was received from the server. You can retrieve the response status code using {@code #getStatus()}.
						  
		Classes throwing this Exception:
BasketsManager: 
updateBasket - 	basket not found during update
			createInvoice - basket not found during invoice creation
		ProfileManager: 
addPaymentInstrument - if profile or billing address not found
			updatePaymentInstrument - if profile could not be found
			addAddress ? - if profile could not be found  
			getProfile - if profile could not be found
			updateProfile - if profile could not be found
			updateAddress - if profile could not be found
			deleteAddress - if profile could not be found
			deletePaymentInstrument = if profile could not be found
		WorkflowManager:
 getWorkflow - if the workflow for the tag cannot be found.				
											




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


# PowaTagAuthorizationException
Indicates an attempt to make an API request without proper authorization such as trying to access a protected API before logging in.

# PowaTagCancellationException
Indicates an asynchronous operation was cancelled.

# PowaTagException
The base class for all exceptions indicating unexpected errors from the SDK.
Other runtime exceptions such as {@code IllegalArgumentException} may be thrown by the SDK to indicate serious programming error.

# PowaTagHttpException
Indicates an HTTP error response was received from the server. You can retrieve the response status code using {@code #getStatus()}.

# PowaTagInvalidApiKeyException
Indicates an attempt to initialize the SDK without a valid api key.

# PowaTagInvalidDonationAmountException
Indicates an invalid donation amount, for instance when specifying an amount that is not one of {@link Campaign#getSuggestedAmounts()} when {@link Campaign#isCustomAmountAllowed()} is not true.

# PowaTagInvalidTagFormatException
Indicates an attempt to create a {@link Tag} from an invalid label. You should use {@link Tag#isValidQrFormatUrl} to check if a string is a valid label before attempting to create a tag from it.

# PowaTagInvalidWorkflowTypeException
Indicates an attempt to convert a workflow object to an incorrect specific workflow type, e.g. attempting to convert a workflow object of type {@link WorkflowType#BASKET} to a {@link ProductWorkflow}.

# PowaTagKitNotInitializedException
Indicates an attempt to use an SDK component before properly initializing the SDK. Call {@link PowaTagKit#initializeSdk} when your application loads, before using any of the other SDK components.

# PowaTagMissingRequiredActDataValuesException
Indicates an attempt to submit values for an act campaign "act" but one or more non-optional values, as specified by {@link Act#getActDataKeys} and {@link ActDataKey#isOptional}, were not present.

# PowaTagNetworkException
Indicates a generic network problem.

# PowaTagNetworkTimeoutException
Indicates the network operation took too long to complete and was aborted.

# PowaTagNoInternetConnectionException
Indicates no internet connection is available.

# PowaTagNotFoundException
Indicates an HTTP error response was received from the server. You can retrieve the response status code using {@code #getStatus()}.

# PowaTagOutOfStockException
Indicates a product is out of stock.

# PowaTagSerializationException
Indicates a generic issue serializing or deserializing data.

# PowaTagServiceException
Indicates an error from a PowaTag API service in response to a request.
Information for each error reported by the service can be found in the list of errors provided by {@link #getErrors()}.

# PowaTagServiceValidationException
Indicates a validation issue with a request sent to a service.

# PowaTagUndefinedPropertySerializationException
Indicates a response could not be deserialized because a required property is undefined.

# PowaTagUnsupportedActDataTypeException
Indicates an Act campaign requires a data type that is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this Act campaign.

# PowaTagUnsupportedCustomDataTypeException
Indicates a merchant requires a custom data type that is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this merchant.

# PowaTagUnsupportedFeatureException
Indicates an attempt to use a feature that is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this workflow type.

# PowaTagUnsupportedWorkflowTypeException
Indicates a workflow type is not supported in the current version of the SDK.
You should check for upgrades to the SDK to enable support for this workflow type.

# PowaTagValidationException
Indicates a generic validation issue with data provided to an SDK component.

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





