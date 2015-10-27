---
layout: page
title: Android SDK Error Handling
permalink: /tag-mobile-sdks/android/errors/
---

To build a robust and reliable app you want to make sure that it properly responds to errors.

This guide covers features that the PowaTag SDK provides to help you do this.

<br />

# Error Handling and Recovery
	list the different parent types of exceptions and describe how to handle them.

# SDK Exceptions

# Error Codes


Key                    | Codes                         | Description
-----------------------|-------------------------------|---------------------------
NSUnderlyingErrorKey   | Any                           | Underlying NSError, if any
-----------------------|-------------------------------|---------------------------
PTKErrorMessageKey     | Any                           | Optional error message
-----------------------|-------------------------------|---------------------------
PTKErrorDescriptionKey | Any                           | Description of the error
-----------------------|-------------------------------|---------------------------
PTKHTTPStatusCodeKey   | PTKPowaTagHttpErrorCode,      | HTTP status code
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