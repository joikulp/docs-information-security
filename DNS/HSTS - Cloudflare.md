#### What is HTTP Strict Transport Security?

HTTP Strict Transport Security (HSTS, RFC 6797) is a header which allows a website to specify and enforce security policy in client web browsers. This policy enforcement protects secure websites from downgrade attacks, SSL stripping, and cookie hijacking. It allows a web server to declare a policy that browsers will only connect using secure HTTPS connections, and ensures end users do not “click through” critical security warnings. HSTS is an important security mechanism for high security websites. HSTS headers are only respected when served over HTTPS connections, not HTTP.

HSTS generally has the following behavior in user web browsers:

-   Insecure HTTP links become secure HTTPS links
-   SSL certificate warnings or other errors show an error message and cannot be bypassed by the user

#### Considerations

One critical consideration when using HSTS on Cloudflare is that once HSTS is turned on, your website must continue to have a valid HTTPS configuration conforming with the HSTS header to avoid making the website inaccessible to users. If SSL is disabled through other means (“grey clouding” a Flexible SSL website, or moving a website off Cloudflare), it is possible the website will be inaccessible to users for the duration of cached max-age headers, or until HTTPS is re-established and an HSTS header with value 0 is served. Consequently, HSTS configuration requires reading and acknowledging understanding of a warning message.

#### Max-Age Header

HSTS includes a “max-age” parameter which specifies the duration HSTS will continue to be cached and enforced by the web browser. This parameter generally is set at 6 months by default, however you must use a minimum of 12 months if you wish to be included in the HSTS Preload list (see below). The special value of “0” means HSTS is disabled and will no longer be cached by the client web browser. For the amount of time specified in the max-age header after a website is successfully accessed over HTTPS, the browser will enforce this HSTS policy, requiring HTTPS with correctly-configured certificates.

#### Including Subdomains with HSTS

Cloudflare supports the “includeSubDomains” parameter in HSTS headers. This parameter applies the HSTS policy from a parent domain (such as example.com) to subdomains (such as [www.development.example.com](http://www.development.example.com/) or api.example.com). Caution is encouraged with this header, as if any subdomains do not work with HTTPS they will become inaccessible.

#### HSTS Preload

Cloudflare supports HSTS preload. This flag signals to web browsers that a website’s HSTS configuration is eligible for preloading, that is, inclusion into the browser’s core configuration. Without preload, HSTS is only set after an initial successful HTTPS request, and thus if an attacker can intercept and downgrade that first request, HSTS can be bypassed. With preload, this attack is prevented.

Once HSTS is configured, you must visit each browser’s preload submission URL manually. For Chrome, Firefox/Mozilla and Safari use the [Chrome preload list](https://hstspreload.appspot.com/). Microsoft IE HSTS support is being updated.

### Minimum TLS Version

Only allow HTTPS connections from visitors that support the selected TLS protocol version or newer.

TLS 1.0 (default)

API