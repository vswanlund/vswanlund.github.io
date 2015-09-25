---
layout: page
title: iOS SDK Error Handling
permalink: /tag-mobile-sdks/ios/errors/
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
