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
- [FFUF Command Options Explained](#-ffuf-command-options-explained)
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

| Command/Option     | Description                                                                                       |
| ------------------ | ------------------------------------------------------------------------------------------------- |
| `-u`               | URL of the target, with `FUZZ` keyword marking where fuzzing occurs.                               |
| `-w`               | Wordlist for fuzzing. Can specify multiple wordlists with commas or multiple `-w` options.         |
| `-X`               | Specify the HTTP method (GET, POST, PUT, DELETE, etc.).                                            |
| `-d`               | POST data to be sent in requests (for POST requests).                                              |
| `-H`               | Add custom headers to the request. Multiple headers can be added by using multiple `-H` options.   |
| `-t`               | Number of concurrent threads (concurrent requests).                                                |
| `-r`               | Automatically follow redirects.                                                                   |
| `-x`               | Proxy support: send requests through a specified proxy (e.g., Burp Suite).                         |
| `-fs`              | Filter responses by size (exclude specific sizes).                                                 |
| `-fc`              | Filter responses by HTTP status codes (exclude specific status codes).                             |
| `-mc`              | Match specific HTTP status codes (only include specific status codes).                             |
| `-s`               | Silent mode (minimal output).                                                                     |
| `-o`               | Output results to a file.                                                                         |
| `-of`              | Output file format (`json`, `html`, `csv`, `md`).                                                  |
| `-recursion`       | Enables recursive fuzzing (fuzz deeper into the discovered directories).                           |
| `-recursion-depth` | Set recursion depth. Defines how many levels deep to recurse during fuzzing.                       |
| `-e`               | Extensions to append to the fuzzing wordlist (e.g., `.php`, `.txt`, `.html`).                      |
| `-ac`              | Auto-calibration mode: automatically reduces noise by calibrating against baseline responses.      |
| `-rate`            | Set the number of requests per second (to avoid rate limiting).                                    |
| `-timeout`         | Set a timeout value (in seconds) for each request.                                                 |
| `-input-cmd`       | Use an external command to provide input for fuzzing (stdin).                                      |
| `-input-num`       | Number of entries to process from the input.                                                       |
| `-input-shell`     | Use a shell command as the input generator for fuzzing.                                             |
| `-v`               | Verbose mode: show additional information during execution.                                        |
| `-p`               | Delay in seconds between each request to avoid rate limiting or detection.                         |
| `-replay-proxy`    | Proxy through which to replay requests that triggered interesting results.                         |
| `-ignore-body`     | Ignore the response body in the results output.                                                    |
| `-noninteractive`  | Disable the interactive progress bar and use a cleaner output format (for scripts).                |
| `-debug-log`       | Write a debug log to a specified file for troubleshooting.                                         |
| `-auth`            | Use HTTP Basic Authentication (format: username:password).                                         |

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
ffuf -u https://target.com/login -X POST -d 'username=FUZZ&password=password' -w /path/to/wordlist.txt
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

## 🔍 FFUF Command Options Explained

### 1. `-u` (URL)

**Description**: The target URL where you want to fuzz. The keyword `FUZZ` in the URL tells FFUF where to insert the fuzzed data.

**Example**:

```bash
ffuf

 -u https://target.com/FUZZ -w /path/to/wordlist.txt
```

### 2. `-w` (Wordlist)

**Description**: The path to the wordlist you want to use for fuzzing. You can provide multiple wordlists by separating them with commas or using multiple `-w` flags.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist1.txt,/path/to/wordlist2.txt
```

### 3. `-X` (HTTP Method)

**Description**: Specifies the HTTP method to use (GET, POST, PUT, DELETE, etc.).

**Example**:

```bash
ffuf -u https://target.com/login -X POST -d 'username=FUZZ&password=password' -w /path/to/wordlist.txt
```

### 4. `-d` (POST Data)

**Description**: Data to send in the body of the request. This is typically used in POST requests.

**Example**:

```bash
ffuf -u https://target.com/login -X POST -d 'username=FUZZ&password=pass123' -w /path/to/wordlist.txt
```

### 5. `-H` (Custom Headers)

**Description**: Add custom headers to the request. You can add multiple headers by repeating the `-H` option.

**Example**:

```bash
ffuf -u https://target.com/admin -H "Authorization: Bearer FUZZ" -w /path/to/wordlist.txt
```

### 6. `-t` (Number of Threads)

**Description**: Specifies the number of concurrent requests (threads). More threads = faster fuzzing, but it may increase the chance of detection or getting blocked.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -t 50
```

### 7. `-r` (Follow Redirects)

**Description**: Automatically follows redirects when fuzzing.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -r
```

### 8. `-x` (Proxy)

**Description**: Use a proxy to send requests through (e.g., Burp Suite or ZAP).

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -x http://127.0.0.1:8080
```

### 9. `-fs` (Filter by Size)

**Description**: Exclude responses that match the specified size in bytes.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -fs 100
```

### 10. `-fc` (Filter by Status Code)

**Description**: Exclude responses that return specific HTTP status codes.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -fc 404
```

### 11. `-mc` (Match by Status Code)

**Description**: Only include responses that return specific HTTP status codes.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -mc 200
```

### 12. `-s` (Silent Mode)

**Description**: Minimizes the output to only show results, useful when fuzzing in a non-interactive mode or scripting.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -s
```

### 13. `-o` and `-of` (Output and Format)

**Description**: Save the fuzzing results to a file. You can specify the format with `-of`, including JSON, CSV, HTML, and Markdown (md).

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -o results.json -of json
```

### 14. `-recursion` and `-recursion-depth`

**Description**: Enables recursive fuzzing (FFUF will automatically fuzz directories found) and sets the recursion depth.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -recursion -recursion-depth 2
```

### 15. `-e` (File Extensions)

**Description**: Append extensions to the fuzzed wordlist (e.g., `.php`, `.html`, `.txt`).

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -e .php,.txt
```

### 16. `-ac` (Auto-Calibration)

**Description**: Automatically adjusts based on baseline responses to reduce noise and false positives.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -ac
```

### 17. `-rate` (Rate Limiting)

**Description**: Set the number of requests per second to avoid getting blocked by rate-limiting mechanisms.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -rate 100
```

### 18. `-timeout` (Request Timeout)

**Description**: Set a timeout (in seconds) for each request.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -timeout 5
```

### 19. `-input-cmd` (Input via Command)

**Description**: Use an external command to generate input for fuzzing, e.g., from `stdin`.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -input-cmd "cat wordlist.txt"
```

### 20. `-v` (Verbose Mode)

**Description**: Enables verbose mode, showing additional information about the fuzzing process.

**Example**:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -v
```

---

## 🔍 Advanced Fuzzing Techniques

### Recursive Fuzzing
Use FFUF to fuzz deeper directories:

```bash
ffuf -u https://target.com/FUZZ -w /path/to/wordlist.txt -recursion -recursion-depth 2
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
Change the User-Agent header with each request:

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
4. **Vulnerability-Specific Fuzzing**: Test for

 vulnerabilities like SQLi, XSS, and more.

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