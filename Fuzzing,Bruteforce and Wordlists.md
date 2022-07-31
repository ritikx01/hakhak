## Ways to FUZZ
1. ferroxbuster for recursive  directory bruteforcing. (Flags: -g -L 1 --force-recursion -e  -r -d 0)
2. File discovery with ffuf
3. Fuzzing with special characters. (https://domain.tld/endpoint/LIST1SPECIALWORDSLIST2)


## Places for Fuzzing
-  /Myadmin_FUZZ  (if found this endpoint do Fuzzing here and then do parameter bruteforcing)
	/api/FUZZ
	
- /admin/endpoint  --> 401 ; try : 
   /admin/FUZZ/endpoint
   /admin/endpoint/FUZZ
   
- If `target.tld/target/endpoint` redirects to /target/app/login (Login) do:
   /target/app/FUZZ
   /target/FUZZ
   
 - Use gau to get all urls, filter extensions like **_.php .aspx .jsp .js_**, check if alive using httpx, then fuzz.
	 **_redacted.com/x/y/z/anything.php_** --> **_redacted.com/x/y/z/FUZZ_** (Example: crossdomain.php)


## Check
https://github.com/the-xentropy/samlists

## Wordlists (Revised)
### For Files
raft-large-files.txt + common.txt + sam gh files lowercase
### For Directory
   - dnaielmiessler -- robots disallowed repo (curated.txt)
   - raft-large-directories.txt
   - sam gh directories
### For DNS bruteforcing
best-dns-wordlist.txt (wordlists.assetnote.io)
### For  VHost
- https://gist.githubusercontent.com/six2dez/a307a04a222fab5a57466c51e1569acf/raw 
### For parameters
sam cc parameters 
### More Bruteforce
- bak.txt (wordlists.assetnote.io)
### Create DNS Wordlist using chaos
- https://gist.github.com/m4ll0k/2df369418798717d12bef7f42138fb78
### Custom wordlist
- Burp extension scavanger 

## Wordlists (Deprecated)
#### General
403 bypass (FILE): raft large words
### For Directory
   - Default dirsearch wordlist
   - dnaielmiessler -- robots disallowed repo (curated.txt)
   - raft
   - directory-list-2.3-medium.txt
   - httparchive_directories (wordlists.assetnote.io)

### For Subdomain and VHost fuzzing
   - SecLists/Discovery/DNS/subdomains-top1million-xxxxxx.txt
   - https://gist.githubusercontent.com/six2dez/a307a04a222fab5a57466c51e1569acf/raw 
   - Assetnote best-dns-wordlist.txt 