# Application Security (AppSec) & Secure Coding

The vast majority of cyberattacks today target the application layer (Layer 7). Whether it's a web application, a mobile app, or a backend API, attackers focus on exploiting flaws in the logic or code written by developers. Application Security (AppSec) is the practice of finding, fixing, and preventing security vulnerabilities at the application level.

## 1. Common Web Vulnerabilities (OWASP Top 10)

The Open Worldwide Application Security Project (OWASP) Top 10 is a widely recognized awareness document that represents a broad consensus on the most critical security risks to web applications.

While the list is updated periodically, the core vulnerability classes remain constant:
*   **A01: Broken Access Control:** Users acting outside of their intended permissions. (e.g., User A modifying the URL from `account=1` to `account=2` and viewing User B's details - Insecure Direct Object Reference or IDOR).
*   **A02: Cryptographic Failures:** (Previously Sensitive Data Exposure) Failing to protect data in transit (using old TLS) or at rest (storing passwords in plain text or using weak hashing like MD5).
*   **A03: Injection:** Untrusted data is sent to an interpreter as part of a command or query.
    *   *SQL Injection (SQLi):* Modifying a database query to dump data, bypass authentication, or drop tables.
    *   *Cross-Site Scripting (XSS):* Injecting malicious JavaScript into a web page viewed by other users to steal session cookies or redirect them.
    *   *Command Injection:* Executing arbitrary OS commands via the application.
*   **A04: Insecure Design:** Flaws in architectural design. A perfectly coded application can still be vulnerable if the fundamental design lacks security controls (e.g., not requiring MFA for administrative actions).
*   **A05: Security Misconfiguration:** Insecure default settings, incomplete configurations, open cloud storage, misconfigured HTTP headers, and verbose error messages containing stack traces.
*   **A06: Vulnerable and Outdated Components:** Using third-party libraries (npm, PyPI) that have documented vulnerabilities (CVEs). This was the root cause of the infamous Equifax breach (Apache Struts).
*   **A07: Identification and Authentication Failures:** Permitting automated brute-force attacks, permitting weak passwords, or having flawed session timeout mechanisms.
*   **A08: Software and Data Integrity Failures:** Making assumptions related to software updates, critical data, and CI/CD pipelines without verifying integrity (e.g., an automated update mechanism fetching a malicious update without verifying a digital signature - like SolarWinds).
*   **A09: Security Logging and Monitoring Failures:** Failing to log critical events (logins, failed logins, high-value transactions) hinders or entirely prevents incident response.
*   **A10: Server-Side Request Forgery (SSRF):** A web application fetching a remote resource without validating the user-supplied URL. An attacker can force the application to read internal resources (like cloud metadata APIs - e.g., the Capital One breach).

## 2. Static and Dynamic Analysis (SAST/DAST)

You cannot manually review every line of code in massive applications. We use automated tools to scale security testing.

*   **SAST (Static Application Security Testing):** "White-box" testing. SAST tools analyze the raw source code or bytecode *without executing it*. 
    *   *Pros:* Finds issues early in the development lifecycle (developers get instant feedback in their IDEs), pinpoints the exact line of vulnerable code.
    *   *Cons:* Cannot find runtime vulnerabilities, high rate of false positives.
*   **DAST (Dynamic Application Security Testing):** "Black-box" testing. DAST tools interact with the running application from the outside, injecting payloads (like SQLi or XSS) into input fields and observing the response.
    *   *Pros:* Identifies actual exploitable vulnerabilities, independent of the programming language used.
    *   *Cons:* Found later in the development cycle (requires a compiled/running app), harder to pinpoint the exact line of code causing the issue.
*   **SCA (Software Composition Analysis):** Tools dedicated specifically to scanning third-party open-source libraries (the `package.json` or `requirements.txt`) against databases of known CVEs.

## 3. Secure Coding Practices

Developers are the first line of defense. Core secure coding practices include:
*   **Input Validation:** Assume all input is malicious. Validate data against a strict allow-list of expected characters, type, and length.
*   **Output Encoding:** If you must display user input back to the browser, encode it appropriately for the context (HTML, JavaScript, CSS) to prevent execution (XSS).
*   **Parameterized Queries (Prepared Statements):** The *only* robust defense against SQL Injection. It forces the database to treat input as data, never as an executable query.
*   **Defense in Depth:** Implementing security at multiple layers (e.g., input validation on the client-side *and* the server-side).
*   **Fail Securely:** When an application crashes or throws an exception, it should default to denying access and should never reveal internal system details to the user.

## 4. Integrating Security into the SDLC (DevSecOps)

Historically, security was a discrete phase at the very end of the Software Development Life Cycle (SDLC), acting as a "gatekeeper" and causing massive delays.

**DevSecOps** is the integration of security practices within the DevOps process.
*   **Shift Left:** Moving security testing as early in the SDLC as possible. Fixing a vulnerability during the coding phase is orders of magnitude cheaper than fixing it in production.
*   **Automation in the CI/CD Pipeline:**
    *   *Commit:* A developer commits code; an IDE plugin runs local linting for security flaws.
    *   *Build:* The CI server (like Jenkins or GitHub Actions) automatically runs SCA (checking libraries) and SAST scans. If critical vulnerabilities are found, the build *fails*.
    *   *Test/Staging:* The application is deployed to a staging environment, and automated DAST scanners attack it.
    *   *Production:* Real-time protection with Web Application Firewalls (WAF) and Runtime Application Self-Protection (RASP).


## References & Further Learning

**HackerRepo (GitHub)**
*   [Exploit Development](https://github.com/The-Art-of-Hacking/h4cker/tree/master/exploit-development)

**Hacker Training**
*   [AI-Enabled Programming, Networking, and Cybersecurity (Video Course)](https://learning.oreilly.com/course/ai-enabled-programming-networking/9780135402696/)
*   [WebSploit Labs](https://websploit.org/)
