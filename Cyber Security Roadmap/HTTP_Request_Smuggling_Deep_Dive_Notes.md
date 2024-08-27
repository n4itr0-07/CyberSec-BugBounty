### HTTP Request Smuggling: Deep Dive Notes

**Overview:**
HTTP Request Smuggling is a sophisticated web vulnerability that occurs when an attacker exploits discrepancies in the interpretation of HTTP requests between front-end and back-end servers. This attack can lead to unauthorized actions, information disclosure, and other security breaches.

**Key Concepts:**
- **Front-End Server:** The server that directly receives HTTP requests from clients (e.g., a load balancer, proxy, or CDN).
- **Back-End Server:** The server that processes the HTTP requests forwarded by the front-end server (e.g., application server, API server).

**Types of HTTP Request Smuggling:**
1. **TE.CL (Transfer-Encoding to Content-Length):**
   - Occurs when the front-end server processes requests based on `Transfer-Encoding: chunked` while the back-end server uses `Content-Length` headers.
   - Exploit involves sending a request with both headers where the front-end processes `Transfer-Encoding`, and the back-end uses the malformed `Content-Length`.

2. **CL.TE (Content-Length to Transfer-Encoding):**
   - Occurs when the front-end uses `Content-Length`, and the back-end server uses `Transfer-Encoding: chunked`.
   - Exploit involves sending a request with a `Content-Length` that is different from the actual body length, leading the back-end to interpret part of the body as a separate request.

3. **TE.TE (Transfer-Encoding to Transfer-Encoding):**
   - Both servers use `Transfer-Encoding: chunked`, but interpret the request differently.
   - The attacker can craft a request where one server sees the body differently, allowing a smuggled request.

4. **CL.CL (Content-Length to Content-Length):**
   - Both servers use `Content-Length`, but the attacker manipulates it to desynchronize request parsing between them.
   - This form is less common but still possible in specific configurations.

**Attack Scenarios:**
- **Example Attack Vector:**
   1. Attacker sends a specially crafted HTTP request to the front-end server.
   2. The front-end server forwards the request to the back-end server, where parsing discrepancies cause the back-end to interpret two requests instead of one.
   3. The attacker’s smuggled request is executed, leading to unauthorized actions.

- **Real-World Example:**
   - A vulnerable server setup with a reverse proxy might process a smuggled request as a valid administrative action, allowing the attacker to bypass authentication and escalate privileges.

**Exploitation Steps:**
1. **Identify Potential Vulnerability:**
   - Check the HTTP headers and server behavior for discrepancies in `Transfer-Encoding` and `Content-Length` handling.
   - Use tools like Burp Suite’s HTTP Request Smuggler to detect possible vulnerabilities.

2. **Craft the Malicious Request:**
   - Create a request with mismatched headers to exploit the identified discrepancy.
   - Example of a TE.CL attack:
     ```http
     POST / HTTP/1.1
     Host: vulnerable-website.com
     Transfer-Encoding: chunked
     Content-Length: 50
     ```
     ```
     0

     GET /admin HTTP/1.1
     Host: vulnerable-website.com
     ```

3. **Send the Request:**
   - Deliver the crafted request to the front-end server.
   - Observe the back-end server's response to determine if the attack was successful.

**Defense Mechanisms:**
- **Synchronize Header Parsing:** Ensure that front-end and back-end servers interpret `Content-Length` and `Transfer-Encoding` headers consistently.
- **Disable HTTP/1.1 Pipelining:** Prevent multiple HTTP requests from being sent over the same connection, mitigating the attack.
- **Use Web Application Firewalls (WAFs):** Employ WAFs that can detect and block suspicious HTTP requests, including potential smuggling attempts.
- **Regular Patching:** Keep servers, proxies, and load balancers up to date with security patches to mitigate known vulnerabilities.

**Common Vulnerable Configurations:**
- **Misconfigured Load Balancers:** Load balancers or proxies that mishandle `Content-Length` or `Transfer-Encoding` headers.
- **Outdated Servers:** Older versions of web servers or application servers that do not handle HTTP/1.1 features securely.

**Testing Tools:**
- **Burp Suite:** Burp’s HTTP Request Smuggler extension is a powerful tool for detecting and exploiting request smuggling vulnerabilities.
- **Smuggle Attack (OWASP ZAP):** Another tool for testing HTTP request smuggling, integrated into the OWASP ZAP framework.
- **Custom Scripts:** Python or similar scripting languages can be used to craft and send custom HTTP requests to test for vulnerabilities.

**Detection and Mitigation:**
- **Server Logs:** Regularly review server logs for anomalies that might indicate request smuggling attempts, such as unexpected request sequences.
- **Traffic Analysis:** Analyze network traffic for unusual patterns that could suggest request smuggling, particularly when multiple servers are involved.

**Conclusion:**
HTTP Request Smuggling is a critical web application vulnerability that can be exploited to perform various malicious actions, including bypassing security controls and executing unauthorized requests. A thorough understanding of how different servers interpret HTTP headers, coupled with proactive detection and mitigation strategies, is essential for protecting web applications from this complex threat.