# Lab: [Insert Exact PortSwigger Lab Name]

## 1. Objective
[Briefly describe the goal of the lab. E.g., Exploit the SQL injection vulnerability to log in as the administrator.]

## 2. Vulnerability Overview
* **Vulnerability Class:** [e.g., SQL Injection, Cross-Site Scripting, BOLA]
* **Mechanism:** [Briefly explain how the vulnerability works conceptually.]

## 3. The Exploit (Burp Suite Execution)
**Methodology:**
1. Intercepted the target request in Burp Proxy.
2. Sent the request to Repeater to test payload variations.
3. [Insert specific action, e.g., Injected a UNION SELECT payload into the category parameter].

**Malicious HTTP Request Payload:**
```http
[Paste the raw HTTP request from Burp Suite here. Example below:]
GET /filter?category=Gifts'+UNION+SELECT+username,+password+FROM+users-- HTTP/1.1
Host: vulnerable-website.com

## 4. Root Cause Analysis
[Explain the underlying flaw in the backend logic. E.g., The application takes the user's input from the `category` parameter and directly concatenates it into the backend SQL string without sanitization. This allows the attacker's payload to break out of the data context and alter the structure of the database query.]

## 5. Secure Code Remediation
[Provide the specific engineering solution required to patch the flaw, including a secure code snippet to guide the developers.]

**Remediation Strategy:**
* [E.g., Replace the vulnerable string concatenation with Parameterized Queries (Prepared Statements). This ensures the database treats the input strictly as literal data, not executable code.]

**Secure Code Example (Java):**
```java
PreparedStatement pstmt = connection.prepareStatement("SELECT * FROM products WHERE category = ?");
pstmt.setString(1, categoryInput);
