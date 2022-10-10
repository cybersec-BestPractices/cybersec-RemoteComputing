
| Action        | Description           | Mitigation            |
|---------------|-----------------------|-----------------------|
| keep software up-to-date | keep your devices updated with all software updates, including OS and applications | zero-day exploits, bugs, known vulnerabilities |
|		|                       |  mitigates the risk of the remote computing system being compromised via the end user workstation  |
| use ssh to connect to remote systems | de-facto tool to connect to remote systems using asymmetric encryption | MITM attacks, packet interception (sniffing) |
| use ssh-keys | more efficient and convenient way to authenticate | key-loggers, stolen credentials |
| use ssh-keys + MFA  | enhanced way to authenticate | stolen private key |
| verify fingerprint of remote system | checks validity and authenticity of remote system by comparing system's fingerprints with publicly reported ones | MITM attacks, IP spoofing |
| connect through VPN | improves network protection and privacy by creating an encrypted channel over unsecured networks such as the Internet | MITM attacks, sensitive data exposure |
| firewall | "middle-ware" (hardware and/or software) to intercept and filter potential attacks  | brute-force attacks, malicious network traffic |
| use an antivirus | local protection against wide spectrum of malware | multiple types of malware |
|            |                          |  mitigates the risk of the remote computing system being compromised via the end user workstation |
| use a passwords manager | specialized tool to more securely (i.e. using encryption) store passwords and generate strong passwords, which is useful if SSH keys as an authentication method  is not available  | password stealing, password brute-force  |
| encrypted signed email | enhance authenticity and validity of email communications | MITM attacks, impersonation |



Summary of some best practices for end users to enhance cybersecurity in remote computing.
