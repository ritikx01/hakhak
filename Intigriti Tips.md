## [Gitbook tips link](https://gowsundar.gitbook.io/book-of-bugbounty-tips/intigrity-tips)
1. Bypass paywalls using Google Bot user Agents. https://developers.google.com/search/docs/advanced/crawling/overview-google-crawlers
2. Try OPTIONS on api root path to see what endpoints exist.
3. Try Blind XSS as password
4. Use round brackets to Inject XSS,SQLi, RCE payloads in a valid E=mail address. https://twitter.com/intigriti/status/1078318258661531648
	1.  user(payload)@email.com  payload = {}<>"''"
	2.  user@(payload)email.com
5. Blind XSS, SQLi payloads in X-Forwarded-For
6. Look inside apk files
	1. Use APK Tools
	2. grep -r
7. Check an all e-mails [[Headers]] and Body
8. Google copyright footer to get more subdomains. "© 2019 Spotify AB" [Twitter](https://twitter.com/intigriti/status/1108365683069456385)
9. Take SS from eyewitness and sort them by size to get juicy information
10. Endpoint bruteforce on /login pages
11. Append .json at the end of a URL if it runs on Ruby
12. FUZZ non printable characters in user input. (0x00-->00x2F, 0x3A-->0x40, 0x5B-->0x60, 0x7B-->0xFF) [Reference](https://www.eso.org/~ndelmott/url_encode.html)
13. Put Long strings in POST parameters (50k chars or euler number 9e999 to gain very high values)
14. To find UUID of a user, register with their username. Error message ,may contain their UUID
15. 