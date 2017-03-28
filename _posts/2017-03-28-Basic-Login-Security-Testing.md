---
layout: post
published: true
title: Login Security Testing
---
In this post I will be outlining some concepts when testing a Login box for a web application.  Hopefully you can learn a thing or two which can be applied in more places than a simple login form.  You would think a simple login box can be covered in a miniscule amount of testcases, its pretty straight forward right? **wrong**.

For the purpose of this tutorial, we will assume a the login box is similar to this one:
![Image taken from premiumpixels.com]({{site.baseurl}}/http://turbo.premiumpixels.com/wp-content/uploads/2011/06/preview.jpg)

### The Basics

**Valid Login** -> Correct username and password combo -> User is successfully logged in.

**Invalid Login** -> Incorrect username(or) password -> User is unable to login.  **note:** Check for an error message giving away any sort of data, for example a correct username returns - "The password is incorrect for this username".  This is username enumeration and should be highlighted immediately.  Other things to consider are is there some sort of lockout capabilities for _n_ incorrect passwords? combined with username enumeration and no validation/verification can be **deadly** for a public facing external website. (WHY? -> A hacker can farm out your usernames due to the enumeration, they can safely know if the username was a valid one, simply password spamming/brute forcing these usernames will create a Denial-Of-Service for your users.

**Empty Criteria** -> Login provides appropriate client-side validation, user is clearly alerted that they are missing key data.

**Page Resources** -> Load up the google chrome developer console (F12) and hit your login page, pay attention to the resources which are attained (generally GET requests) and make sure there is nothing erroring out, perhaps a bad Asset path/directory to jquery, css classes etc.  

**Enable/Disabling Remember Me** -> If remember me is true, then the username will be remembered on next login.  If Disabled the username will be empty on next login.  Things like remembering the username on login A, then disabling it again during Login B, what is the status during Login C?

**Multi-browser/Devices** -> Does the page display well when using a wealth of devices? what about different browsers, do a simple test or two using those.  Consider disabling javascript in the browser and see how the page holds up.

**Submitting/Deleting Data** -> Submit using the enter key in the password/login fields, is the form submitted? does delete erase the characters properly?  How about whitespace in the username/password is it accounted for?

**Password Readability** -> Type into the password field, is it starred / asterisks?  If not this is a problem which should be highlighted, a shoulder surfer could easily grab the credentials.  Consider copying and pasting from the password field too, when pasted it should **not** display the password from the user.

**Successful and Failed Logins** -> Is there some database audit occuring? logging any successful or even failed login attempts?  Careful with failed login captures as a brute forcing program has an increased chance to bload your database or crash your system.

**Unauthed Access** -> Login as a valid user and grab a url once inside, maybe something like localhost:8080/Messaging.  Log back out and try hit this url directory without logging in, the user should not be able to access the page.

**User Access?** -> Is there functionality in the system to delete or block out a user for a period of time? if so try login as a deleted user or one that is temp blocked from logging in, both instance should return a failed login.

**Change password** -> Change a users password, can they now login successfully with the new one? **yes,** can they login with the old one? **no.**.  Is there password expiration functionality, check that the password expiration works as intended.

**Fresh user** -> Can a freshly created account actually login?

**Authentification** -> Is there a multiple-step authorisation process? are there secret answer functionality? if so these need checked.

**Check password maxLength attribute** -> This is one very little people will even think of checking, Ensure firstly the password maxLength matches up with the administrator side for changing and setting passwords.  Imagine my login password is a maximum of 10 characters, but when changing a password as an admin its 15 characters, I can create a password that **cannot** be used.  At the same time ensure the password field is **not** unlimited.  This is potentially exposing yourself, in the past I have encountered a bug using a bespoke android system where entering a unbeleivably login password crashed the application handling logins allowing free access to the user.

**Priviledges** -> Logged in user can only see things which are appropriate for their level.

**Login, Close Browser** -> When Logging in and closing your browser, ensure the user is not automatically logged in when they launch the application again later.  This should also consider logging out and pressing the (back) button in the browser.  

**Password changes** -> Check if the user or admin can change password that they adhere to the initial application password policy, e.g capitals, numbers, symbols etc.

**General Layout/Usability** -> Page looks good collectively and is a positive User Experience.

### Advanced

**Form submit is POST** -> Ensure the form data is being POSTED to the server

**Automation friendly** -> Ensure any elements, especially textboxes and or buttons have good locators, consider using id where possible, if there is no id attribute consider highlighting it to the developers to add to make automation on the product much easier and effecient.

**SQL Injection** -> Enter **'OR''='** as username and or password, are you able to login or get any useful data/information back from the login?

**Capability** -> Logging in as the same user? should this be possible? Consider exploring multiple devices if this should **not** be allowed, e.g login on firefox and a tablet.  

**Performance** -> Consider Logging in as multiple users at the same time and record latency, this will give us a starting point for performance, does the time to login increase exponentially? do things crash? has the server buckled with just 20 users?  Consider doing some simple navaigation and logging out again as a bit of a soak test

** Ensure Https** -> Ensure HTTPS is being used, we don't want somebody sniffing packets and stealing a plaintext password from an internet cafe etc.

** Anti-brute force measures** -> Ensure there is some sort of anti brute force protection, things like Captcha's etc, we don't want to allow a hacker to bombard the server continiously with no repercussions.

**Password Encryption** -> Ensure the passwords are properly encrypted.  Especially in the end database, we don't want plaintext passwords stored in our production database, this is a pending disaster.

**Error Handling** -> Ensure error handling has been well designed, invalid characters for example e.g - ╬ should not be a valid username, especially at the registration stage.  null inputs, white space.

**Authentification Offline** -> If the backend/database authentification is offline what happens? is anything exposed to the user? if so this should be highlighted immediately, best practice would simply be to deny the login.

**Leave the system idle once logged in** -> Session should expire and the user will be taken out to relogin again after _x_ amount of time.

**Inspecting page source** -> Ensure no code is visible that could be used to expose the system or data.  or even hint at something a hacker could use and utilise to gain an entry or advantage.  Things like hidden fields can be exposed etc.













