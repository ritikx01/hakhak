## Manual
1. Check for directories mentioned in [[Custom Wordlist]]
2. Curl the website and replace "Host" with IP or random Values
3. Check SSL certificate for domains/subdomains
4. Bruteforce VHosts
5. Send requests multiple times to check for load balancers
6. Check TXT Records (dig tomain.tld TXT)
7. Check the server used to load resources.(JS, CSS)
8. Reverse whois using `https://tools.whoisxmlapi.com/reverse-whois-search`
9. Find directories and buckets by analysing the path of assets. (Images, JS or CSS)
10. When using waybackurls, use the following regex to find parameterized URLs
	 `\/[A-Za-z0-9_.-][a-z]\?.*=`


# For Finding Subdomains/Endpoints
- Find subdomains
- Find IP
- Find open Ports
----------------------------------
## Bruteforce VHOST 
1. Use server IP (curl or proxy)
2. Use ffuf or gobuster
------------------------------------------------------------------------
# Subdomain Enumeration Tools (Active/Passive):
   1. Subfinder
   2. Sublister ###
   3. Findomain ( findomain --target domain.tld --threads -o) (or --file)
   4. Amass
   5. Ctfr ###
   6. crobat
   7. Assetfinder
   8. Gauplus / unfurl
   9. DNSRecon (dnsrecon -d vulnbegin.co.uk -D ~/wordlists/subdomains.txt -t brt) 
   10. KnockPy ###
   11. Haktrails (Securitytrails API)
   12. Zone transfer (`dig axfr hipflasks.thm @10.10.156.230` or `host -t axfr hipflasks.thm 10.10.156.230`)
   13. From SPF Records `https://github.com/yamakira/assets-from-spf`
   14. From Github Subdomains `https://github.com/gwen001/github-search/blob/master/github-subdomains.py`
   15. Subdomain bruteforce using Subbrute and massdns
	   1. `$Tools/subbrute.py $Tools/massdns/lists/names.txt domain.com | massdns -r $Tools/massdns/lists/resolvers.txt -t A -a -o -w massdns_output.txt -`
16. Favicon hashing 
15. 
``` 
massdns -r $Tools/massdns/lists/resolvers.txt -t A -o S allsubdomains.txt -w livesubdomains.messy
sed 's/A.*//' livesubdomains.messy | sed 's/CN.*//' | sed 's/\..$//' > domains.resolved
```
16. Use tok (tomnomnom) two times, one with `-delim-exceptions -` flag.
	1. Merge both output.
	2. Use duplicat to deduplicate.
	3. and then bruteforce using httpx. (or puredns)
## Check the technologies used
1. Wappalyzer Browser extension.
2. Whatruns browser extension
3. BuiltWith browser extension
4. Nuclei scan
5. Webanalyze (CLI Tool)
## Scanners
1. Burp Scanner
2. Nikto
3. jaeles
4. 

## DNS
   1. DNS bruteforce using puredns (VPS recommended)
	   1. Use dnsvalidator to generate dns resolvers `dnsvalidator -tL https://public-dns.info/nameservers.txt -threads 200 -o resolvers.txt`
	   2. https://public-dns.info/nameservers.txt (Get public NS)
	   3. Trusted resolvers: 1.1.1.1, 8.8.8.8, 9.9.9.9, 8.8.4.4
   2. dnsgen (cat amass-output.txt | dnsgen - | httprobe)
## Crawling
1. Use gospider. Probe subdomains using httpx and feed to gospider. Extract subdomains using below command.
	`cat gospider.txt | grep -Eo 'https?://[^ ]+' | sed 's/]$//' | unfurl -u domains | grep ".example.com$" | sort -u scrap_subs.txt`	
2. Use SecretFinder on URLs

### Passive checks, on websites
1. Shodan
2. Censys
3. Nerdydata

## Ports
   1. httprobe 
   2. Check for domain on shodan for top ports to probe.
   3. Common ports	   `81,300,591,593,832,981,1010,1311,1099,2082,2095,2096,2480,3000,3128,3333,4243,4567,4711,4712,4993,5000,5104,5108,5280,5281,5601,5800,6543,7000,7001,7396,7474,8000,8001,8008,8014,8042,8060,8069,8080,8081,8009,8083,8088,8090,8091,8095,8118,8123,8172,8181,8222,8243,8280,8281,8333,8337,8443,8500,8834,8880,8888,8983,9000,9001,9043,9060,9080,9090,9091,9200,9443,9502,9800,9981,10000,10250,11371,12443,15672,16080,17778,18091,18092,20720,32000,55440,55672`
   4. Using unimap
	   1. ` sudo unimap --fast-scan -f subdomains.txt --ports $COMMON_PORTS_WEB -q -k --url-output > unimap_commonweb.txt`
	   2. First initialize `COMMON_PORTS_WEB=$above_ports`
	   3. Combine with httpx
		   `cat unimap_commonweb.txt | httpx -random-agent -status-code -silent -retries 2 -no-color | cut -d ' ' -f1 | tee probed_common_ports.txt`  

## Favicon lookup
1. Shodan favicon lookup
	1. Grab the URL of the favicon.
	2. Put the URL in the favicon_hash script. (https://gist.github.com/ritikx01/8e20667107a957060d427ac1b3f10c20)
	3. On shodan search `http.favicon.hash:<hash>`
2. Grab favicon, pass to md5sum and compare with [https://wiki.owasp.org/index.php/OWASP_favicon_database](https://wiki.owasp.org/index.php/OWASP_favicon_database) to fingerprint technologies
 -------------------------------------------------------------------------
 ## Find JS files
1. [ScriptHunter](https://github.com/robre/scripthunter) (Manual)
 -------------------------------------------------------------------------
### Finding links from .js:
   - Linkfinder
   - JS Files can contain endpoints for [[IDOR]]

### On Github:
   Search for endpoints on github
  ## Keywords 
Burp suite search keywords:
```
uri=
url=
key=
.json
oauth
redirect=
api
dashboard
config.
=http
&api
@ (for user based URL for [SSRF])
dir
file
php_path
page
data
val
root
?q
?query
Token
user
db
```

## On main page
1- Bruteforce parameters (Arjun or x8)
Check for parameters. https://github.com/lutfumertceylan/top25-parameter

## Wayback
1- robots.txt
2- main page (/index)

## ASN lookup
bgp.he.net
