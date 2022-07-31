1) Change Content-Type Header to image/png
2) Append the required extension i.e. png/jpeg
3) If the server is validating file size, use a smaller webshell
4) Change the magic number if it is bieng valdiated 
5) If the php file is uploaded but not executed, change the .htaccess file. Add the below contents to a file named .htaccess, upload it and then upload and execute the shell.
    `AddType application/x-httpd-php PHP`
6) XSS vaia SVG image upload
7)  Check if the application is using serverless computing. Eg: AWS S3 etc for file storage.
	1) Test for Denial of Wallet Attack 
	2) Upload a file of around 500mb. (Any upload functionality including Profile pictures of size > 100GB)
	3) DoW can incurr huge charges to the organization.
	4) References: 
		1) https://portswigger.net/daily-swig/denial-of-wallet-attacks-how-to-protect-against-costly-exploits-targeting-serverless-setups
		2) https://medium.com/geekculture/denial-of-wallet-attack-3d8ecadfbd4e