# Server side template injection
- SSTI can be detected by using a sequence of special characters. Ex- `${{<%[%'"}}%\`

```
{{7*7}}
${7*7}
<%= 7*7 %>
```
