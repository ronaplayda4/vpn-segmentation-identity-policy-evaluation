# Network Security Evaluation: VPN Segmentation and Identity Policy Review

## Project Overview

This project documents a network security evaluation completed in a controlled GNS3 virtual lab. The assessment focused on two risks: excessive network reachability from a remote-access segment and weak Active Directory password controls.

Connectivity testing, OPNsense firewall review, and PowerShell policy queries were used to validate the findings and develop practical remediation recommendations.

## Objectives

- Evaluate whether the remote-access endpoint could reach unauthorized internal systems
- Review the VPN firewall policy for least-privilege enforcement
- Distinguish network reachability from confirmed service access
- Evaluate domain password and account-lockout controls
- Identify accounts with password-expiration exceptions
- Recommend controls that reduce lateral-movement and credential risks

## Lab Environment and Tools

- GNS3
- OPNsense firewall
- Windows endpoints and servers
- Active Directory
- Windows PowerShell
- ICMP connectivity testing
- PowerShell `Test-NetConnection`
- RFC1918 private lab networks

## Key Findings

### Excessive VPN reachability

- The VPN interface contained an overly permissive `pass in quick on em2 inet all` rule.
- The remote-access endpoint reached an internal IT workstation using ICMP.
- RDP port 3389 and SMB port 445 tests failed.
- The evidence confirmed unnecessary network-layer reachability but did not prove successful login, RDP access, SMB access, or unrestricted access to every internal subnet.

### Weak identity and password controls

- The domain password minimum was seven characters.
- The account-lockout threshold was disabled.
- Multiple human and administrator accounts had `PasswordNeverExpires` enabled.
- Complexity and password history were enabled, but account-level exceptions weakened the applied controls.

## Risk

An overly broad VPN rule could allow a compromised remote endpoint to perform internal discovery or attempt lateral movement. Long-lived credentials and unlimited failed authentication attempts increase exposure to password guessing, reuse, and spraying.

## Recommendations

- Replace the VPN allow-all rule with source-, destination-, protocol-, and port-specific rules
- Permit access only to required administration services and destinations
- Add explicit deny-and-log rules for unauthorized internal networks
- Review firewall logs for scanning and repeated denied connections
- Remove unjustified `PasswordNeverExpires` exceptions
- Use managed service accounts or controlled credential rotation for service identities
- Require stronger passphrases and block common or compromised passwords
- Require MFA for administrators and remote access
- Configure reasonable lockout or smart-lockout protections
- Review authentication logs and security-sensitive account exceptions periodically

## Skills Demonstrated

- Network segmentation analysis
- Firewall-rule review
- Least-privilege assessment
- Connectivity and service validation
- Active Directory password-policy analysis
- PowerShell administration
- Evidence-based reporting
- Risk-based remediation planning

## Report

[View the sanitized network security evaluation](Network_Security_Evaluation_VPN_Segmentation_Identity_Policy_Rona_Playda.pdf)

## Disclaimer

This project was completed in a controlled virtual lab. It does not contain production customer data. The displayed IP addresses are non-routable RFC1918 lab addresses. Course identifiers, assignment language, metadata, and potentially identifying command-prompt paths were removed from the public edition.

## Analyst

**Rona Playda**  

