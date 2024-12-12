# Networking Protocols - A Cheatsheet for Common Questions

**Q1. Explain how 'www.abc.ghc.com' works**

**A1.**  The process involves several key networking protocols and steps:

**1. URL Parsing and Handling:**

   * The browser first checks if the entered text is a valid URL (with a protocol like HTTP or HTTPS) or a search term.
   * If it's a search term, it's passed to the default search engine, often with special text appended to indicate it came from the browser's address bar. 
   * **Why?** This allows search engines to understand user behavior and provide more relevant results.

**2. Punycode Encoding:**

   * If the hostname contains non-ASCII characters (e.g., internationalized domain names), Punycode encoding is applied to convert it into a valid ASCII format.

**3. HSTS (HTTP Strict Transport Security):**

   * The browser checks its HSTS preload list for the website. This list contains sites that have requested to be accessed only over HTTPS.
   * If the site is on the list or has previously requested HTTPS, the browser will use HTTPS directly.
   * **Downgrade Attack:** If the site is not on the list and doesn't enforce HTTPS, the initial connection could be vulnerable to a downgrade attack, where an attacker forces the use of unencrypted HTTP.

**4. DNS Lookup:**

   * **a. Browser Cache:** The browser checks its own DNS cache for the domain's IP address. (You can view Chrome's cache at `chrome://net-internals/#dns`.) Cache entries typically have a TTL (Time-to-Live) of around 1 minute.
   * **b. OS Cache:** If not found in the browser cache, the browser calls the operating system's `gethostbyname` function to check the OS DNS cache (TTL is usually around 1 day).
   * **c. Recursive Resolver:** If the IP address is not in the OS cache, the browser contacts a recursive DNS resolver, usually provided by your ISP or local router. This resolver handles the remaining steps of the DNS lookup process.

**5. ARP Process (Address Resolution Protocol):**

   * Before sending a DNS request, the browser needs the MAC address of the next hop (either the DNS server or the default gateway). This is where ARP comes in.
   * **a. ARP Cache:** The system checks its ARP cache for the target IP address and its corresponding MAC address.
   * **b. ARP Route Table:** If not in the cache, the system consults the ARP routing table to determine if the target IP is on a directly connected subnet. If not, the default gateway's subnet is used.
   * **c. MAC Address Lookup:** The system then determines the MAC address of the network interface that will be used to send the request.
   * **d. ARP Request and Reply:** An ARP request is sent on the local network. The format of the reply depends on the network topology:
      * **Directly Connected:** If the router is directly connected, it responds with an ARP reply containing its MAC address.
      * **Hub/Switch:** If a hub or switch is used, the router will still receive the ARP request and respond with its MAC address.
   * **e. ARP Reply Contents:** The ARP reply includes the target IP address, target MAC address, sender IP address, and sender MAC address.

**6. DNS Process:**

    Queries are iterative or recursive. Recursive queries find the final IP address and return that to the browser. Iterative queries return the next device's IP and the browser continues asking for the IP.

   * **a. Recursive vs. Iterative Queries:** DNS resolvers can use either recursive or iterative queries. 
      * **Recursive:** The resolver handles the entire lookup process, querying other DNS servers as needed, and returns the final IP address to the client.
      * **Iterative:** The resolver only provides the IP address of the next DNS server in the hierarchy. The client then sends a query to that server, and so on, until the authoritative DNS server for the domain is reached.
   * **b. DNS Hierarchy:** The recursive resolver starts by querying a root DNS server. The root server provides the address of a top-level domain (TLD) server (e.g., `.com`). The resolver then queries the TLD server, which provides the address of the authoritative nameserver for the specific domain (`ghc.com` in this case). Finally, the resolver queries the authoritative nameserver to get the IP address of `www.abc.ghc.com`.

**7. TCP Connection Establishment (for HTTP or HTTPS):**

   * Once the browser has the IP address, it initiates a TCP connection with the web server on port 80 (HTTP) or 443 (HTTPS). This involves a three-way handshake (SYN, SYN-ACK, ACK) to establish a reliable connection.

**8. HTTP Request:**

   * The browser sends an HTTP request to the web server, specifying the desired resource (e.g., the webpage at `/`). This request includes headers with information like the browser type, accepted languages, and any cookies.

**9. HTTP Response:**

   * The web server processes the request and sends back an HTTP response. This response includes headers (e.g., content type, status code) and the requested content (HTML, images, etc.).

**10. Page Rendering:**

   * The browser receives the HTTP response and parses the HTML, CSS, and JavaScript to render the webpage. It also downloads any associated resources like images, videos, and scripts.

**11. HTTPS (if used):**

   * If HTTPS is used, an additional step of TLS/SSL handshake occurs after the TCP connection to establish a secure, encrypted channel. This ensures data confidentiality and integrity.

This detailed explanation covers the key steps and protocols involved in accessing a website, providing a comprehensive answer for interview situations. Remember to emphasize your understanding of the underlying concepts and the interactions between different protocols.
