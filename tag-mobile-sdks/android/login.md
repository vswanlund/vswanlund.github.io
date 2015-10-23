---
layout: page
title: Login on Android
permalink: /tag-mobile-sdks/android/login/
---

PowaTag Login is a secure and easy way for people to log in to your app and manage their PowaTag Profile.

To facilitate seamless engagement, you can create an temporary profile for users that do not have an existing PowaTag profile. This temporary profile requires no personal user information upfront because the profile is tied to the device. 

The temporary profile can later be saved allowing the user to use their newly created PowaTag account across multiple devices. However, if the application is deleted or the data is cleared before the profile is saved the account will be irrevocably lost.

When saving the temporary profile use the following steps:

1. [Create a guest profile]({{site.baseurl}}/tag-mobile-sdks/android/login/).
2. Update Profile (optional) email, mobile
3. Save the profile
4. Log into the profile using the id,email or phone with profile id (or email/phone number if already added to the profile)



Use the <code>LoginManager</code> class to do the following:

<br />

# Log In and Create a Temporary Profile

A temporary or guest user profile lets you build a frictionless PowaTag experience by allowing users to start making payments without requiring a PowaTag account. Guest accounts are deleted after an hour of inactivity.

1. Log in as an anonymous guest user using the LoginManager:
	
    <pre>LoginManager lm = LoginManager.getInstance();
   lm.signInAsGuest(new PowaTagCallback&lt;AccessToken&gt;() {
     public void onSuccess(AccessToken accessToken) {
       // Guest user is now logged in
       Profile profile = ProfileManager.getInstance().getCurrentProfile();
       Baskets baskets = BasketsManager.getInstance().getCurrentBaskets();
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>
   
   <b>Note:</b> The login manager also provides a synchronous <code>signInAsGuest()</code> method which should only be used outside of the main thread to avoid performance bottlenecks. For more information please see the Reference documentation included in the SDK.

   
   
2. The access token for the currently authenticated user can be retrieved using:
   
    <pre>AccessToken accessToken = LoginManager.getInstance().getCurrentAccessToken();  </pre>

<br/> 

# Log into an Existing PowaTag Profile

A existing PowaTag user can log in and immediately begin making payments using the payment instruments stored in their PowaTag profile.

There are three ways an existing user can log in using the SDK: 

1. Using a Profile ID

	<pre>ProfileIdSignInDetails profileIdSignInDetails = new ProfileIdSignInDetails( signInDiag.getProfileId(), signInDiag.getPassword());
	LoginManager loginManager = LoginManager.getInstance();
	loginManager.signIn(profileIdSignInDetails, new PowaTagCallback&lt;Profile&gt;() {
		public void onSuccess(Profile profile) {
			// User is now logged in
			Profile profile = ProfileManager.getInstance().getCurrentProfile();
			Baskets baskets = BasketsManager.getInstance().getCurrentBaskets();
		}
	}</pre>


2. Using a Mobile Number

	<pre>MobileNumberSignInDetails mobileNumberSignInDetails = new MobileNumberSignInDetails( signInDiag.getMobileNumber(), signInDiag.getPassword());
	LoginManager loginManager = LoginManager.getInstance();
	loginManager.signIn(mobileNumberSignInDetails, new PowaTagCallback&lt;Profile&gt;() {
		public void onSuccess(Profile profile) {
			// User is now logged in
			Profile profile = ProfileManager.getInstance().getCurrentProfile();
			Baskets baskets = BasketsManager.getInstance().getCurrentBaskets();
		}
	}</pre>

	
3. Using an Email Address

	<pre>EmailSignInDetails emailSignInDetails = new EmailSignInDetails( signInDiag.getEmail(), signInDiag.getPassword());
	LoginManager loginManager = LoginManager.getInstance();
	loginManager.signIn(emailSignInDetails, new PowaTagCallback&lt;Profile&gt;() {
		public void onSuccess(Profile profile) {
			// User is now logged in
			Profile profile = ProfileManager.getInstance().getCurrentProfile();
			Baskets baskets = BasketsManager.getInstance().getCurrentBaskets();
		}
	}</pre>

	
For details on the getter and setter methods available please see the SDK Reference documentation that is included as part of the SDK.
<br/>	

# After Logging In

Once the user is logged in you can retrieve the [Profile]({{site.baseurl}}/tag-mobile-sdks/android/profile/) for the current user or get a [Workflow]({{site.baseurl}}/tag-mobile-sdks/android/workflows/) when a [Trigger]({{site.baseurl}}/tag-mobile-sdks/android/triggers/) detects a PowaTag.

<br />

# Checking if the User is Logged In

1. Check if the user is logged in:

    <pre>if (LoginManager.getInstance().isLoggedIn()) {
     // User is already logged in
   } else {
     // Go to login screen
   }</pre>

<br />

# Log Out

Log out from the current profile, removing the current AccessToken, baskets and profile data from memory. If the current profile is a temporary profile, all personal user information associated with that account will be deleted.


1. Log out using LoginManager:

    <pre>LoginManager loginManager = LoginManager.getInstance();
   loginManager.logout(new PowaTagCallback&lt;Void&gt;() {
     public void onSuccess(Void result) {
       // User is now logged out and you can log in as another user
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>

	<b>Note:</b> The login manager also provides a synchronous <code>logout()</code> method which should only be used outside of the main thread to avoid performance bottlenecks. For more information please see the Reference documentation included in the SDK.

<br/>
	
# Sample

To see detailed examples of three methods, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/android/start/#importing-the-sample-app) app and review the <code>WelcomeActivity</code> class.
    
<br/>


