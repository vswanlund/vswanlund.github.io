---
layout: page
title: Login on Windows Phone
permalink: /tag-mobile-sdks/wp/login/
---

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

# Log In and Create a Temporary Profile

A temporary or guest user profile lets you build a frictionless PowaTag experience by allowing users to start making payments without requiring a PowaTag account. Guest accounts are deleted after an hour of inactivity.

1. Log in as an anonymous guest user using the LoginManager:

    <pre>LoginManager lm = LoginManager.GetInstance();
   AccessToken accessToken = await lm.GuestLoginAsync();
   // User is now logged in
   Profile profile = ProfileManager.GetInstance().CurrentProfile;
   Baskets baskets = BasketsManager.GetInstance().CurrentBaskets;</pre>

   #DO WE NEED TO DESCRIBE ASYNCHRONOUS METHOD HERE?
   
2. The current access token for the user can also be retrieved using:

    <pre>AccessToken accessToken = LoginManager.GetInstance().CurrentAccessToken();</pre>

<br />

# After Logging In

Once logged in you can retrieve the [Profile]({{site.baseurl}}/tag-mobile-sdks/wp/profile/) for the current user or get a [Workflow]({{site.baseurl}}/tag-mobile-sdks/wp/workflows/) when a [Trigger]({{site.baseurl}}/tag-mobile-sdks/wp/triggers/) detects a PowaTag.

<br />

# Log Out

1. Log out using LoginManager, if the current profile is temporary this will delete the profile:

    <pre>LoginManager lm = LoginManager.GetInstance();
   await lm.LogoutAsync();
   // User is now logged out and you can log in as another user</pre>

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   