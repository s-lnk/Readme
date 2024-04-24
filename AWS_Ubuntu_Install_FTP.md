## AWS Ubuntu install FTP server

Log in to your AWS account. Under Security Groups expose ports 20-21 for FTP access and ports 1024-1048 as passive ports for Anywhere.
### Install and configure vsftpd
```
sudo apt-get update
sudo apt-get install vsftpd
sudo nano /etc/vsftpd.conf
```
Make the following edits:
```
listen=YES
#listen_ipv6=YES
anonymous_enable=no
write_enable=YES
connect_from_port_20=YES
pasv_enable=YES
pasv_min_port=1024
pasv_max_port=1048
pasv_address=54.165.49.1
port_enable=YES
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO
```
### Create FTP user
```
sudo adduser aloka
sudo passwd awsftpuser
echo "aloka" | sudo tee -a /etc/vsftpd.userlist
```
Check if You can connect locally:
```
ftp -p <public_ip>
```
### Set user permissions
```
sudo chown USER_NAME:USER_NAME /home/USER_NAME/FTP
sudo chmod 755 /home/USER_NAME/FTP
```
