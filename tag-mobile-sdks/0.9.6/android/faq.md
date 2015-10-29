---
layout: page
title: Android SDK FAQ & Troubleshooting
permalink: /tag-mobile-sdks/0.9.6/android/faq/
---

In this document:

**FAQ**

* [Changing The PowaTag API Endpoint](#faq-endpoint)

**Troubleshooting**

<br />

# FAQ

**Changing The PowaTag API Endpoint**<a name="faq-endpoint"></a>

During testing or development you may need to change the PowaTag API endpoint the SDK communicates with, e.g. to "beta.powatag.com".

To change the endpoint pass the desired endpoint when initializing the SDK:

    PowaTagKit.initializeSdk(getApplicationContext(), PowaTagEndpoint.defaultEndpointPorts("https://beta.powatag.com"));

<br />

# Troubleshooting
