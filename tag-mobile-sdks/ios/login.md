---
layout: page
title: Login on iOS
permalink: /tag-mobile-sdks/ios/login/
---

PowaTag Login is a secure and easy way for people to log in to your app and manage their PowaTag Profile.

To facilitate seamless engagement, you can create an temporary user profile for users that do not have an existing PowaTag profile. This temporary profile requires no personal user information upfront because the profile is tied to the device. 

The temporary profile can later be saved allowing the user to use their newly created PowaTag account across multiple devices. However, if the application is deleted or the data is cleared before the profile is saved the account will be irrevocably lost.

Use the <code>LoginManager</code> class to do the following:

<br />

# Checking if the User is Logged In

1. Check if the user has a current access token:

    <pre>if ([PTKLoginManager sharedManager].isLoggedIn) {
     // User is already logged in
   } else {
     // Go to login screen
   }</pre>

<br />

# Log In and Create a Temporary Profile

A temporary or guest user profile lets you build a frictionless PowaTag experience by allowing users to start making payments without requiring a PowaTag account. Guest accounts are deleted after an hour of inactivity.

1. Log in as an anonymous get user using the LoginManager:

    <pre>PTKLoginManager *lm = [PTKLoginManager sharedManager];
   [lm guestLoginWithCompletion:^(PTKAccessToken *accessToken, NSError *error) {
     if (accessToken) {
       // User is now logged in
       PTKProfile *profile = [PTKProfileManager sharedManager].currentProfile;
       PTKBaskets *baskets = [PTKBasketsManager sharedManager].currentBaskets;
     }
   }];</pre>

   
   #DO WE NEED TO DESCRIBE ASYNCHRONOUS METHOD HERE
   
   
2. The access token for the currently authenticated user can be retrieved using:

    <pre>PTKAccessToken *accessToken = [PTKLoginManager sharedManager].currentAccessToken;</pre>

<br />

# After Logging In

Once logged in you can retrieve the [Profile]({{site.baseurl}}/tag-mobile-sdks/ios/profile/) for the current user or get a [Workflow]({{site.baseurl}}/tag-mobile-sdks/ios/workflows/) when a [Trigger]({{site.baseurl}}/tag-mobile-sdks/ios/triggers/) detects a PowaTag.

# Log Out

Log out from the current profile, removing the current AccessToken and other user data from memory. If the current profile is a temporary profile, all personal user information associated with that account will be deleted.

1. Log out using PTKLoginManager:

    <pre>PTKLoginManager *lm = [PTKLoginManager sharedManager];
   [lm guestLoginWithCompletion:^(NSError *error) {
     if (!error) {
       // User is now logged out and you can log in as another user
     }
   }];</pre>
   
   #IS ASYNCHRONOUS METHOD DESCRIPTION NEEDED?

   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   