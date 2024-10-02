# HTTP Request Smuggling: A Comprehensive Guide

HTTP Request Smuggling (HRS) is a sophisticated vulnerability that arises due to discrepancies in how front-end (load balancers, proxies) and back-end (origin) servers process HTTP requests. When exploited, it allows attackers to interfere with the sequence of requests sent to a server, potentially leading to unauthorized access, data exfiltration, or even complete compromise of web applications.

This guide aims to explore the entire topic of HTTP Request Smuggling, from its fundamental concepts to advanced exploitation techniques.

## Table of Contents
1. [Introduction to HTTP Request Smuggling](#introduction-to-http-request-smuggling)
2. [Basic Concepts](#basic-concepts)
    - [HTTP Request Anatomy](#http-request-anatomy)
    - [Chunked Transfer Encoding](#chunked-transfer-encoding)
    - [HTTP/1.1 vs HTTP/2](#http1-vs-http2)
    - [Role of Proxies and Load Balancers](#role-of-proxies-and-load-balancers)
3. [How HTTP Request Smuggling Works](#how-http-request-smuggling-works)
4. [Types of HTTP Request Smuggling](#types-of-http-request-smuggling)
    - [CL.TE (Content-Length vs Transfer-Encoding)](#cl-te-content-length-vs-transfer-encoding)
    - [TE.CL (Transfer-Encoding vs Content-Length)](#te-cl-transfer-encoding-vs-content-length)
    - [CL.CL (Content-Length vs Content-Length)](#cl-cl-content-length-vs-content-length)
5. [Vulnerability Scenarios](#vulnerability-scenarios)
    - [Scenario 1: Exploiting a vulnerable proxy](#scenario-1-exploiting-a-vulnerable-proxy)
    - [Scenario 2: Exploiting a vulnerable load balancer](#scenario-2-exploiting-a-vulnerable-load-balancer)
6. [Attack Techniques](#attack-techniques)
    - [Basic Exploit Techniques](#basic-exploit-techniques)
    - [Advanced Exploit Techniques](#advanced-exploit-techniques)
7. [Impact of HTTP Request Smuggling](#impact-of-http-request-smuggling)
8. [Detection and Mitigation](#detection-and-mitigation)
    - [Detecting HTTP Request Smuggling](#detecting-http-request-smuggling)
    - [Mitigating HTTP Request Smuggling](#mitigating-http-request-smuggling)
9. [Best Practices](#best-practices)
10. [Conclusion](#conclusion)

---

## Introduction to HTTP Request Smuggling

HTTP Request Smuggling is a technique used by attackers to exploit inconsistencies in how two or more HTTP servers (like a front-end proxy and a back-end web server) parse and handle HTTP requests. These inconsistencies allow an attacker to inject a fake request that will be processed by the back-end server, bypassing authentication or allowing for tampered requests.

HRS exploits the ambiguity in:
- The HTTP request line and headers.
- The ways different systems interpret `Content-Length` and `Transfer-Encoding`.

By crafting a carefully designed request, attackers can manipulate how the servers process requests, leading to potentially catastrophic outcomes.

---

## Basic Concepts

### HTTP Request Anatomy

An HTTP request is composed of:
- **Request Line**: Contains the method (GET, POST), the path, and the HTTP version (e.g., `GET /index.html HTTP/1.1`).
- **Headers**: Key-value pairs such as `Host`, `User-Agent`, `Content-Length`, etc.
- **Body**: (Optional) Present in methods like POST, where form data or other payloads are sent.

Here’s an example of a basic HTTP request:
```http
POST /login HTTP/1.1
Host: www.example.com
Content-Length: 27
Connection: keep-alive

username=admin&password=1234
```

### Chunked Transfer Encoding

Chunked Transfer Encoding is a method of data transmission where the data is sent in chunks. It’s useful for sending dynamically generated content without knowing the total size beforehand.

- Instead of using `Content-Length`, each chunk is prefixed with its size in hexadecimal:
```http
POST /upload HTTP/1.1
Host: www.example.com
Transfer-Encoding: chunked

5\r\n
hello\r\n
0\r\n
\r\n
```

### HTTP/1.1 vs HTTP/2

HRS is commonly found in HTTP/1.1 due to how requests are parsed, but with the introduction of HTTP/2, the likelihood of encountering HRS in that protocol has decreased. However, certain setups may still exhibit HRS in HTTP/2 environments.

### Role of Proxies and Load Balancers

Proxies and load balancers sit between the client and the server. They handle the distribution of traffic to back-end servers, often parsing HTTP requests and forwarding them. The key issue arises when the proxy and back-end server interpret requests differently. If the proxy forwards part of the request that was not intended for processing, it can lead to request smuggling.

---

## How HTTP Request Smuggling Works

The core idea of HTTP Request Smuggling is that front-end and back-end systems process request headers differently, allowing an attacker to craft a single request that is interpreted as two different requests by the front-end and back-end servers.

This desynchronization typically revolves around:
- The `Content-Length` header.
- The `Transfer-Encoding: chunked` header.

In a typical HTTP request smuggling attack:
1. The attacker sends a request with conflicting headers (e.g., both `Content-Length` and `Transfer-Encoding`).
2. The front-end server processes the request based on one header (e.g., `Transfer-Encoding`), while the back-end uses the other (e.g., `Content-Length`).
3. The back-end server inadvertently processes part of the attacker’s request as a new request, allowing malicious actions like request hijacking or cache poisoning.

---

## Types of HTTP Request Smuggling

### CL.TE (Content-Length vs Transfer-Encoding)
This is the most common type of request smuggling where the front-end uses the `Content-Length` header, while the back-end uses `Transfer-Encoding`. This discrepancy can allow an attacker to craft a request that looks benign to the proxy but is interpreted maliciously by the back-end server.

**Example of CL.TE Smuggling:**
```http
POST / HTTP/1.1
Host: example.com
Content-Length: 13
Transfer-Encoding: chunked

0

GET /admin HTTP/1.1
Host: example.com
```

The proxy sees the `Content-Length` of 13 and forwards the request body (empty in this case). The back-end, using `Transfer-Encoding: chunked`, will process the `GET /admin` as a new request.

### TE.CL (Transfer-Encoding vs Content-Length)
In TE.CL, the front-end honors the `Transfer-Encoding: chunked` header, but the back-end uses `Content-Length` to determine how much data to read.

**Example of TE.CL Smuggling:**
```http
POST / HTTP/1.1
Host: example.com
Transfer-Encoding: chunked
Content-Length: 6

0

G
```

Here, the back-end server processes the `G` as the start of a new request, leading to confusion or exploitation.

### CL.CL (Content-Length vs Content-Length)
In CL.CL smuggling, both servers use the `Content-Length` header, but the attacker leverages inconsistent handling of malformed or overlapping headers.

**Example of CL.CL Smuggling:**
```http
POST / HTTP/1.1
Host: example.com
Content-Length: 14
Content-Length: 6

username=admin
```

If the front-end uses the second `Content-Length` (6), and the back-end uses the first (14), a smuggling attack can occur by manipulating the body to include partial or additional malicious requests.

---

## Vulnerability Scenarios

### Scenario 1: Exploiting a Vulnerable Proxy

When a vulnerable proxy is between the attacker and the back-end server, attackers can inject extra HTTP requests to:
- Hijack legitimate user requests.
- Inject commands into the back-end server.

### Scenario 2: Exploiting a Vulnerable Load Balancer

If the load balancer misinterprets request headers, an attacker can poison the cache or hijack sessions, effectively redirecting requests intended for other users to their own controlled requests.

---

## Attack Techniques

### Basic Exploit Techniques
- **Injecting Additional Requests**: Crafting requests that look normal to the proxy but contain additional, malicious requests targeting the back-end server.
- **Session Hijacking**: Smuggling requests to steal session tokens or cookies from other users.

### Advanced Exploit Techniques
- **Cache Poisoning**: Injecting malicious responses into the cache via smuggled requests, allowing an attacker to serve malicious content to users.
- **Cross-Site Scripting (XSS)**: Leveraging request smuggling to inject JavaScript into server responses that get cached, leading to widespread XSS attacks.

---

## Impact of HTTP Request Smuggling

The consequences of a successful HTTP request smuggling attack include:
- **Security Bypass**: Access to restricted areas without proper authentication.
- **Session Hijacking**: Stealing cookies and sensitive information from other users.
- **Cache Poisoning**: Serving malicious content to users by poisoning the cache.
- **Cross-Site Scripting (XSS)**: Persistent injection of malicious scripts into a web application.

---

## Detection and Mitigation

### Detecting HTTP Request Smuggling
- **Manual Testing**: Tools like Burp Suite can be used to craft HTTP requests with conflicting headers.
- **Automated Scanners**: Web application scanners that can detect inconsistent header handling (

e.g., Content-Length/Transfer-Encoding inconsistencies).

### Mitigating HTTP Request Smuggling
- **Disable Unsupported Headers**: If `Transfer-Encoding: chunked` is not required, disable it entirely.
- **Input Validation**: Ensure that proxies and load balancers handle requests consistently with the back-end server.
- **Use Strict Parsers**: Configure the front-end and back-end servers to adhere to strict request parsing rules.

---

## Best Practices
- **Use HTTP/2 where possible**: HTTP/2 reduces the risk of HRS attacks due to its different request-handling mechanism.
- **Unified Parsing Logic**: Ensure all systems (proxies, load balancers, and back-end servers) follow consistent parsing rules.
- **Regular Security Audits**: Perform regular penetration testing focusing on HRS vulnerabilities.

---

## Conclusion

HTTP Request Smuggling is a highly impactful and often-overlooked vulnerability that can have devastating consequences. By understanding the intricacies of how different systems process HTTP requests and implementing strict parsing rules, the risk of HRS can be significantly mitigated. Always conduct thorough testing to detect and prevent this class of attacks.