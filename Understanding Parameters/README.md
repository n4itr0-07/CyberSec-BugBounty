# Understanding Parameters in Bug Bounty

## What are Parameters?

**Parameters** in the context of web applications and APIs are key-value pairs used to pass data between the client (usually the browser or a script) and the server. They play a crucial role in defining the behavior of a request and how data is processed on the server side.

Parameters can be found in various parts of an HTTP request, such as the URL, request body, headers, and more. They are often the primary target for manipulation in security testing because improperly handled parameters can lead to various security vulnerabilities.

## Types of Parameters

### 1. URL Query Parameters
- **Description**: These parameters are appended to the URL after a `?` and separated by `&`.
- **Example**:
  ```http
  https://example.com/search?query=bug+bounty&sort=asc
  ```
  - `query` and `sort` are parameters, with values `bug bounty` and `asc`, respectively.

### 2. Path Parameters
- **Description**: Variables embedded directly within the URL path, often used for routing.
- **Example**:
  ```http
  https://example.com/users/12345
  ```
  - `12345` is a parameter representing a user ID.

### 3. Form Data Parameters
- **Description**: Parameters sent through HTTP POST requests, typically within form submissions.
- **Example**:
  ```http
  POST /login HTTP/1.1
  Host: example.com
  Content-Type: application/x-www-form-urlencoded
  
  username=admin&password=password123
  ```
  - `username` and `password` are parameters in the request body.

### 4. Headers
- **Description**: HTTP headers can also contain parameters that affect the request or response.
- **Example**:
  ```http
  GET /api/resource HTTP/1.1
  Host: example.com
  Authorization: Bearer <token>
  ```
  - The `Authorization` header contains a parameter with an authentication token.

### 5. JSON/XML Payloads
- **Description**: Parameters embedded in JSON or XML payloads sent with HTTP requests.
- **Example**:
  ```json
  {
    "user_id": "12345",
    "action": "delete"
  }
  ```
  - `user_id` and `action` are parameters within the JSON payload.

## Relevance of Parameters in Bug Bounties

### Injection Attacks
Parameters are often the entry points for injection attacks, such as:

- **SQL Injection**:
  - Vulnerable Query:
    ```sql
    SELECT * FROM users WHERE id = '12345';
    ```
  - Malicious Input:
    ```sql
    12345'; DROP TABLE users; --
    ```

- **Cross-Site Scripting (XSS)**:
  - Vulnerable HTML:
    ```html
    <input type="text" name="search" value="bug bounty">
    ```
  - Malicious Input:
    ```html
    <script>alert('XSS')</script>
    ```

### Authentication Bypass
- **Example**: Manipulating parameters related to user roles or permissions could lead to unauthorized access to sensitive areas of an application.

### Business Logic Flaws
- **Example**: Parameters controlling purchase quantities, discount codes, or other business logic can be exploited to gain unintended benefits.

## Examples of Vulnerable Parameters

### Insecure Direct Object Reference (IDOR)
- **Description**: By altering a parameter representing an object ID, an attacker might access data belonging to another user.
- **Example**:
  ```http
  GET /api/orders/12345 HTTP/1.1
  Host: example.com
  ```
  - Changing `12345` to another valid ID could allow access to someone else's order.

### Cross-Site Request Forgery (CSRF)
- **Description**: Parameters can be crafted in CSRF attacks to perform unintended actions on behalf of authenticated users.

## Tools for Testing Parameters

- **Burp Suite**: A comprehensive tool for capturing, analyzing, and manipulating HTTP requests, including parameters.
- **OWASP ZAP**: An open-source tool for intercepting and analyzing web traffic.
- **Param Miner**: A Burp Suite extension that helps discover hidden or undocumented parameters.

## Tips for Bug Hunters

- **Parameter Fuzzing**: Test how the application responds to unexpected, malformed, or edge-case parameter values.
- **Check All Parameter Locations**: Examine parameters in URLs, headers, bodies, and even cookies.
- **Explore Hidden Parameters**: Use tools or brute-forcing techniques to discover parameters not explicitly documented or visible.

## Conclusion

Understanding parameters is critical in bug bounty hunting. They are often the weakest link in the chain of web application security. By knowing where to look and how to manipulate parameters, you can uncover vulnerabilities that might otherwise go unnoticed.
