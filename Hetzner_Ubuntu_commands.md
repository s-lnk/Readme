# Hetzner Ubuntu commands
Show current state of firewall
'''
sudo ufw status verbose
'''
Show listening ports
'''
ss -ltnp
'''
Switch user
'''
su - USERNAME
'''
List running services
'''
systemctl list-units --type=service --state=active
'''
Add read/write rights to folder
'''
sudo chmod o+w ./storage/ -R
'''