# How Web2 Infrastructure Attacks Target Web3 Systems

**Author:** Vektasafe  
**Category:** Cybersecurity Research  
**Topic:** Web2 attack vectors on Web3 infrastructure  

---

## Overview

The dominant narrative in blockchain security focuses on smart contract vulnerabilities -- reentrancy, flash loan exploits, oracle manipulation. These are real and costly. But a parallel and frequently underreported attack surface exists at the infrastructure layer: the Web2 systems that Web3 projects depend on every day.

Domain name servers, cloud hosting providers, frontend code repositories, API key management, email accounts, social media channels, and employee devices -- none of these are decentralised. They are standard Web2 infrastructure, and they are targeted constantly.

A 2023 analysis by Chainalysis found that approximately 80% of funds stolen from crypto projects were taken not through smart contract exploits but through attacks on surrounding infrastructure. The contracts worked exactly as designed. The humans and systems around them did not.

This document covers the primary Web2 attack classes used against Web3 targets, with documented real-world incidents for each.

---

## 1. DNS Hijacking

### What It Is

The Domain Name System (DNS) translates human-readable domain names into IP addresses. When a user types app.uniswap.org into a browser, DNS tells the browser which server to connect to. If an attacker gains control of a project's DNS records, they can redirect all traffic to a server they control -- serving a fake frontend that looks identical to the real one.

### How It Happens

DNS hijacking typically occurs through one of three routes:

- Compromising the domain registrar account (weak password, no MFA, phishing the account owner)
- Exploiting vulnerabilities in the DNS provider's own infrastructure
- BGP hijacking to redirect DNS queries at the routing level (covered separately below)

### Real Incident -- Curve Finance (2022)

In August 2022, Curve Finance's frontend at curve.fi was hijacked via a DNS attack. The attacker gained access to the domain's DNS settings through the registrar iwantmyname and pointed the domain to a malicious server. Users visiting the legitimate URL were served a cloned frontend with a contract approval prompt that drained their wallets. Approximately 570,000 USD was stolen before the attack was identified and the DNS records restored.

The smart contracts were untouched. The vulnerability was a Web2 registrar account.

### Mitigations

- Enable registrar lock (also called domain lock) to prevent unauthorised transfers or record changes
- Use hardware security keys for MFA on all registrar and DNS provider accounts
- Monitor DNS records continuously with automated alerting on any changes
- Consider DNSSEC (DNS Security Extensions) to cryptographically sign DNS records

---

## 2. BGP Hijacking

### What It Is

Border Gateway Protocol (BGP) is the routing protocol that directs internet traffic between autonomous systems -- the large networks operated by ISPs, cloud providers, and major organisations. BGP was designed for trust between known peers, not adversarial environments. An attacker who can announce false BGP routes can redirect traffic intended for a legitimate server to a server they control, intercepting or manipulating it in transit.

### How It Happens

BGP hijacking is typically carried out by state-level actors, compromised ISPs, or attackers who have gained access to a router operated by a BGP peer. It is more sophisticated than most Web2 attacks but has been used against cryptocurrency infrastructure specifically because of the high value of the targets.

### Real Incident -- Amazon Route 53 and MyEtherWallet (2018)

In April 2018, attackers executed a BGP hijack against Amazon's Route 53 DNS service. By announcing false BGP routes, they redirected DNS queries for MyEtherWallet (MEW) to a server they controlled in Russia. Users who visited myetherwallet.com were served a phishing site with a fake SSL certificate. The attack lasted approximately two hours and resulted in approximately 17 million USD stolen from users who approved transactions on the fake site.

The MEW smart contracts and backend were not compromised. The attack was entirely at the routing and DNS layer.

### Mitigations

- Use BGP route origin validation (ROV) and RPKI (Resource Public Key Infrastructure) where possible
- Distribute frontend infrastructure across multiple regions and providers to reduce single points of failure
- Monitor for unexpected SSL certificate issuance via Certificate Transparency logs
- Implement HSTS (HTTP Strict Transport Security) with long max-age values and preloading

---

