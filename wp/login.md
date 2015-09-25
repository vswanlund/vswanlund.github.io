---
layout: page
title: Login on Windows Phone
permalink: /tag-mobile-sdks/wp/login/
---

PowaTag Login is a secure and easy way for people to log in to your app and manage their PowaTag Profile.

To facilitate seamless engagement, you can create a temporary user profile for which no personably identifiable user information is required up-front using the `LoginManager.GuestLoginAsync` method. The profile is tied to the device and if the application is deleted or the data is cleared before the profile is saved the account will be irrevocably lost.

A temporary profile can later be saved allowing the user to use their PowaTag account across multiple devices.

<br />

# Checking if the User is Logged In

1. Check if the user has a current access token:

    <pre>if (LoginManager.GetInstance().IsLoggedIn) {
     // User is already logged in
   } else {
     // Go to login screen
   }</pre>

<br />

# Log In as a Guest

A temporary or guest user profile lets you build a frictionless PowaTag experience by allowing users to start making payments without requiring a PowaTag account. Guest accounts are deleted after an hour of inactivity.

1. Log in as an anonymous get user using the LoginManager:

    <pre>LoginManager lm = LoginManager.GetInstance();
   AccessToken accessToken = await lm.GuestLoginAsync();
   // User is now logged in
   Profile profile = ProfileManager.GetInstance().CurrentProfile;
   Baskets baskets = BasketsManager.GetInstance().CurrentBaskets;</pre>

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
