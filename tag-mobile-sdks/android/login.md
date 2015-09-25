---
layout: page
title: Login on Android
permalink: /tag-mobile-sdks/android/login/
---

PowaTag Login is a secure and easy way for people to log in to your app and manage their PowaTag Profile.

To facilitate seamless engangement, you can use a guest login for users that do not have an existing PowaTag profile. This creates a temporary user profile which requires no user information upfront because the profile is tied to the device. 

The temporary profile can later be saved allowing the user to use their newly created PowaTag account across multiple devices. However, if the application is deleted or the data is cleared before the profile is saved the account will be irrevocably lost.

Use the <code>LoginManager</code> class to do the following:

<br />

# Checking if the User is Logged In

1. Check if the user is logged in:

    <pre>if (LoginManager.getInstance().isLoggedIn()) {
     // User is already logged in
   } else {
     // Go to login screen
   }</pre>

<br />

# Log In and Create a Temporary Profile

A temporary or guest user profile lets you build a frictionless PowaTag experience by allowing users to start making payments without requiring a PowaTag account. Guest accounts are deleted after an hour of inactivity.

1. Log in as an anonymous guest user using the LoginManager:
	
    <pre>LoginManager lm = LoginManager.getInstance();
   lm.guestLogin(new PowaTagCallback&lt;AccessToken&gt;() {
     public void onSuccess(AccessToken accessToken) {
       // User is now logged in
       Profile profile = ProfileManager.getInstance().getCurrentProfile();
       Baskets baskets = BasketsManager.getInstance().getCurrentBaskets();
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>
   
   <b>Note:</b> The login manager also provides a synchronous <code>guestLogin()</code> method which should only be used outside of the main thread to avoid performance bottlenecks. For more information please see the Reference documentation in the SDK.

	<pre>public AccessToken guestLogin() throws PowaTagException {</pre>
    ====================================================================
   
   
2. The access token for the currently authenticated user can be retrieved using:
   
    <pre>AccessToken accessToken = LoginManager.getInstance().getCurrentAccessToken();  </pre>

<br/>

# After Logging In

Once the user is logged in you can retrieve the [Profile]({{site.baseurl}}/tag-mobile-sdks/android/profile/) for the current user or get a [Workflow]({{site.baseurl}}/tag-mobile-sdks/android/workflows/) when a [Trigger]({{site.baseurl}}/tag-mobile-sdks/android/triggers/) detects a PowaTag.

<br />

# Log Out

Log out from the current profile, removing the current AccessToken and other user data from memory. If the current profile is a temporary profile, all personal user information associated with that account will be deleted.


1. Log out using LoginManager:

    <pre>LoginManager lm = LoginManager.getInstance();
   lm.logout(new PowaTagCallback&lt;Void&gt;() {
     public void onSuccess(Void result) {
       // User is now logged out and you can log in as another user
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>

	<b>Note:</b> The login manager also provides a synchronous <code>logout()</code> 	 method which should only be used outside of the main thread to avoid performance bottlenecks. For more information please see the Reference documentation in the SDK.

	<pre>public void logout()</pre>
    ===============================

   
    
    
    

 /**
     * Clears the currently authenticated user by clearing all login information from the device including the current access token, profile and baskets.
     * This method does not invalidate the current access token with the server.
     */
    public void clearLogin() {