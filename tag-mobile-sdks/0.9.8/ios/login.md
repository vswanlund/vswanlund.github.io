---
layout: page
title: Login on iOS
permalink: /tag-mobile-sdks/0.9.8/ios/login/
---

PowaTag Login is a secure and easy way for people to log in to your app and manage their PowaTag Profile.

To facilitate seamless engagement, you can create an temporary profile for users that do not have an existing PowaTag profile. This temporary profile requires no personal user information upfront because the profile is tied to the device.

The temporary profile can later be saved allowing the user to use their newly created PowaTag account across multiple devices. However, if the application is deleted or the data is cleared before the profile is saved the account will be irrevocably lost.

To save the temporary profile, making it permanent, use the following steps:

1. Use the <code>PTKLoginManager</code> to [create a temporary profile]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/login#log-in-and-create-a-temporary-profile).
2. Use the <code>PTKProfileManager</code> to [update profile details]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/profile#updating-the-profile). E.g Email and Mobile number. (An optional step that can be done later)
3. Use the <code>PTKProfileManager</code> to [save the temporary profile]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/profile#saving-the-profile).
4. Use the <code>PTKLoginManager</code> to [log into the profile]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/login#log-into-an-existing-powatag-profile) using the profile ID, Email or Mobile number.

	<b>Note:</b> Email and mobile login is only possible if these values have been set on the profile.

<br/>
The <code>PTKLoginManager</code> can be used to do the following:

<br />

# Log In and Create a Temporary Profile

A temporary or guest user profile lets you build a frictionless PowaTag experience by allowing users to start making payments without requiring a PowaTag account. Guest accounts are deleted after an hour of inactivity.

1. Log in as an anonymous get user using the LoginManager:

	<pre>PTKLoginManager *loginManager = [PTKLoginManager sharedManager];
	[loginManager signInAsGuestWithCompletion:^(PTKAccessToken *accessToken, NSError *error) {
		if (accessToken) {
			// User is now logged in
			PTKProfile *profile = [PTKProfileManager sharedManager].currentProfile;
			PTKBaskets *baskets = [PTKBasketsManager sharedManager].currentBaskets;
		}
	}];</pre>


2. The access token for the currently authenticated user can be retrieved using:

	<pre>PTKAccessToken *accessToken = [PTKLoginManager sharedManager].currentAccessToken;</pre>

<br/>

# Log into an Existing PowaTag Profile

A existing PowaTag user can log in and immediately begin making payments using the payment instruments stored in their PowaTag profile.

There are three ways an existing user can log in using the SDK:

1. Log In Using a Profile ID

	<pre>PTKLoginManager *loginManager = [PTKLoginManager sharedManager];
	PTKProfilIdSignInDetails *signInDetails = [PTKProfileIdSignInDetails profileIdSignInDetailsWithProfileId:@"profileId"
		password:@"Password"];

	[loginManager signInWithProfileId:signInDetails;
	completion:^(PTKProfile *__nullable currentProfile, NSError *__nullable error) {
	if (error) {
		// Handle error.
	} else {
		// Handle login success.
		}
	}];</pre>


2. Log In Using a Mobile Number

	<pre>PTKLoginManager *loginManager = [PTKLoginManager sharedManager];
	PTKMobileNumberSignInDetails *signInDetails = [PTKMobileNumberSignDetails mobileNumberSignInDetailsWithMobileNumber:@"71234567"
                                                                                                           password:@"Password"];

	[loginManager signInWithMobileNumber:signInDetails
    completion:^(PTKProfile *__nullable currentProfile, NSError *__nullable error) {
		if (error) {
			// Handle error.
		} else {
			// Handle login success.
		}
	}];</pre>


3. Log In Using an Email Address

	<pre>PTKLoginManager *loginManager = [PTKLoginManager sharedManager];
	PTKEmailSignInDetails *signInDetails = [PTKEmailSignInDetails emailSignInDetailsWithEmail:@"email@email.com"
								password:@"Password"];

	[loginManager signInWithEmail:signInDetails
	completion:^(PTKProfile *__nullable currentProfile, NSError *__nullable error) {
		if (error) {
			// Handle error.
		} else {
		// Handle login success.
		}
	}];</pre>


For details on the getter and setter methods available please see the SDK Reference documentation that is included as part of the SDK.

<br />

# After Logging In

Once logged in you can retrieve the [Profile]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/profile/) for the current user or get a [Workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/workflows/) when a [Trigger]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/triggers/) detects a PowaTag.

<br/>

# Checking if the User is Logged In

1. Check if the user has a current access token:

    <pre>if ([PTKLoginManager sharedManager].isLoggedIn) {
     // User is already logged in
   } else {
     // Go to login screen
   }</pre>

<br />

# Log Out

Log out from the current profile, removing the current AccessToken, baskets and profile data from memory. If the current profile is a temporary profile, all personal user information associated with that account will be deleted.

1. Log out using PTKLoginManager:

    <pre>PTKLoginManager *loginManager = [PTKLoginManager sharedManager];
	[loginManager logoutWithCompletion:^(NSError *__nullable error) {
		if (error) {
			// Handle error
		} else {
			// Logout success.
		}
	}];</pre>

   <br/>

# Sample

To see detailed examples of three methods, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/start/#importing-the-sample-app) app and review the <code>LoginController</code>.

<br/>
