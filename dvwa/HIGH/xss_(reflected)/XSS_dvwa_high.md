```
Tested by: Mikail Kakabayev (nulbyt3)
Date: 2025/23/07

---------- Details ----------
Lab: DVWA (Damn Vulnerable Web Application)
Vulnerability: Reflected Cross-Site Scripting (XSS)
Security Level: High
Endpoint: https://localhost/dvwa/vulnerabilities/xss_r/?name=
```

## Vulnerability Confirmed
Payload: `<img src=x onerror="setTimeout(alert(1), 0)"/>`  
Impact: Arbitrary JavaScript execution in victim's browser.  
Context: The application filters `<script>` tags but fails to sanitize event handlers in `<img>` tags.

## Testing Process
1. Entered the basic (test) into the search input to observe normal behavior:
![Basic Test](../test_process/basic_test.png)

2. Tried to inject basic HTML command `<script>alert(1)</script>` but it only shows `>` on the result.
![Basic JS Command](../test_process/basic_js_command.png)

3. Then injected many other HTML commands including:
- Case sensitive: `<ScRiPT>alert(1)</sCrIpt>`
- URL encoded: `%3c%73%63%72%69%70%74%3e%61%6c%65%72%74%28%31%29%3c%2f%73%63%72%69%70%74%3e`
- Null byte: `<script%00>alert(1)</script>`
- Extra whitespace: `<scrip \t>alert(1)</script >`  
  
4. Realized that it has BLACKLISTING protected functionality.  
5. Now, attempt to inject `<img src=x />`, and BOOM! It allows us to load an `<img>`.  
![Basic JS Command](../test_process/xss_img_tag.png)  

6. Finally, inject following HTML code:
`<img src=x onerror="setTimeout(alert(1), 0)"/>`
