---
layout: page
title: Getting Started with Android SDK
permalink: /tag-mobile-sdks/android/start/
---

The PowaTag SDK for Android is the easiest way to integrate your Android app with PowaTag.

It enables:

* Triggers - Your app can react to PowaTag tags placed around the environment.
* Workflows - Respond to tags by providing appropriate and contextual user journeys.
* Baskets - People can purchase products from PowaTag merchants using your app.

<br />

# Requirements

PowaTag SDK for Android requires a minimum Android API version of 9, ensure either your AndroidManifest.xml has `android:minSdkVersion="9"` or your /app/build.gradle file has `minSdkVersion 9` or higher.

<br />

# Install the SDK using Android Studio

To use PowaTag SDK in a project, add it as a build dependency and import it.

1. Add the following to Module-level /app/build.gradle before dependencies:

    <pre>repositories {
        maven { url "http://nexus.ht.powa.com/nexus/content/repositories/ptk-releases/" }
    }</pre>

2. Modify the build.gradle file:
	a. Add the compile dependency with the latest version of the PowaTag SDK
    
	<pre>
    dependencies {
        compile 'com.powatag.android:powatag-kit:0.8.5'
    }</pre>
	
	b. Add exclusions to the packagingOptions
	
	<pre>packagingOptions {
        exclude 'META-INF/LICENSE'
        exclude 'META-INF/LICENSE.txt'
        exclude 'META-INF/NOTICE'
        exclude 'META-INF/NOTICE.txt'
    }</pre>	
	

3. Press the Sync Now notification at the top of the code window, or manually refresh Gradle if you are not prompted.

4. Build your project. Now you can import `com.powatag.android.sdk.PowaTagKit` into your app.

<br />

# Initialize the SDK

You need to initialize PowaTag SDK before you can use it. Add a call to `PowaTagSdk.initializeSdk` from onCreate in Application or Activity:

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //Initialize the SDK using the default PowaTag endpoint
        PowaTagKit.initializeSdk(getApplicationContext(), apiKey, secret);
    }

During development you will need ot use a non-production endpoint and for this a second constructor is available for initializing the SDK:    

    @Override
    public void onCreate(Bundle savedInstanceState) {
        PowaTagEndpoint endpoint;
        super.onCreate(savedInstanceState);
        endpoint = PowaTagEndpoint.defaultEndpointPorts(hostNameString);
        PowaTagKit.initializeSdk(getApplicationContext(), endpoint, apiKey, secret);
    }	
<br />	

        
If you plan to test your application using a mock server 
There is a third approach to initialising the SDK. This method requires that you provide every endpoint and port manually.on is to use the builder directly to set all the services endpoints
* This is intended for testing purposes where you may need the ability to change ports when using mock servers
Note; they need to set every single endpoint if they use this method because 
==================================

# Importing The Sample App

The **HelloPowaTag-Sample** application has been included in the SDK.

You can experiment with the sample by importing the it into a Android Studio project:

1. Go to Android Studio \| New \| Import Project

2. Navigate to the folder where you unpacked the SDK, open the samples folder, and choose the sample project you want to import. In this example, we choose the barcode-sample project. Click OK to open it.

    <img src="{{ '/images/powatag_mobile_sdks_android_start_import.png' | prepend: site.baseurl }}" height="400" />

3. Build the sample project.

The sample has a project dependency rather than a central repository dependency via Maven Central or jcenter. This is so that when a local copy of the SDK gets updates, the sample reflects the changes.

<br />

# Next Steps

After you install PowaTag SDK for Android, you can see:

* [Login]({{site.baseurl}}/tag-mobile-sdks/android/login/)
* [Profile]({{site.baseurl}}/tag-mobile-sdks/android/profile/)
* [Triggers]({{site.baseurl}}/tag-mobile-sdks/android/triggers/)
* [Workflows]({{site.baseurl}}/tag-mobile-sdks/android/workflows/)
* [Baskets]({{site.baseurl}}/tag-mobile-sdks/android/baskets/)
* [Campaigns]({{site.baseurl}}/tag-mobile-sdks/android/campaigns/)
* [Acts]({{site.baseurl}}/tag-mobile-sdks/android/acts/)
* [Payments]({{site.baseurl}}/tag-mobile-sdks/android/payments/)

<br />

# Install the SDK Manually

1. Extract the SDK Zip folder.

2. Go to File > New Module > "Import .JAR or .AAR Package" and add the powatag-kit.aar file located in the library folder.

3. Set powatag-kit-0.8.5 as a new dependency of your application module by going to File > Project Structure. On tab Dependencies tab click plus button and choose powatag-kit-0.8.5 module.

4. Now you can import `com.powatag.android.sdk.PowaTagKit` into your app.

<br />

# Using the PowaTag SDK with Maven

You can declare the Maven dependency with the latest available version of the Android SDK:

    <dependency>
        <groupId>com.powatag.android</groupId>
        <artifactId>powatag-kit</artifactId>
         <version>0.8.5</version>
    </dependency>
