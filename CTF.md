- FTP connect
	- ftp <ip> 

-  MySQL connect
```
mysql -h remote-ip -u<username> -p<password>
```
- NFS Service (Port 2049/tcp). Use:
```
showmount -e <ip>                                                                 //Shows which folder can be mountrd, suppose /opt/files *
mkdir /mnt/to_mount
mount <ip>:/opt/files /mnt/to_mount
ls to_mount
```

## Apache Tomcat resource: https://vk9-sec.com/apache-tomcat-manager-war-reverse-shell/

MySQL Login:
mysql -h remote-ip -u<username> -p<password>

Proxy the terminal:
export http_proxy='http://127.0.0.1:8080'
export https_proxy='https://127.0.0.1:8080'