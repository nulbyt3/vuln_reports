```
Reported by: Mikail Kakabayev (nulbyt3)
Date: 2025/29/07

 ---------- Details ----------
Lab: DVWA (Damn Vulnerable Web Application)
Vulnerability: Reflected Cross-Site Scripting (XSS)
Security Level: High
Endpoint: http://localhost/dvwa/vulnerabilities/xss_r/?name=
```

## <span style='color: red'>Vulnerable:</span> Reflected Cross-Site Scripting (XSS) with BLACKLISTING bypass

### Description:
A reflected Cross-Site Scripting (XSS) vulnerability exists in the DVWA application's "XSS Reflected" module. The blacklisting functionality does not properly validate the name parameter in the search bar. Causing arbitrary JavaScript execution.

### Impact:
An attacker could:
- Steal user sessions (e.g., cookie via `document.cookie`).
- Account takeover (e.g., impersonate authenticated users).
- Force users into attacker-controlled sessions.
- Capture key strokes via injected JavaScript.
- Steal form data before submission.
- Target payment forms or financial info.

### Steps to Reproduce:
1. Navigate to `http://localhost/dvwa/vulnerabilities/xss_r/?name=`.
2. Try to inject `<img src=x onerror="setTimeout(alert(1), 0)"` in search parameter.
3. The browser executes the injected `alert(1)` script.  
  
<span style="color: yellow">[Recommended]</span> check the testing process => [How i tested](./XSS_dvwa_medium.md)  
  