## 3. Frontend Repository Compromise

### What It Is

Most Web3 project frontends are hosted as static sites, often with code stored on GitHub and deployed automatically to services like Vercel, Netlify, or Cloudflare Pages. If an attacker gains access to the GitHub repository or the deployment pipeline, they can inject malicious JavaScript into the frontend that drains user wallets silently on approved interactions.

### How It Happens

- Compromising a developer's GitHub account (phishing, credential stuffing, session token theft)
- Compromising a third-party npm package that the frontend depends on (supply chain attack)
- Gaining access to the CI/CD pipeline credentials
- Social engineering a project contributor into merging a malicious pull request

### Real Incident -- Ledger Connect Kit (2023)

In December 2023, an attacker gained access to a former Ledger employee's npm account through a phishing attack. The compromised account had publish rights to the @ledgerhq/connect-kit package, which is used by a large number of DeFi frontends including SushiSwap, Kyber Network, and others. The attacker published a malicious version of the package that injected a wallet drainer into every frontend that loaded it. Approximately 600,000 USD was stolen within hours before the package was taken down.

No smart contracts were exploited. The attack was entirely through the npm supply chain.

### Mitigations

- Enable npm two-factor authentication for all package publish operations
- Pin dependency versions and use lockfiles -- avoid floating version ranges
- Audit third-party dependencies regularly with tools like npm audit and Snyk
- Implement Subresource Integrity (SRI) checks on externally loaded scripts
- Use GitHub branch protection rules and require code review before merging
- Rotate credentials immediately when contributors leave the project

---

## 4. API Key and Private Credential Exposure

### What It Is

Web3 projects routinely use API keys for RPC providers (Alchemy, Infura, QuickNode), cloud services (AWS, GCP), monitoring tools, and communication platforms. Private keys for hot wallets used in operations are also frequently stored in environment variables or configuration files. Exposure of these credentials -- through public repository commits, misconfigured cloud storage, or compromised developer machines -- gives attackers direct access to funds or infrastructure.

### How It Happens

- Accidentally committing .env files or private keys to a public GitHub repository
- Storing credentials in plaintext in cloud storage buckets with public access
- Hardcoding API keys in frontend JavaScript that is shipped to users
- Malware on a developer's machine extracting credentials from memory or files

### Real Incident -- Ronin Network (2022)

While the Ronin bridge hack involved validator key compromise rather than a public credential leak, the attack vector was fundamentally a credential security failure. Attackers (later attributed to the Lazarus Group) gained access to five of the nine Ronin validator private keys -- four through a compromised Sky Mavis system and one through a backdoored PDF sent to an employee. The result was 625 million USD stolen in the largest DeFi hack to date.

The smart contracts performed exactly as designed. The attack was entirely through credential and endpoint compromise.

### Mitigations

- Never commit secrets to version control -- use .gitignore and pre-commit hooks to prevent accidental exposure
- Use secret scanning tools (GitHub Secret Scanning, truffleHog, gitleaks) to detect existing leaks
- Store secrets in dedicated secret management systems (AWS Secrets Manager, HashiCorp Vault)
- Rotate all credentials immediately upon any suspected exposure
- Use hardware security modules (HSMs) for high-value key storage
- Implement the principle of least privilege -- each service should have access only to what it needs

---

## 5. Phishing and Social Engineering

### What It Is

Social engineering attacks target the humans in a system rather than the technical infrastructure. In the Web3 context this includes phishing emails targeting developers and executives, fake job offers delivering malware, Discord and Telegram impersonation, and SIM swapping attacks to bypass SMS-based two-factor authentication.

### How It Happens

- Spear phishing emails impersonating investors, partners, or service providers
- Fake job recruitment campaigns (common vector used by Lazarus Group) that deliver malware through fake coding assignments
- Discord server compromise -- gaining admin access and posting fake announcements with malicious links
- SIM swapping -- convincing a mobile carrier to transfer a target's phone number to an attacker-controlled SIM, bypassing SMS MFA

### Real Incident -- Axie Infinity / Ronin (2022)

