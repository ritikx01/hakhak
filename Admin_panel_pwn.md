1:- Using google dorks. 
site:target.com inurl:admin | administrator | adm | login | l0gin | wp-login
intitle:"login" "admin" site:target.com
intitle:"index of /admin" site:target.com
inurl:admin intitle:admin intext:admin


2:- Using httpx and a wordlist:-
httpx -l hosts.txt -ports 80,443,8009,8080,8081,8090,8180,8443 -paths /root/admin-login.txt -threads 100 -random-agent -x GET,POST  -tech-detect -status-code  -follow-redirects -title -content-length
[admin-login.txt](https://github.com/emadshanab/admin-login)

httpx -l hosts.txt-ports 80,443,8009,8080,8081,8090,8180,8443 -paths /root/admin-login.txt -threads 100 -random-agent -x GET,POST  -tech-detect -status-code  -follow-redirects -title -content-length

3:- Using some programs:-
[https://github.com/the-c0d3r/admin-finder](https://github.com/the-c0d3r/admin-finder)
[https://github.com/RedVirus0/Admin-Finder](https://github.com/RedVirus0/Admin-Finder)
[https://github.com/mIcHyAmRaNe/okadminfinder3](https://github.com/mIcHyAmRaNe/okadminfinder3)
[https://github.com/penucuriCode/findlogin](https://github.com/penucuriCode/findlogin)
[https://github.com/fnk0c/cangibrina](https://github.com/fnk0c/cangibrina)
[https://github.com/s0md3v/Breacher](https://github.com/s0md3v/Breacher)

### Bypass
1. Crawl with gospider and anaalyse JS files

- Search for "Login" on shodan