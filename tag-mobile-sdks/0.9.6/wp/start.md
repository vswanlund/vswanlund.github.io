---
layout: page
title: Getting Started with Windows Phone SDK
permalink: /tag-mobile-sdks/0.9.6/wp/start/
---

The PowaTag SDK for Windows Phone is the easiest way to integrate your Windows Phone app with PowaTag.

It enables:

* Triggers - Your app can react to PowaTag tags placed around the environment.
* Workflows - Respond to tags by providing appropriate and contextual user journeys.
* Baskets - Users can add products to a basket for purchase from PowaTag merchants to using your app.
* Payments - Users can easily pay for the products they selected using your app.

<br />

# Requirements

PowaTag SDK for Windows Phone runs on devices with Windows Phone 8.0 or higher.

<br/>

# Install the SDK with NuGet

To use PowaTag SDK in a project, add it as a build dependency and import it.

1. Select the 'Tool' tab in Visual Studio and find NuGet Package Manager, then select Manage NuGet Packages for Solution:

    <img src="{{ '/images/powatag_mobile_sdks_wp_start_nuget.png' | prepend: site.baseurl }}" />

2. In a Manage NuGet Packages window, click the 'Online' tab, choose 'All' and Search Online `Ctrl+E` for "PowaTag".

3. Install the PowaTag SDK. Now you can import `PowaTag.WindowsPhone.Sdk.PowaTagKit` into your project.

<br />

# Initialize the SDK

You need to initialize PowaTag SDK before you can use it. Please use the API key and secret that was provided to you during registration.


Add a call to <code>PowaTagKit.InitializeSdk</code> from the constructor of your `Application` subclass:

	public App()
	{
		string endpoint = getAlternateEndpoint();
		PowaTagKit.InitializeSdk(App.API_KEY, App.SECRET, PowaTagEndpoint.DefaultEndpointPorts(new Uri(endpoint)));
	}


<br/>

# Importing The Sample App

The **HelloPowaTagSample** app is included with the SDK to provide you with examples of the main PowaTag SDK features.

You can experiment with the SDK features by importing the app into into Visual Studio.

The sample has a project dependency rather than a central repository dependency via NuGet. This is so that when a local copy of the SDK gets updates, the samples reflect the changes.

<br />

# Next Steps

After you install PowaTag SDK for Windows Phone, you can see:

* [Login]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/login/)
* [Profile]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/profile/)
* [Triggers]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/triggers/)
* [Workflows]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/workflows/)
* [Baskets]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/baskets/)
* [Campaigns]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/campaigns/)
* [Acts]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/acts/)
* [Payments]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/payments/)

<br />

# Install the SDK Manually

1. Extract the SDK Zip into a folder.

2. In Solution Explorer, find 'References' of your project and click right mouse button on it and choose 'Add reference...'

    <img src="{{ '/images/powatag_mobile_sdks_wp_start_manual.png' | prepend: site.baseurl }}" />

3. Open Assemblies and click 'Browse...'

4. Select "PowaTagKit.dll" from the Library folder of the ZIP you extracted earlier and click 'Add'

5. Build your project. Now you can import `PowaTag.WindowsPhone.Sdk.PowaTagKit` into your app.