The Ronin network compromise referenced above was initiated through a fake job offer. A senior Ronin engineer was approached on LinkedIn with a fraudulent employment opportunity. As part of the recruitment process they were sent a PDF containing malware. This gave attackers initial access to Sky Mavis internal systems from which they eventually extracted validator keys. The technical sophistication of the final attack was made possible by a simple social engineering opening.

### Real Incident -- Mixin Network (2023)

In September 2023, Mixin Network lost approximately 200 million USD after attackers compromised the database of their cloud service provider. Initial access was obtained through a phishing attack targeting a Mixin employee. Once inside the cloud environment, attackers accessed private keys stored in the database.

### Mitigations

- Train all team members to recognise phishing and social engineering attempts
- Use hardware security keys (FIDO2/WebAuthn) for all critical account MFA -- eliminate SMS-based 2FA
- Establish out-of-band verification procedures for any high-value requests (transfers, key operations)
- Treat all unsolicited job offers, investment approaches, and partnership requests with heightened scrutiny
- Implement a security-aware culture where reporting suspected phishing is encouraged

---

## 6. Cloud Infrastructure Misconfiguration

### What It Is

Web3 projects use cloud infrastructure (AWS, GCP, Azure) for backend services, databases, monitoring, and key management. Misconfigured cloud resources -- publicly accessible S3 buckets, overly permissive IAM roles, exposed management interfaces -- provide attackers with direct access to sensitive data and systems.

### How It Happens

- S3 buckets or cloud storage set to public read/write by default or misconfiguration
- Overly broad IAM policies granting more access than necessary
- Management interfaces (SSH, RDP, admin dashboards) exposed to the public internet without restriction
- Unused access keys that are never rotated or revoked
- Logging and monitoring disabled, allowing attackers to operate undetected

### Mitigations

- Run regular cloud security posture assessments using tools such as AWS Security Hub, Prowler, or ScoutSuite
- Apply the principle of least privilege to all IAM roles and service accounts
- Enable CloudTrail (AWS) or equivalent audit logging across all regions
- Restrict management interface access to known IP ranges using security groups and VPC configurations
- Enable MFA delete on S3 buckets containing sensitive data
- Conduct regular access reviews and revoke unused credentials

---

## Summary

| Attack Class | Primary Target | Example Incident | Estimated Loss |
|--------------|---------------|-----------------|----------------|
| DNS Hijacking | Domain registrar account | Curve Finance (2022) | 570,000 USD |
| BGP Hijacking | Internet routing infrastructure | MyEtherWallet (2018) | 17,000,000 USD |
| Frontend Repository Compromise | npm / GitHub / CI pipeline | Ledger Connect Kit (2023) | 600,000 USD |
| API Key / Credential Exposure | Developer machines, cloud storage | Ronin Network (2022) | 625,000,000 USD |
| Phishing / Social Engineering | Employees and developers | Axie Infinity / Ronin (2022) | 625,000,000 USD |
| Cloud Misconfiguration | Cloud infrastructure | Mixin Network (2023) | 200,000,000 USD |

---

## Conclusion

Smart contract auditing is a necessary discipline. It is not a sufficient one. The attack surface of a Web3 project extends far beyond the contracts themselves -- into the registrars, cloud providers, package registries, developer machines, and communication channels that surround them.

A project can have flawless Solidity and lose everything through a phishing email or a misconfigured S3 bucket. Security at the contract layer and security at the infrastructure layer are not alternatives. They are both required.

The auditor who understands both layers is not just more valuable -- they are categorically different from one who understands only one.

---

## References

- Chainalysis Crypto Crime Report 2023
- Curve Finance DNS incident post-mortem (August 2022)
- MyEtherWallet BGP hijack analysis -- Oracle and ARIN (2018)
- Ledger Connect Kit supply chain attack analysis (December 2023)
- Ronin Network incident report -- Sky Mavis (2022)
- Mixin Network security incident statement (September 2023)
- NIST SP 800-207 -- Zero Trust Architecture
- SWC Registry -- Smart Contract Weakness Classification
