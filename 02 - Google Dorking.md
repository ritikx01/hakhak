1. site:http://site.com ext:xml | ext:conf | ext:cnf | ext:reg | ext:inf | ext:rdp | ext:cfg | ext:txt | ext:ora | ext:ini | ext:log | ext:cfm | ext:jsp | ext:asp | ext:pl  | ext:sql | ext:xls | ext:json | ext:csv 
2. site:http://target.com intitle:"index of"
3. inurl:/proc/self/cwd
4. intitle:"index of" inurl:ftp
5. site:xyz.com/.env
6. site:http://target.com intitle:"index o /" "\*key.pem"
7. site:example.com inurl:app/kibana
8. inurl:site.com "MYSQL_ROOT_PASSWORD:" ext:env OR ext: yml -git
9. site:s3.amazonaws.com COMPANY_NAME
10. Copyright Text
11. site:http://repl.it intext:company 
12. site:http://zoom.us inurl:company 
13. site:http://atlassian.net inurl:company




Add "secret", "private" after Dorks













## Writeup/Tutorials
1. [mr.sinister writeup](https://infosecwriteups.com/dorking-for-bug-bounties-d81cc857b2c8)





## RAW Dorks
1. intitle
2. inurl
3. site
4. link
5. filetype
6. | (or)


## Helper
https://dorks.faisalahmed.me

## Open Redirect
```
inurl:url=https
inurl:url=http
inurl:u=https
inurl:u=http
inurl:redirect?https
inurl:redirect?http
inurl:redirect=https
inurl:redirect=http
inurl:link=http
inurl:link=https
inurl:redirectUrl=http site:paypal.com
```

## Pre Cooked
```

site:your-target.com inurl:id=
site:your-target.com filetype:php
site:your-target.com intitle:upload
inurl:”.php?id=” intext:”View cart”
inurl:”.php?cid=” intext:”shopping”
inurl:/news.php?include=
inurl:”.php?query=”
```