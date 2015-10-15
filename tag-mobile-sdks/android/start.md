---
layout: page
title: Getting Started with Android SDK
permalink: /tag-mobile-sdks/android/start/
---

The PowaTag SDK for Android is the easiest way to integrate your Android app with PowaTag.

It enables:

* Triggers - Your app can react to PowaTag tags placed around the environment.
* Workflows - Respond to tags by providing appropriate and contextual user journeys.
* Baskets - Users can add products to a basket for purchase from PowaTag merchants to using your app.
* Payments - Users can easily pay for the products they selected using your app.


<br />

# Requirements

PowaTag SDK for Android requires a minimum Android API level of 9, ensure either your AndroidManifest.xml has `android:minSdkVersion="9"` or your /app/build.gradle file has `minSdkVersion 9` or higher.

<br />

# Install the SDK using Android Studio

To use PowaTag SDK in a project, add it as a build dependency and import it.

1. Add the following to Module-level build.gradle before dependencies:

    <pre>repositories {
        maven { url "http://nexus.ht.powa.com/nexus/content/repositories/ptk-releases/" }
    }</pre>

2. Modify the build.gradle file:
	a. Add the compile dependency with the latest version of the PowaTag SDK
    
	<pre>
    dependencies {
        compile 'com.powatag.android:powatag-kit:{{site.current_sdk_version}}'
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

You need to initialize PowaTag SDK before you can use it. Add a call to `PowaTagKit.initializeSdk` from onCreate in Application or Activity:

	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		//Initialize the SDK using the default PowaTag endpoint
		PowaTagKit.initializeSdk(getApplicationContext(), apiKey, secret);
	}
	
During development you need to use a non-production endpoint and for this a second initialization method is available:
	
	~~~~
	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		PowaTagEndpoint endpoint = PowaTagEndpoint.defaultEndpointPorts(hostNameString);
		PowaTagKit.initializeSdk(getApplicationContext(), endpoint, apiKey, secret);
	}
	~~~~
	
<br/>	


# Importing The Sample App

The **HelloPowaTagSample** app is included with the SDK to provide you with examples of the main PowaTag SDK features. 

You can experiment with the SDK features by importing the app into Android Studio project (steps may differ in other IDEs):

1. Go to Android Studio \| New \| Import Project

2. Navigate to the folder where you unpacked the SDK, open the samples folder, and choose the hellopowatag-sample project to import. Click OK to open it.

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

3. Set powatag-kit-{{site.current_sdk_version}} as a new dependency of your application module by going to File > Project Structure. On tab Dependencies tab click plus button and choose powatag-kit-{{site.current_sdk_version}} module.

4. Now you can import `com.powatag.android.sdk.PowaTagKit` into your app.

<br />

# Using the PowaTag SDK with Maven

You can declare the Maven dependency with the latest available version of the Android SDK:

    <dependency>
        <groupId>com.powatag.android</groupId>
        <artifactId>powatag-kit</artifactId>
         <version>{{site.current_sdk_version}}</version>
    </dependency>
