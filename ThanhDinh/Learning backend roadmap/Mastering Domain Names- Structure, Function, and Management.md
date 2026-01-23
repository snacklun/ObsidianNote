## Briefing Document: Understanding Domain Names

This briefing document summarizes key concepts related to domain names, their structure, function, and management, drawing from the provided excerpts from "What is a Domain Name?" (MDN) and "What is a domain name? | Domain names vs. URLs | Cloudflare."

### 1. What is a Domain Name?

A domain name is a **human-readable address** used to access websites and other internet resources. It serves as an easy-to-remember alternative to complex numerical IP addresses (e.g., IPv4 or IPv6 addresses) that computers use to identify each other on the internet.

- **MDN states:** "Domain names are a key part of the Internet infrastructure. They provide a human-readable address for any web server available on the Internet."
- **Cloudflare defines it as:** "A unique, easy-to-remember address used to access websites, such as ‘google.com’, and ‘facebook.com’."
- **Purpose:** To solve the problem of people having "a hard time finding out who is running the server or what service the website offers" and remembering "hard to remember" IP addresses, as noted by MDN.

### 2. Domain Name System (DNS) and IP Addresses

The Domain Name System (DNS) is the critical infrastructure that translates human-friendly domain names into the machine-readable IP addresses required for internet communication.

- **Cloudflare explains:** "The actual address of a website is a complex numerical IP address (e.g. 192.0.2.2), but thanks to DNS, users are able to enter human-friendly domain names and be routed to the websites they are looking for. This process is known as a DNS lookup."

1. **DNS Lookup Process (MDN):**User types a domain name (e.g., mozilla.org) into their browser.
2. Browser checks a local DNS cache for the IP address.
3. If not found, the computer asks a DNS server to match the domain name to its corresponding IP address.
4. Once the IP address is known, the browser can connect and negotiate content with the web server.

- **DNS Refreshing (MDN):** DNS information is stored on servers worldwide. Updates from registrars are propagated by "authoritative name servers" to all other DNS servers. This process takes "some time" as servers periodically query authoritative servers for updated information.

### 3. Structure of Domain Names

Domain names have a hierarchical structure, read from right to left, with each part separated by a dot.

- **MDN emphasizes:** "A domain name has a simple structure made of several parts (it might be one part only, two, three…), separated by dots and **read from right to left**."
- **Components (Cloudflare and MDN):Top-Level Domain (TLD):** The rightmost part (e.g., .com, .org, .net, .uk, .gov). TLDs can indicate the general purpose or geographical location of a service.
- **MDN examples:** .gov for government departments, .edu for educational institutions, local TLDs like .us or .fr for specific countries or languages.
- **Cloudflare notes:** TLDs include "‘generic’ TLDs such as ‘.com’, ‘.net’, and ‘.org’, as well as country-specific TLDs like ‘.uk’ and ‘.jp’."
- The full list of TLDs is maintained by ICANN (MDN).
- **Labels (or Components) / Secondary Level Domain (SLD) / Third Level Domain (3LD):** These are the parts to the left of the TLD.
- The label directly before the TLD is often called the Secondary Level Domain (SLD) (MDN, Cloudflare).
- Further labels to the left are called Third Level Domains (3LDs) or subdomains (Cloudflare, MDN).
- **Cloudflare example:** In google.co.uk, .uk is the TLD, .co is the 2LD (indicating a company), and google is the 3LD.
- Labels are "case-insensitive character sequences anywhere from one to sixty-three characters in length, containing only the letters A through Z, digits 0 through 9, and the '-' character" (MDN).

### 4. Domain Names vs. URLs

A Uniform Resource Locator (URL) is a broader term that includes the domain name along with other information.

- **Cloudflare clarifies:** "A uniform resource locator (URL), sometimes called a web address, contains the domain name of a site as well as other information, including the protocol and the path."
- **Example (Cloudflare):** In https://cloudflare.com/learning/, cloudflare.com is the domain name, https is the protocol, and /learning/ is the path.

### 5. Domain Name Ownership and Registration

Users do not "buy" or "own" domain names; instead, they **pay for the right to use them** for a specified period, typically one or more years, with the option to renew.

- **MDN states:** "You cannot 'buy a domain name'." This prevents "unused domain names that were locked and couldn't be used by anyone."
- **Registration Process:**Domain names are managed by **domain registries**, which delegate the reservation to **registrars** (Cloudflare, MDN).
- To get a domain name, one goes to a registrar's website, uses their "Get a domain name" feature, fills out required details (ensuring correct spelling), and pays (MDN).
- Registrars "keep track of technical and administrative information connecting you to your domain name" (MDN).
- **Checking Availability (MDN):**Use a registrar's "whois" service on their website.
- Alternatively, use the whois command in a system's shell (e.g., whois mozilla.org). A "NOT FOUND" response indicates availability.
- **Security and Trust in Registrars (Cloudflare):** It is crucial to choose a "trustworthy registrar" to avoid predatory practices such as "domain squatting" (buying expired domains and reselling them at high prices) or "domain hijacking" (malicious parties taking control). Registrars are responsible for notifying registrants about upcoming expirations.

### 6. Importance of Domain Names

- **Human-Readability:** Makes internet navigation intuitive and user-friendly, as names are easier to remember than numerical IP addresses (MDN, Cloudflare).
- **Identification:** Provides a clear identity for websites and services, indicating their purpose or origin (MDN).
- **Stability:** Domain names can remain consistent even if the underlying IP address of a server changes, preventing broken links and ensuring continuous access (MDN implies this by stating IP addresses "might change over time").