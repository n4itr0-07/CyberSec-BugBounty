# 🚀 Fuzzing with FFUF – Ultimate Guide

Welcome to the **ultimate guide** on fuzzing using **FFUF**! Whether you're just starting out or looking to sharpen your skills, this guide will walk you through everything you need to know about fuzzing and mastering FFUF. Let's dive in! 🌊

---

## 📚 Table of Contents
- [What is Fuzzing?](#-what-is-fuzzing)
- [Fuzzing Tools](#-fuzzing-tools)
- [What is FFUF?](#-what-is-ffuf)
- [FFUF Cheat Sheet and Resources](#-ffuf-cheat-sheet-and-resources)
- [FFUF Tool – Command Reference](#-ffuf-tool--command-reference)
- [FFUF Command Examples](#-ffuf-command-examples)
- [Advanced Fuzzing Techniques](#-advanced-fuzzing-techniques)
- [Fuzzing for Vulnerabilities](#-fuzzing-for-specific-vulnerabilities)
- [Integrating FFUF with Other Tools](#-integrating-ffuf-with-other-tools)
- [Output Formats & Reporting](#-output-formats--reporting)
- [Handling Authentication](#-handling-authentication)
- [Dealing with Rate-Limiting](#-dealing-with-rate-limiting)
- [Common Issues and Troubleshooting](#-common-issues-and-troubleshooting)
- [Practical Workflow for Bug Bounty Hunters](#-practical-workflow-for-bug-bounty-hunters)
- [Pro Tips](#-pro-tips)
- [Additional Resources](#-additional-resources)

---

## 🌐 What is Fuzzing?

**Fuzzing** is an automated technique used to discover vulnerabilities, bugs, and edge cases in software or web applications. It works by feeding random or unexpected data into inputs to see how the application responds. This process can uncover security flaws and other issues that manual testing might miss.

### Types of Fuzzing
- **File format fuzzing**: Testing applications' file handling.
- **Web fuzzing**: Exploring web apps for hidden directories, parameters, and vulnerabilities like SQL injection or XSS.
- **Protocol fuzzing**: Checking for bugs in network protocols.

### Why Fuzzing is Important:
- Detect **0-day vulnerabilities** 💥
- Uncover **edge cases** developers may overlook.
- Strengthen the **security** of web applications 🔐

---

## 🛠️ Fuzzing Tools

Some of the most popular fuzzing tools include:

- **FFUF (Fuzz Faster U Fool)**: A fast, web-focused fuzzer.
- **Burp Suite Intruder**: A powerful tool for web app fuzzing.
- **AFL (American Fuzzy Lop)**: A tool for file format fuzzing.
- **WFuzz**: A tool for fuzzing GET/POST requests.
- **SecLists**: A collection of attack patterns, payloads, and fuzzing lists.

---

## 🔍 What is FFUF?

FFUF (**Fuzz Faster U Fool**) is a **fast web fuzzer** written in **Go**. It's designed to find hidden files, directories, parameters, and vulnerabilities in web applications.

### Why FFUF?
- 🌪️ **Speed**: FFUF is incredibly fast.
- 🧩 **Customizable**: You can fuzz GET/POST requests, headers, URLs, and more.
- 🚀 **Flexible**: Supports different input methods and formats.

---

## 📚 FFUF Cheat Sheet and Resources

Here are some must-know resources to boost your fuzzing skills:

- [FFUF Cheat Sheet by HackTricks](https://book.hacktricks.xyz/pentesting/pentesting-web/ffuf-fuzz-fast-you-fool)
- [Fuzzing SecLists](https://github.com/danielmiessler/SecLists)
- [OWASP Fuzzing Guide](https://owasp.org/www-community/Fuzzing)
- [PortSwigger Fuzzing Guide](https://portswigger.net/web-security/fuzzing)

---

## 💻 FFUF Tool – Command Reference

FFUF comes with a variety of options to customize your fuzzing experience. Here's a quick reference guide:

| Command/Option   | Description                                                                                       |
| ---------------- | ------------------------------------------------------------------------------------------------- |
| `-u`             | URL of the target, with `FUZZ` keyword marking where fuzzing occurs.                               |
| `-w`             | Wordlist for fuzzing (can include multiple wordlists).                                             |
| `-X`             | HTTP method (GET, POST, PUT, DELETE, etc.).                                                       |
| `-d`             | POST data (for POST requests).                                                                    |
| `-H`             | Add headers to the request.                                                                       |
| `-t`             | Number of threads (concurrent requests).                                                          |
| `-r`             | Follow redirects automatically.                                                                   |
| `-x`             | Proxy support (send requests through a proxy).                                                    |
| `-fs`            | Filter responses by size (exclude specific sizes).                                                |
| `-fc`            | Filter responses by HTTP response codes (exclude specific status codes).                           |
| `-mc`            | Match specific HTTP response codes (only include specific status codes).                           |
| `-s`             | Silent mode (minimal output).                                                                     |
| `-o`             | Output results to a file.                                                                         |
| `-ac`            | Auto-calibration to reduce noise based on response patterns.                                       |
| `-e`             | Extensions to append to the fuzzing wordlist (e.g., `.php`, `.txt`).                               |

---

## 🚀 FFUF Command Examples

### 1. 🗂️ Directory Fuzzing
Discover hidden directories:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist/directory-list.txt
```

### 2. 🔐 Fuzzing POST Data
Fuzz a POST request's `username` field:

```bash
ffuf -u https://target.com/login -X POST -d 'username=FUZZ&password=pass123' -w /path/to/wordlist.txt
```

### 3. 🔎 Fuzzing with Custom Headers
Test with custom headers:

```bash
ffuf -u https://target.com/admin -H "Authorization: Bearer FUZZ" -w /path/to/wordlist.txt
```

### 4. 📂 Fuzzing File Extensions
Try fuzzing for different file extensions:

```bash
ffuf -u https://target.com/indexFUZZ -w /path/to/wordlist.txt -e .php,.html,.txt
```

### 5. 📊 Filtering HTTP Responses
Filter out 404 responses and small response sizes:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -fc 404 -fs 100
```

### 6. 💥 Fuzzing with Proxy Support
Send fuzzing traffic through Burp Suite:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -x http://127.0.0.1:8080
```

---

## 🔍 Advanced Fuzzing Techniques

### Recursive Fuzzing
Use FFUF to fuzz deeper directories:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -recursion
```

### Fuzzing APIs and JSON
Test API endpoints with fuzzing:

```bash
ffuf -u https://api.target.com/users/1/FUZZ -w /path/to/wordlist.txt
```

---

## 🔐 Fuzzing for Specific Vulnerabilities

### SQL Injection Fuzzing Example:
Use FFUF to fuzz for SQL injection vulnerabilities:

```bash
ffuf -u https://target.com/login -X POST -d 'username=FUZZ' -w /path/to/sqli_payloads.txt
```

---

## 🔗 Integrating FFUF with Other Tools

### FFUF + Burp Suite
Proxy FFUF traffic through Burp for deeper analysis:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -x http://127.0.0.1:8080
```

### FFUF + masscan/nmap
Use masscan or nmap to find open ports and then fuzz with FFUF.

---

## 📂 Output Formats & Reporting

You can export the FFUF results in different formats, such as JSON or CSV.

### Save Output as JSON
```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -o output.json -of json
```

---

## 🔑 Handling Authentication

### Token-Based Authentication Example:
```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -H "Authorization: Bearer your_token"
```

### Basic Authentication Example:
```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -H "Authorization: Basic dXNlcjpwYXNz"
```

---

## 🚧 Dealing with Rate-Limiting

### Throttle Requests
Limit the request rate to avoid getting blocked:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -rate 50
```

### Rotate User-Agents
Change the User-Agent header with each

 request:

```bash
ffuf -u https://target.com/FUZZ -H "User-Agent: FUZZ" -w /path/to/user-agents.txt
```

---

## 🚨 Common Issues and Troubleshooting

### SSL Errors
If you encounter SSL certificate errors, try adding:

```bash
-k
```

### Handling Timeouts
Increase the timeout if FFUF is too fast for the server:

```bash
-Timeout 5
```

---

## 🎯 Practical Workflow for Bug Bounty Hunters

1. **Recon**: Use tools like `masscan` or `nmap` to discover open ports and services.
2. **Directory Fuzzing**: Use FFUF to find hidden directories and files.
3. **Parameter Fuzzing**: Explore web forms and parameters with FFUF for hidden inputs.
4. **Vulnerability-Specific Fuzzing**: Test for vulnerabilities like SQLi, XSS, and more.

---

## 🎯 Pro Tips

1. **Use multiple wordlists** for better coverage.
2. **Filter responses** by HTTP status codes and response size.
3. **Optimize concurrency** by adjusting the thread count (`-t`) to match server speed.
4. **Fuzz Parameters**: Don't limit yourself to URLs, fuzz headers, POST data, and parameters.
5. **Auto-calibration**: Use `-ac` to reduce false positives.

---

## 📦 Wordlists

- [SecLists by Daniel Miessler](https://github.com/danielmiessler/SecLists)
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)
- [DirBuster Wordlist](https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)

---

## 🔗 Additional Resources

- [Comprehensive Fuzzing Guide by OWASP](https://owasp.org/www-community/Fuzzing)
- [FFUF Cheat Sheet by HackTricks](https://book.hacktricks.xyz/pentesting/pentesting-web/ffuf-fuzz-fast-you-fool)
- [Fuzz Faster U Fool (FFUF) in Bug Bounties (Video)](https://www.youtube.com/watch?v=Qx8vXYPgqh4)
- [Automating FFUF with Burp Suite (Video)](https://www.youtube.com/watch?v=5nxG0o2ZORs)

---

## 🤖 Conclusion

Fuzzing is an essential skill for finding hidden vulnerabilities in web applications. **FFUF** is an incredibly powerful tool to assist you in this task. Armed with the right wordlists and the examples from this guide, you're ready to explore and secure web applications more effectively!

Happy fuzzing! 🐞🔍

---