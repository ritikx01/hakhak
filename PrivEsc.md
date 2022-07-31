1. Powershell privilege escalation script: PowerShell Mafia 


# Linux PrivEsc
1. Find a suid binary which gives privillege of another user (root probably)
```find / -perm -4000 -print 2>>/dev/null```
