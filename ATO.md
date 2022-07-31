1. Check if user@email.com and user@email.coM are interpreted as same.
2. **Pre-Account Takeover** : A pre-account takeover occurs when an attacker creates a user account using one signup method and the victim creates another account using a different signup method using the same email address. Because the email addresses are the same, the application connects the two accounts. when the app is unable to validate email addresses.
	How to hunt :-
		-   Try registering any email address without verifying it.
		-   Try registering an account again, but this time with a different method, such as ‘sign up with Google’ from same email address.
		-   Due to the fact that both email addresses are the same, the web application will link the two accounts.
		-   Now try logging in using the specified password and username. Check to see whether you can see information from that account that was retrieved via Google.
3. ritik@gmail.com == r.i.t.i.k@email.com
4. Check if password reset, change email token recieved as confirmation in Email works with another account.
5. 