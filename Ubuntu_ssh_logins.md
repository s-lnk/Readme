# Ubuntu SSH logins
Set SSH public key for root user
'''
cd /root/.ssh
sudo nano authorized_keys
'''
Enter Your new key and save


Open SSH config
'''
nano /etc/ssh/sshd_config
'''

## Login to server with password only
Set /etc/ssh/sshd_config 
'''
PasswordAuthentication yes
'''
Restart service 
'''
service sshd restart
'''

## Copy and ungzip all files
'''
cp -r FROM TO
gunzip -r FOLDERNAME
'''

## Check if file is executable and set proper value
In your machine where you are building the docker image (not inside the docker image itself) try running:
'''
ls -la path/to/directory
'''
The first column of the output for your executable (in this case docker-entrypoint.sh) should have the executable bits set something like:
'''
-rwxrwxr-x
'''
If not then try:
'''
chmod +x docker-entrypoint.sh
'''