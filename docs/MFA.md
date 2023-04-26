# Multi-Factor Authentication (MFA)

Multi-Factor Authentication (MFA) is a tenchqiue employed to strength the process of authenticating against a service.
In a typical situation you would use a set of credentials, such as a username and a passwords or keys to validate your identity.
By adding an additional way of confirming the identity of an user we can more securely of authenticating that such an user holds the identity is attempting to validate.

There are a few different ways to implement this, for instance, financial institutions --such as banks-- would use a code sent to your cell-phone or older technologies included the utilization of pre-distributed codes in the form cards or usb devices generating specific sequences of codes assigned to the corresponding user.

Another way to implement this strategy is by the use of the so-called *One Time Password* (OTP) following the same premises as described above.

The way this technique works is by sharing a common "root" or source of information, and then based on a predefine prescription generate sequences of codes using this initial 'state'; pretty similar to how *pseudo-random number generation* (PRNG) works as well.
Not so surprisingly then, at the core of many MFA implementations is a PRNG algorithm, some of them will use an "initial" value (aka seed), some will use the actual time as such, making them a *time-based* token.

Among some of the most used MFA tools are:

- Google Authenticator -- https://github.com/google/google-authenticator
  An open-source, time-based implementation for MFA.
  
- DUO -- https://duo.com
  A propietary implementation, offering different ways to authentication.

- YubiKeys -- https://www.yubico.com
  Hardware propietary tokens.
  
- PrivacyIdea -- https://www.privacyidea.org/


---
*Last Modified: Oct. 12, 2022*  --  v 0.1

