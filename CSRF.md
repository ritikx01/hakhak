1) Use null characters in token `%00`
2) Remove the CSRF token/header requests with parameter
3) Replace the CSRF token with a random value (for example 1)
4) Replace the CSRF token with a random token of the same restraints
5) Use a CSRF token that has been used before
6) See if you can request a CSRF by executing the call manually and use that token for the request
7)  Check if it is a hash and try to crack it
8)  Remove the referrer header
	1)  \<meta name="referrer"> content="no-referrer"
9) Use overly long token e.g 4096 characters
10) Check CSRF while downloading any document.
11) Try changing POST to GET
12) Intercept a request with a valid token and use that token