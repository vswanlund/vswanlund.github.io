---
layout: page
title: Login on iOS
permalink: /tag-mobile-sdks/ios/login/
---

PowaTag Login is a secure and easy way for people to log in to your app and manage their PowaTag Profile.

To facilitate seamless engangement, you can create a temporary user profile for which no personably identifiable user information is required up-front using the `PTKLoginManager guestLoginWithCompletion` method. The profile is tied to the device and if the application is deleted or the data is cleared before the profile is saved the account will be irrevocably lost.

A temporary profile can later be saved allowing the user to use their PowaTag account across multiple devices.

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

2. The current access token for the user can also be retrieved using:

    <pre>PTKAccessToken *accessToken = [PTKLoginManager sharedManager].currentAccessToken;</pre>

<br />

# After Logging In

Once logged in you can retrieve the [Profile]({{site.baseurl}}/tag-mobile-sdks/ios/profile/) for the current user or get a [Workflow]({{site.baseurl}}/tag-mobile-sdks/ios/workflows/) when a [Trigger]({{site.baseurl}}/tag-mobile-sdks/ios/triggers/) detects a PowaTag.

# Log Out

1. Log out using PTKLoginManager, if the current profile is temporary this will delete the profile:

    <pre>PTKLoginManager *lm = [PTKLoginManager sharedManager];
   [lm guestLoginWithCompletion:^(NSError *error) {
     if (!error) {
       // User is now logged out and you can log in as another user
     }
   }];</pre>
