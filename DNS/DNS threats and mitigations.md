# DNS threats and mitigations
## Overview
* [[DNSSEC]]
* [[DNSSEC - Cloudflare]]
* [[HSTS - Cloudflare]]
* [[CAA record]]

## Threats and mitigations

### DoS, DDoS, and DNS amplification attacks
Denial-of-service (DoS) attacks and distributed-denial-of-service (DDoS) attacks are two forms of the same thing. They’re what most people think of when they think of a DNS attack. In both cases, attackers flood internet servers with so many requests that they simply can’t answer them all, and the system crashes as a result.

**How to mitigate:**
Use a good DNS provider such as Cloudflare. Cloudflare has good a DDOS mitigation.


### DNS tunneling
DNS tunneling transmits information through the DNS protocol that usually resolves network addresses.

Normal DNS requests only contain the information necessary to communicate between a client and a server. DNS tunneling inserts an additional string of data into that pathway. It establishes a form of communication that bypasses most filters, firewalls, and packet capture software.

That makes it especially hard to detect and to trace its origin.

DNS tunneling can establish command and control. Or, it can exfiltrate data. Information is often broken up into smaller pieces, moved throughout DNS, and reassembled on the other end.

**How to mitigate:**
Malware protection and patching endpoints

### DNS poisoning and cache poisoning
DNS poisoning (also known as DNS spoofing) and its cousin, DNS cache poisoning, use security gaps in the DNS protocol to redirect internet traffic to malicious websites. These are sometimes called man-in-the-middle attacks.

When your browser goes out to the internet, it starts by asking a local DNS server to find the IP address for a website name. The local DNS server will ask the root servers that own that domain, and then ask that domain’s authoritative name server for the address.

DNS poisoning happens when a malicious actor intervenes in that process and supplies the wrong answer. Once it has tricked the browser into thinking that it received the right answer to its query, the malicious actor can divert traffic to whatever fake website it wants.

**How to mitigate:**
[[DNSSEC]]
[[DNSSEC - Cloudflare]]
[[HSTS - Cloudflare]] - might help as well

### Typosquatting
Top 5 DNS Security ThreatsThe practice of registering a domain name that is confusingly similar to an existing popular brand – typosquatting -- is often considered a problem for trademark attorneys. However, as recent research has demonstrated, it can present a profound risk to the confidentiality of corporate secrets and should be increasingly thought of as a security problem.

**How to mitigate:**
Find lookalike domains that adversaries can use to attack you. This tool can detect typosquatters, phishing attacks, fraud, and brand impersonation. Useful as an additional source of targeted threat intelligence.
https://github.com/elceef/dnstwist

### Registrar Hijacking
The majority of domain names are registered via a registrar company, and these represent single points of failure. If an attacker can compromise your account with your chosen registrar, they gain control over your domain name, allowing them to point it to the servers of their choice, including name servers, Web servers, email servers, etc. Worse still, the domain could be transferred to a new owner or to an “offshore” registrar, making domain name recovery a complex matter.

**How to mitigate:**
1. Enable two-factor authentication on registrar's website
2. Use a strong password on registrar's website
3. Enable domain locking
4. Enable whois protection