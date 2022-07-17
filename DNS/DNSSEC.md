Domain Name System Security Extensions (DNSSEC) allow registrants to digitally sign information they put into the Domain Name System (DNS). This protects consumers by ensuring DNS data that has been corrupted, either accidentally or maliciously, doesn't reach them.

Two sides of DNSSEC must be enabled for it to work.

1. Registrants, who are responsible for publishing DNS information, must ensure their DNS data is DNSSEC–signed.
2. Network operators need to enable DNSSEC validation on their resolvers that handle DNS lookups for users.

# DNSSEC
Every DNS zone has a _public/private key pair_. The zone owner uses the zone's _private key_ to sign DNS data in the zone and generate digital signatures over that data. As the name "private key" implies, this key material is kept secret by the zone owner. The zone's _public key_, however, is published in the zone itself for anyone to retrieve. Any recursive resolver that looks up data in the zone also retrieves the zone's public key, which it uses to _validate_ the authenticity of the DNS data. The resolver confirms that the digital signature over the DNS data it retrieved is valid. If so, the DNS data is legitimate and is returned to the user. If the signature does not validate, the resolver assumes an attack, discards the data, and returns an error to the user.

DNSSEC adds two important features to the DNS protocol:

-   _Data origin authentication_ allows a resolver to cryptographically verify that the data it received actually came from the zone where it believes the data originated.
-   _Data integrity protection_ allows the resolver to know that the data hasn't been modified in transit since it was originally signed by the zone owner with the zone's private key.

# Trusting DNSSEC keys
Every zone publishes its public key, which a recursive resolver retrieves to validate data in the zone. But how can a resolver ensure that a zone's public key itself is authentic? A zone's public key is signed, just like the other data in the zone. However, the public key is not signed by the zone's private key, but by the _parent zone's_ private key. For example, the _icann.org_ zone's public key is signed by the _org_ zone. Just as a DNS zone's parent is responsible for publishing a child zone's list of authoritative name servers, a zone's parent is also responsible for vouching for the authenticity of its child zone's public key. Every zone's public key is signed by its parent zone, except for the root zone: it has no parent to sign its key.

The root zone's public key is therefore an important starting point for validating DNS data. If a resolver trusts the root zone's public key, it can trust the public keys of top-level zones signed by the root's private key, such as the public key for the _org_ zone. And because the resolver can trust the public key for the _org_ zone, it can trust public keys that have been signed by their respective private key, such as the public key for _icann.org_. (In actual practice, the parent zone doesn't sign the child zone's key directly--the actual mechanism is more complicated--but the effect is the same as if the parent had signed the child's key.)

The sequence of cryptographic keys signing other cryptographic keys is called a _chain of trust_. The public key at the beginning of a chain of trust is a called a _trust anchor_. A resolver has a list of trust anchor_s_, which are public keys for different zones that the resolver trusts implicitly. Most resolvers are configured with just one trust anchor: the public key for the root zone. By trusting this key at the top of the DNS hierarchy, a resolve can build a chain of trust to any location in the DNS name space, as long as every zone in the path is signed.


Source: https://www.icann.org/resources/pages/dnssec-what-is-it-why-important-2019-03-05-en