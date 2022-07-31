Fierce --domain domain.com
## Naabu
-exclude-cdn    	Skip full port scans for CDNs (only checks for 80,443)
-iL string    			  File containing list of hosts to enumerate ports
-o string    			  File to write output to (optional)
 -p string   			  Ports to scan (80, 80,443, 100-200, (-p - for full port scan)
 -ping    				   Use ping probes for verification of host
 -verify    			   Validate the ports again with TCP verification
 
 naabu -iL file.txt -o ports -exclude-cdn -ping -verify
 
 ------------------------------------------------------------------------------------------------------
## Ciphey (For encrypted/encoded text )
https://github.com/Ciphey/Ciphey


## Tools/Scanners 
### Nikto
### For LFI
	- https://github.com/D35m0nd142/LFISuite
	- https://github.com/kurobeats/fimap
### gf patterns
	- https://github.com/emadshanab/Gf-Patterns-Collection
### CSRF
Bolt by Somedev (Forked in my github)

### Kiterunner
Commands:
```bash
kr scan ht
```