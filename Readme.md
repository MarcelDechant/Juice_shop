# OWASP Juice Shop Challenges

In this repository I am gradually making **my solutions to the OWASP Juice Shop challenges** available and presenting the security vulnerabilities behind them.  
  
The content is created as part of my training at the **Developer Akademie** and is used exclusively for teaching purposes.  

## Table of Contents

1. [Introducing the OWASP Juice Shop](#introducing-the-owasp-juice-shop)
   * [What is the OWASP Juice Shop?](#what-is-the-owasp-juice-shop)
   * [What are the OWASP Top Ten?](#what-are-the-owasp-top-ten)
2. [What vulnerabilities lurk in web applications?](#what-vulnerabilities-lurk-in-web-applications)
   * [Improper Input Validation](#1-improper-input-validation)
   * [Broken Authentication](#2-broken-authentication)
   * [XSS - Cross-Site Scripting](#3-xss---cross-site-scripting)
3. [List of solved challenges so far](#list-of-solved-challenges-so-far)

## Introducing the OWASP Juice Shop

### What is the OWASP Juice Shop?

The OWASP Juice Shop is not a juice shop and you can not buy juice or anything else there. But it keeps the promise of being a really bad online shop. So bad that you can even learn something - about **Web Application Security Risks**.

> [!NOTE] 
> OWASP Juice Shop is probably the most modern and sophisticated insecure web application! It can be used in security trainings, awareness demos, CTFs and as a guinea pig for security tools! Juice Shop encompasses vulnerabilities from the entire OWASP Top Ten along with many other security flaws found in real-world applications!
[More Information](https://owasp.org/www-project-juice-shop/)

Do you want to solve the challenges yourself? [More Information](https://github.com/juice-shop/juice-shop)

### What are the OWASP Top Ten?

The OWASP Top Ten is a list of the most common and critical web application security risks. It is created and regularly updated by the Open Web Application Security Project (OWASP) community. The list serves as a guide for developers, security analysts and companies to improve the security of their applications. 

> [!NOTE]
> Companies should adopt this document and start the process of ensuring that their web applications minimize these risks. Using the OWASP Top 10 is perhaps the most effective first step towards changing the software development culture within your organization into one that produces more secure code.
[More Information](https://owasp.org/www-project-top-ten/)


### <ins>1) Improper Input Validation</ins>

**Improper Input Validation** is a security vulnerability that occurs when a system does not adequately or correctly validate user inputs before processing them. The lack of proper validation can lead to errors, unexpected behavior, or exploitation by malicious actors. By implementing robust input validation, many attack vectors can be mitigated early, as malicious inputs will be identified and blocked before they reach sensitive parts of the system.
  
### Potential Impacts

1. **Injection Attacks**:
   * <ins>SQL Injection</ins>: Inserting malicious SQL commands.
   * <ins>Command Injection</ins>: Executing system commands.
   * <ins>Privilege Escalation</ins>: Using crafted input to assign higher privileges (e.g. admin rights).

1. **Cross-Site Scripting (XSS)**:
   * Injecting malicious JavaScript into web applications.

1. **Buffer Overflow**:
   * Exploiting memory limits by exceeding allocated buffer sizes.

1. **Path Traversal**:
   * Accessing unauthorized files by manipulating file paths.
 
1. **Denial of Service (DoS)**:
   * Overloading or crashing a system with large or malicious inputs.

### Examples of Improper Input Validation

* <ins>Missing Length Checks</ins>: Allowing excessively long inputs that can cause buffer overflows.
* <ins>Unfiltered Special Characters</ins>: Accepting characters like ', ", <, and > that can be exploited for injections or XSS.
* <ins>Direct Use of User Input</ins>: Passing input directly to databases, files, or APIs without validation.

### Mitigation and Prevention

1. <ins>Whitelist Validation</ins>: 
   * Only allow specific, expected input values.

2. <ins>Escape and Sanitize Input</ins>:
   * Use escaping for SQL, HTML, XML, etc.

3. <ins>Limit Input Size</ins>:
   * Define maximum length and valid ranges for input data.

4. <ins>Use Secure APIs</ins>:
   * Use prepared statements for database interactions.

5. <ins>Regular Security Testing</ins>:
   * Conduct code reviews and penetration testing to identify vulnerabilities.

6. <ins>Utilize Secure Frameworks</ins>:
   * Modern frameworks often include built-in mechanisms to prevent improper input handling.

### <ins>2) Broken Authentication</ins>

**Broken Authentication** is a security vulnerability where an application’s authentication mechanisms are poorly implemented or configured, allowing attackers to take over user accounts or access protected resources. This vulnerability is listed in the OWASP Top 10 and represents a serious threat to web applications.  
A successful attack on authentication mechanisms can grant attackers full access to user accounts and their sensitive data. In the worst-case scenario, an attacker could gain administrative privileges and compromise the entire application.

### Causes of Broken Authentication

1. <ins>Weak Password Implementation</ins>:
   * Allowing weak or easily guessable passwords.
   * No enforcement of password complexity or length requirements.

2. <ins>Lack of Protection Against Brute-Force or Credential Stuffing Attacks</ins>:
   * No limit on login attempts.
   * No delay for repeated failed login attempts.
   * Allowing the reuse of passwords from compromised databases.

3. <ins>Insecure Password Storage</ins>:
   * Storing passwords in plaintext.
   * Using weak hashing algorithms like MD5 or SHA-1.

4. <ins>Session Management Weaknesses</ins>:
   * Session IDs are not invalidated after logout or timeout.
   * Session IDs are predictable or easy to guess.
   * No protection against session hijacking (e.g., missing Secure or HttpOnly flags on cookies).

5. <ins>Insecure Password Recovery Mechanisms</ins>:
   * **Easily guessable security questions or their answers**.
   * Password reset links with no expiration or insufficient security measures.

### Possible Attacks

1. <ins>Credential Stuffing</ins>:
   * Attackers use a list of usernames and passwords from data breaches to log into an application.

2. <ins>Brute-Force Attacks</ins>:
   * Attackers systematically try different passwords until the correct one is found.

3. <ins>Session Hijacking</ins>:
   * Attackers steal an active session ID to gain access to a victim’s account.

4. <ins>Man-in-the-Middle Attacks</ins>:
   * Credentials are transmitted insecurely over unencrypted channels (e.g., HTTP instead of HTTPS).

5. <ins>Password Reset Manipulation</ins>:
   * Attackers guess security questions or manipulate password reset mechanisms.

### Preventive Measures Against Broken Authentication

1. <ins>Enforce Strong Password Policies</ins>:
   * Require password complexity and a minimum length.
   * Enable multi-factor authentication (MFA).

2. <ins>Limit Login Attempts</ins>:
   * Lock accounts after several failed attempts.
   * Introduce delays for repeated requests (rate-limiting).

3. <ins>Secure Password Storage</ins>:
   * Hash passwords using strong algorithms such as bcrypt, Argon2, or PBKDF2.
   * Add salts to prevent rainbow table attacks.

4. <ins>Secure Session Management</ins>:
   * Invalidate session IDs after logout or timeout.
   * Set cookies with Secure, HttpOnly, and SameSite flags.

5. <ins>Defend Against Credential Stuffing</ins>:
   * Check passwords against known breach databases (e.g., using the Have I Been Pwned API).
   * Use captchas or additional authentication steps.

6. <ins>Monitoring and Logging</ins>:
   * Detect and respond to unusual login patterns (e.g., multiple failed login attempts).

7. <ins>Regular Security Testing</ins>:
   * Conduct penetration tests to identify and fix vulnerabilities.

### <ins>3) XSS - Cross-Site Scripting</ins>

**XSS (Cross-Site Scripting)** is a common security vulnerability in web applications that allows attackers to inject malicious code (often JavaScript) into web pages viewed by other users. This vulnerability arises due to inadequate validation or sanitization of user input.

### How XSS Works: Source and Sink

* <ins>Source</ins>: The entry point for untrusted data. This can include URL parameters, form fields, HTTP headers, cookies, or any user-provided input.
* <ins>Sink</ins>: The execution point where the untrusted data is improperly handled or rendered. Examples include inserting data directly into the DOM, using eval(), or rendering it in an HTML context.

### Types of XSS

1. <ins>Reflected XSS (Non-Persistent)</ins>:
   * The malicious code originates from the Source (e.g., user input or query parameters) and is immediately reflected in the server's response without being stored.
     * **Example**: A search field that displays the entered query without filtering it before rendering in the HTML.

1. <ins>Stored XSS (Persistent)</ins>:
   * The malicious code is stored on the server (e.g., in a database) and delivered to users every time they view the affected page. Here, the Source is the attacker's input, and the Sink is where the code is rendered for users.
     * **Example**: A forum post where an attacker embeds a script tag that executes when others view the post.

1. <ins>DOM-Based XSS</ins>:
   * This type of XSS occurs entirely in the client-side browser. The attack manipulates the Source (e.g., URL parameters or client-side variables) and leverages a vulnerable Sink (e.g., dynamically updating the DOM) to execute malicious code.
     * **Example**: A JavaScript function that takes unvalidated user input from the URL and directly injects it into the DOM.

### Risks of XSS

* <ins>Session Cookie Theft</ins>: Attackers can steal cookies to impersonate the victim.
* <ins>Content Manipulation</ins>: Attackers can alter web page content or redirect users to phishing pages.
* <ins>Execution of Malicious Actions</ins>: Attackers can perform actions on behalf of the victim, such as submitting forms or making unauthorized requests.
* <ins>Malware Distribution</ins>: XSS can be used to spread malware by injecting malicious scripts.

### Mitigating XSS

1. <ins>Input Validation and Sanitization</ins>:
   * Validate user input at the Source and sanitize it to remove malicious content.
   * Use escaping and encoding (e.g., convert < to &lt;) before rendering data in the Sink.

2. <ins>Content Security Policy (CSP)</ins>:
   * Implement a CSP to restrict the execution of unauthorized scripts or loading of untrusted resources.

3. <ins>Contextual Output Encoding</ins>:
   * Use encoding mechanisms appropriate for the Sink (e.g., HTML encoding for HTML contexts, JavaScript escaping for JavaScript contexts).

4. <ins>Security Libraries</ins>:
   * Use libraries such as OWASP’s ESAPI or built-in framework functions to handle data safely between Source and Sink.

5. <ins>Cookie Security</ins>:
   * Ensure cookies are set with HttpOnly and Secure flags to reduce the impact of XSS.

6. <ins>Regular Security Testing</ins>:
   * Conduct automated and manual penetration tests to identify vulnerabilities in the flow from Source to Sink.


## List of solved challenges so far

### <ins>Three-Star-Challenges</ins>

| Name | Category | Description | Link |
| ---- | ------- | ----------- | -------- |
| Admin Registration | Improper Input Validation | Register as a user with administrator privileges. | [Admin Registration](./admin_registration) |
| Björn's Favorite Pet | Broken Authentication | Reset the password of Bjoern's OWASP account via the Forgot Password mechanism with the original answer to his security question. | [Björn's Favorite Pet](./bjoern's_favorite_pet) |
| CAPTCHA Bypass  | Broken Anti Automation | Submit 10 or more customer feedback messages within 20 seconds to simulate bypassing a CAPTCHA mechanism. | [CAPTCHA Bypass](./Captcha_bypass) |
