## To do when a bucket is found
- FUZZ for directories. Use wordlist https://raw.githubusercontent.com/gwen001/SecLists/master/mine/s3-buckets.txt
- Sometime s3 buckets are open on image upload function, you can see that all images of registered users. 
	 1) image upload 
	 2) right click and copy image location 
	 3) you can see that remove your picture after / . all users private images disclosed.[[Broken Access Control]]

AWS CLI usage : https://aws.plainenglish.io/aws-s3-cli-cheatsheet-9078366fca83

## To find a bucket
1. Nuclei templates
2. site: s3.amazonaws.com "target"
3. Image or document upload functionality
4. Search the source code
5. `Dig` for CNAMES
6. Bruteforce 