# app-password-persistence
Using Microsoft 365 app passwords for persistent access to a compromised account
# Preface
What’s an app password?

After you turn on two-step verification or set up the Authenticator app, you may run into issues if you use apps or older devices (like Windows Phone 8 and Xbox 360) that don't support two-step verification.

If you have two-step verification turned on and an app isn't prompting you to enter a security code when you sign in, you may be able to sign in with an app password instead. An app password is a long, randomly generated password that you provide only once instead of your regular password when signing in to an app or device that doesn't support two-step verification.

You only need to create an app password if you have two-step verification turned on and are using an app that doesn't support it.

Source: https://support.microsoft.com/en-us/help/12409/microsoft-account-app-passwords-and-two-step-verification

In 2020 the applications that don’t support modern authentication is the exception rather than the rule. For a secure by default approach Microsoft shouldn’t enable app passwords by default on tenants, that is not the current configuration, app passwords are enabled by default when MFA is enabled for the users. 

# Compromised account with MFA enabled and app passwords enabled can lead to persistent access
If a user resets their password or a Global Administrator resets the user’s password it doesn’t revoke access in my testing. There are other methods for persistent access such as malicious 3rd party apps in Office 365 outlined by Brian Krebs and Phishlabs (https://krebsonsecurity.com/2020/01/tricky-phish-angles-for-persistence-not-passwords/)

Step 1: Hard part phish a user with MFA enabled. Thankfully good ole BHIS has a blog post and an app for that.

If you have physical access: An enterprising attacker could create a Rubber Ducky payload script that can be deployed to computer with an account that is logged into Microsoft 365. A pretext for being able to have a target plug in a USB to simply print a document for you. An administrative assistant in a lobby may have been delegated access to various executive email/calendar. Microsoft doesn’t allow for app password creation via PowerShell which would make create a Rubber Ducky (https://shop.hak5.org/products/usb-rubber-ducky-deluxe) payload much easier.

# Concern:
Revoking app passwords isn’t something that most IT Admins know they should be doing when they are dealing with an account that they suspect to be compromised.  It also is not part of Microsoft guidance  (EDIT they added it to their documentation 8/13/2020) on responding to compromised accounts. In Microsoft’s defense they claim that MFA alone prevents 99.9% of phishing attacks.

# How to create an app password:
MS Official documentation: https://support.microsoft.com/en-us/office/create-an-app-password-for-microsoft-365-3e7c860f-bda4-4441-a618-b53953ee1183?ui=en-us&rs=en-us&ad=us
 
To create an app password there aren’t any additional MFA prompts.

If you haven’t used an app password before:
I logged using my app password on an iPhone running iOS 13.3 via the mail account creation wizard. I believe any iOS device running 12.x and newer will be able to use an app password.

# Recommended mitigations:
* Block legacy auth, You should already be doing this and in fact Microsoft has plans to make this a default setting in the near future.
OR
* Disable app passwords on the tenant.
   * Settings, Services and addons, Azure Multifactor
* If you are unable to disable app passwords, your SIEM should alert on app password creation.
 
