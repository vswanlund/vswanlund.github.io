---
layout: page
title: Login on Windows Phone
permalink: /tag-mobile-sdks/wp/login/
---

PowaTag Login is a secure and easy way for people to log in to your app and manage their PowaTag Profile.

To facilitate seamless engagement, you can create an temporary user profile for users that do not have an existing PowaTag profile. This temporary profile requires no personal user information upfront because the profile is tied to the device. 

The temporary profile can later be saved allowing the user to use their newly created PowaTag account across multiple devices. However, if the application is deleted or the data is cleared before the profile is saved the account will be irrevocably lost.

Use the <code>LoginManager</code> class to do the following:

<br />

# Checking if the User is Logged In

1. Check if the user has a current access token:

    <pre>if (LoginManager.GetInstance().IsLoggedIn) {
     // User is already logged in
   } else {
     // Go to login screen
   }</pre>

<br />

# Log into an Existing PowaTag Profile

A existing PowaTag user can log in and immediately begin making payments using the payment instruments stored in their PowaTag profile.

There are three ways an existing user can log in using the SDK: 

1. Using a Profile ID
	
	<B>CODE SNIPPED LIKE THIS:</B>

	
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

<B>CODE SNIPPED LIKE THIS:</B>


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

<B>CODE SNIPPED LIKE THIS:</B>

	<pre>EmailSignInDetails emailSignInDetails = new EmailSignInDetails( signInDiag.getEmail(), signInDiag.getPassword());
	LoginManager loginManager = LoginManager.getInstance();
	loginManager.signIn(emailSignInDetails, new PowaTagCallback&lt;Profile&gt;() {
		public void onSuccess(Profile profile) {
			// User is now logged in
			Profile profile = ProfileManager.getInstance().getCurrentProfile();
			Baskets baskets = BasketsManager.getInstance().getCurrentBaskets();
		}
	}</pre>

	
For details on the getter and setter methods available please see the {% if site.sdk_reference_wp_url  %} <a href="{{site.sdk_reference_wp_url}}" target="_blank">SDK Reference Documentation</a><br /> {% else %} SDK reference documentation{% endif %} 
<br/>	



# Log In and Create a Temporary Profile

A temporary or guest user profile lets you build a frictionless PowaTag experience by allowing users to start making payments without requiring a PowaTag account. Guest accounts are deleted after an hour of inactivity.

1. Log in as an anonymous guest user using the LoginManager:

    <pre>LoginManager lm = LoginManager.GetInstance();
   AccessToken accessToken = await lm.GuestLoginAsync();
   // User is now logged in
   Profile profile = ProfileManager.GetInstance().CurrentProfile;
   Baskets baskets = BasketsManager.GetInstance().CurrentBaskets;</pre>

   #DO WE NEED TO DESCRIBE ASYNCHRONOUS METHOD HERE?
   
2. The access token for the currently authenticated user can be retrieved using:

    <pre>AccessToken accessToken = LoginManager.GetInstance().CurrentAccessToken();</pre>

<br />

# After Logging In

Once logged in you can retrieve the [Profile]({{site.baseurl}}/tag-mobile-sdks/wp/profile/) for the current user or get a [Workflow]({{site.baseurl}}/tag-mobile-sdks/wp/workflows/) when a [Trigger]({{site.baseurl}}/tag-mobile-sdks/wp/triggers/) detects a PowaTag.

<br />

# Log Out

Log out from the current profile, removing the current AccessToken and other user data from memory. If the current profile is a temporary profile, all personal user information associated with that account will be deleted.


1. Log out using LoginManager:

    <pre>LoginManager loginManager = LoginManager.GetInstance();
   await loginManager.LogoutAsync();
   // User is now logged out and you can log in as another user</pre>
   
   
      <b>IS ASYNCHRONOUS METHOD DESCRIPTION NEEDED?</b>

   <br/>
   
# Clearing All Login Information 
 
 Whenever you change an endpoint (e.g during development) you will need to clear all user information from the device including the current access token, profile and baskets. Use the <code>clearLogin</code> method to achieve this.
  	 
 CODE SNIPPET
	<pre>loginManager.clearLogin();</pre>
<br/>	

# Sample

To see detailed examples of three methods, [import the HelloPowaTagSample]({{site.baseurl}}/tag-mobile-sdks/wp/start/#importing-the-sample-app) app and review the <code><b>ADD SOME CLASS NAME</b></code> class.
    
<br/>   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   