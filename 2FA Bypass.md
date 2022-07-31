1. Response/Status Code Manipulation 
2. Brute force token. 
3. Token does not expires after usage. 
4. Request 2 tokens from account A and V. Use the A's token in V's account.
5. Try to go directly to the dashboard URL without solving the 2FA. If not success try adding the referral header to the 2FA page url while going to dashboard. 
6. Search the 2FA code in response and js files. 
7. [[CSRF]]/Clickjacking to disable 2FA.
8. Backup code abuse using these methods. (Try above methods on backup codes to reset 2FA)
9. Enabling 2FA doesn't expire previous sessions. 
10. Login using OAuth to bypass 2FA. 
11. No 2FA required for disabling 2FA. 
12. Password can be reset via forgot password without 2FA. 
13. Enter same number of 0(s) in the code.
14. 14. No 2FA on reset password. 
15. Request Manipulation: Try sending null response for JSON, discover and change params like "otprequired" to false, remove the 2fa code, remove both code and parameter, in JSON give email as an array.
16. Check whether 2FA page is disclosing some sensitive info that you didn't know previously (like mobile number).
17. Create an account with victim@gmail.com (If there is no email verification). Now enable 2FA in the account. So now victim can't create an account. 
18. After login, try to access different endpoints to perform actions from victim's account.
19. 2FA bypass using race conditions