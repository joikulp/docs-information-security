Based off [this Twitter thread](https://twitter.com/joikulp/status/1544792526686720003?s=20&t=wgrwXAufyQKYXBKNUF3laQ)

![[Pasted image 20220707142513.png]]

# SPF
[[1. How to setup SPF]]
**Sender Policy Framework** is an email authentication method designed to detect forging sender addresses during the delivery of the email. SPF alone, though, is limited to detecting a forged sender claim in the envelope of the email, which is used when the mail gets bounced. Only in combination with DMARC can it be used to detect the forging of the visible sender in emails email spoofing, a technique often used in phishing and email spam.

SPF allows the receiving mail server to check during mail delivery that a mail claiming to come from a specific domain is submitted by an IP address authorized by that domain's administrators. The list of authorized sending hosts and IP addresses for a domain is published in the DNS records for that domain.

**Source:**
https://en.wikipedia.org/wiki/Sender_Policy_Framework
https://datatracker.ietf.org/doc/rfc7208/

# DKIM
[[2. How to setup DKIM]]

**DomainKeys Identified Mail** is an email authentication method designed to detect forged sender addresses in email (email spoofing), a technique often used in phishing and email spam.

DKIM allows the receiver to check that an email claimed to have come from a specific domain was indeed authorized by the owner of that domain.

It achieves this by affixing a digital signature, linked to a domain name, to each outgoing email message. The recipient system can verify this by looking up the sender's public key published in the DNS. A valid signature also guarantees that some parts of the email (possibly including attachments) have not been modified since the signature was affixed. Usually, DKIM signatures are not visible to end-users, and are affixed or verified by the infrastructure rather than the message's authors and recipients.

**Source:**
https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail
https://www.rfc-editor.org/info/rfc6376

# DMARC
[[3. How to setup DMARC]]

**Domain-based Message Authentication, Reporting and Conformance** is an email authentication protocol. It is designed to give email domain owners the ability to protect their domain from unauthorized use, commonly known as email spoofing.

DMARC brings SPF and DKIM together, DMARC states the policy for breaking SPF and DKIM rules. Receiving mail-server will reject emails if DMARC policy is to reject any emails that break the rules.

You can tell the receiving mail-server to report any rule breaking via email. When implementing DMARC it's common practice to make receiving server report but not reject for a month or so to know about the mail flowing out to not break anything important.

**Source:**
https://en.wikipedia.org/wiki/DMARC
https://datatracker.ietf.org/doc/html/rfc7489