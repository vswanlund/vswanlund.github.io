---
layout: page
title: Login on Windows Phone
permalink: /tag-mobile-sdks/0.9.6/wp/login/
---

PowaTag Login is a secure and easy way for people to log in to your app and manage their PowaTag Profile.

To facilitate seamless engagement, you can create an temporary profile for users that do not have an existing PowaTag profile. This temporary profile requires no personal user information upfront because the profile is tied to the device.

The temporary profile can later be saved allowing the user to use their newly created PowaTag account across multiple devices. However, if the application is deleted or the data is cleared before the profile is saved the account will be irrevocably lost.

To save the temporary profile, making it permanent, use the following steps:

1. Use the <code>LoginManager</code> to [create a temporary profile]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/login#log-in-and-create-a-temporary-profile).
2. Use the <code>ProfileManager</code> to [update profile details]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/profile#updating-the-profile). E.g Email and Mobile number. (An optional step that can be done later)
3. Use the <code>ProfileManager</code> to [save the temporary profile]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/profile#saving-the-profile).
4. Use the <code>LoginManager</code> to [log into the profile]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/login#log-into-an-existing-powatag-profile) using the profile ID, Email or Mobile number.

	<b>Note:</b> Email and mobile login is only possible if these values have been set on the profile.

<br/>
The <code>LoginManager</code> can be used to do the following:

<br />

# Log In and Create a Temporary Profile

A temporary or guest user profile lets you build a frictionless PowaTag experience by allowing users to start making payments without requiring a PowaTag account. Guest accounts are deleted after an hour of inactivity.

1. Log in as an anonymous guest user using the LoginManager:

	<pre>LoginManager loginManager = LoginManager.GetInstance();
	AccessToken accessToken = await loginManager.GuestLoginAsync();
	// User is now logged in
	Profile profile = ProfileManager.GetInstance().CurrentProfile;
	Baskets baskets = BasketsManager.GetInstance().CurrentBaskets;</pre>


2. The access token for the currently authenticated user can be retrieved using:

    <pre>AccessToken accessToken = LoginManager.GetInstance().CurrentAccessToken();</pre>

<br />

# Log into an Existing PowaTag Profile

A existing PowaTag user can log in and immediately begin making payments using the payment instruments stored in their PowaTag profile.

There are three ways an existing user can log in using the SDK:

1. Log In Using a Profile ID

	<pre>ProfileIdSignInDetails profileIdSignInDetails = new ProfileIdSignInDetails(signInDiag.ProfileId, signInDiag.Password);
	LoginManager loginManager = LoginManager.GetInstance();
	Profile newProfile = await loginManager.SignInAsync(profileIdSignInDetails);
	// User is now logged in
	Profile profile = ProfileManager.GetInstance().GetCurrentProfile();</pre>


2. Log In Using a Mobile Number

	<pre>MobileNumberSignInDetails mobileNumberSignInDetails = new MobileNumberSignInDetails(signInDiag.MobileNumber, signInDiag.Password);
	LoginManager loginManager = LoginManager.GetInstance();
	Profile profile = await loginManager.SignInAsync(mobileNumberSignInDetails);</pre>


3. Log In Using an Email Address

	<pre>EmailSignInDetails emailSignInDetails = new EmailSignInDetails(signInDiag.Email, signInDiag.Password);
	LoginManager loginManager = LoginManager.GetInstance();
	Profile profile = await loginManager.SignInAsync(emailSignInDetails);</pre>


For details on the getter and setter methods available please see the SDK Reference documentation that is included as part of the SDK.
<br/>

# After Logging In

Once logged in you can retrieve the [Profile]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/profile/) for the current user or get a [Workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/workflows/) when a [Trigger]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/triggers/) detects a PowaTag.

<br />

# Checking if the User is Logged In

1. Check if the user has a current access token:

    <pre>if (LoginManager.GetInstance().IsLoggedIn) {
     // User is already logged in
   } else {
     // Go to login screen
   }</pre>

<br />

# Log Out

Log out from the current profile, removing the current AccessToken, baskets and profile data from memory. If the current profile is a temporary profile, all personal user information associated with that account will be deleted.

1. Log out using LoginManager:

    <pre>LoginManager loginManager = LoginManager.GetInstance();
	await loginManager.LogoutAsync();
	// User is now logged out and you can log in as another user</pre>

<br/>

# Sample

To see detailed examples of three methods, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/0.9.6/wp/start/#importing-the-sample-app) app and review the <code>MainPageViewModel</code> class.

<br/>
