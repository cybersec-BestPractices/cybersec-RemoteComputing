# CyberSecurity Glossary

## Cyber-Security/Defense Matrix
Under the premise that security attacks, vulnerabilities and eventually breaches will occur; cybersecturity experts develop strategies and protocols to follow in the occurrence of these events.
One way to organize and categorize these is by employing the so-called *cyber defense matrix* where among others, elememts such as, risk, layer or stratum at which the incident occur or was detected, action to be taken, etc. are arranged.


## Social Engineering
One of the weakest element in any cybersecurity infrastructure is the so-called *human factor*, i.e. the employment of individuals to actually infiltrate and geopardize systems. This can indeed take different forms, e.g. via email manipulation or impersonation --e.g. spam, phishing attempts--, or even convincing individuals of pluging physical devices such as USB sticks of unkown procedence in their computers, etc.
The most direct form of these attack techniques even target specific individuals by learning and correspondingly acting based on someone's typical preferences or behaviors.
The generic term employed to describe this type of attacks is *social engineering*, as they are designed and calibrated to the specific idiosyncrasy of the victim's target.
These attacks are still responsible for large number of cybersecurity breaches, and has been reported that even robust implementations, such as the utilization of MFA combied with other authentication mechansims, could be overcome by convincing and carefully crafted manipulation.
One of the best advices agaisnt this type of manipulative attacks is to always remain vigilant and suspicious, in particular do NOT trust any sources of unknown procedence or origin.

   - "Social engineering in cybersecurity: The evolution of a concept", J.M.Hatfield; Computers & Security 73 (2018)
     https://doi.org/10.1016/j.cose.2017.10.008


## PQC - Post Quantun Cryptography
With the recent advances of quantum computers, one of the potential applications and immediate concers is the capability for "powerful" enough quantum devices to *break* the encryption alogorithm used nowadays.
At the beggining of 2017, the NIST launched a request for propossals to develop standars to develop Post-Quantum Cryptographic (PQC) algorithms.
Further information about this ongoing effort can be found in the following links:

   - "NIST / Post-Quantum Cryptography" - Accessed: June 14, 2023
      https://csrc.nist.gov/Projects/post-quantum-cryptography/selected-algorithms-2022
   - "Post-quantum cryptography", Bernstein, Lange; Nature 549 (2017)
     https://www.nature.com/articles/nature23461
   - "Cisco / Post Quantum Security Brief" - Accessed: June 14, 2023
     https://www.cisco.com/c/en/us/products/collateral/optical-networking/solution-overview-c22-743948.html

---

# Terms and Acronyms

* `AES`
   Advanced Encryption Standard (symmetric)
* `DES`
   Data Encryption Standard -- **unsecure** deprecated, replaced by AES (https://www.rfc-editor.org/rfc/rfc4772.txt)
* `HTTP`|`HTTPS`
     HyperText Transfer Protocol, secure hypertext transfer protocol
* `MFA` | `2FA`
     Multi-Factor (or Two-Factor) Authentication, see [MFA](./MFA.md)
* `OTP`
     One Time Password
* `PGP`
     Pretty Good Privacy
* `PQC`
     Post-Quantum Cryptography
* `RSA`
     Rivest-Shamir-Adelman algorithm (asymmetric)
* `SHA`
     Secure Hash Algorithm
* `ssh`
    Secure Shell, see [ssh](./ssh-summary.md)
* `VPN`
    Virtual Private Network, see [VPN](./VPN.md)
* `VNC`
    Virtual Network Computing, see [VNC](./VNC.md)

---

*Last Modified: Jun. 14, 2023* -- v 1.0
