# SSH and Webserver Essentials

1. Introduction

Tha main goal is to deploy a simple HTML website to a linux web server . 

Key steps:
   - Connect remotely using SSH
   - Secure your sever with SSH keys
   - Manage your server remotely
   - Transfer files to the server via SCP/SFTP
   - Install And manage an apache web server
   - Publish a website online

--------------------

2. understanding SSH (secure shell)

SSH is cryptographic protocol for secure remote login to linux servers.

   - ***server-side***: (usually pre-install): accepts incoming connections.
   - ***client-side***: Connects to the ssh servers

Basic Connection:
```
   ssh user@server_ip
```
if SSH runs on a non-default port (default port is 22):
```
   ssh -p 222 user@server_ip
```

-----------------

3. Server options:
   - Dedicated Server -> Entire physical server rented (high security/performance).
   - Virtual Server -> Shared server slices(cost-effective, minimal isolation risk)
   - Managed Server -> provider manages updates/security
   (less control)
   - Unmanaged Server -> user manages updates/security (more control)
----------------

4. Renting Server (Example: DigitalOcean)

steps:
   - A: create a digitalOcean account
   - B: rent a Droplet(virtual server):
      - select a server region, OS (ubuntu) and plan
   - set authentication method (password initially, later SSH keys)
   - Connect via SSH (e.g ```ssh root@server_ip```)

--------------------------

5. Alternatives to renting

Local Virtual machine (VirtualBox)
   - Set networking to bridged Adapter
   - install SSH server
```
sudo apt install openssh-server
```
   - Connect using VM's IP address from host machine

LocalHost SSH server (for practice)
   - install SSH server locally
```
sudo apt install openssh-server
```
   - connect to yourself:
```
ssh user@localhost
```

--------------


6. Changing ssh default port

ssh on port 222 for security (fewer automated attacks):

Edit /etc/ssh/sshd_config file:
```bash
sudo nano /etc/ssh/ssh_config
```
Change/add line:
```
port 222
```

Reload and restart SSH:
```
sudo systemctl daemon-reload
sudo systemctl restart sshd
```
Connect with new port:
```
ssh -p 222 user@server_ip
```
-------------------

7. Securing SSH (Public/Private Key)

Secure server authentication using keys (instead of passwords)

generate key pair:
```
ssh-keygen -t ed25519
```
   - Private key: ```~/.ssh/id_ed25519 (keep secret 🥷)```
   - Public key: ```~/.ssh/id_ed25519.pub (upload to server)```

upload public key to server's ```~/.ssh/authorized_keys```

Disable password login:

Edit ```/etc/ssh/sshd_config``` and set:
```
PasswordAuthentication no
kdbInteractiveAuthentication no
UsePAM no
```
Restart SSH:
```
sudo systemctl restart sshd
```

-----------------------

8.Installing Apache webserver:

Install Apache:
```
sudo apt install apache2
```
   - Default served directory -> ```/var/www/html```
   - Default config -> ```/etc/apache2/apache2.conf```
   - Website available at -> ```http://server_ip```

Apache logs:

   - Access logs -> ```/var/log/apache2/access.log```
   - Error logs -> ```/var/log/apache2/error.log```
--------------------

9. Manage Linux Services (systemctl)

Control server processes like apache via ```systemctl```

| command | Description |
|------|-----|
|```sudo systemctl status apache2```| Check service status|
|```sudo systemctl start apache2```| Start service|
|```sudo systemctl stop apache2```| Stop service|
|```sudo systemctl restart apache2```| Restart service|
|```sudo systemctl enable apache2```| Enable auto-start at boot|
|```sudo systemctl disable apache2```| Disable auto-start at boot|
|```sudo systemctl reload apache2```| Reload configuration without restart|
----------------------------


10. Uploading file to server (SCP and SFTP)

using SCP (secure copy)

syntax:
```
scp -rp -P port local_path user@server_ip:/remote_path
```
   - ```r``` -> recursive (folder/files)
   - ```p``` -> preserve modification timestamps
   - ```P``` -> custom SSH port (optional)

Example:
```
scp -rp -P 222 ./mywebsite root@123.456.78.90:/var/www/html
```

Using SFTP (graphical)

Linux -> Open File browser and enter URl:
```
sftp://root@123.456.78.90:222
```
- Drag-and-drop files
- Recommended graphical tools:
   - Cyberduck
   - FileZilla
---------------

## 📌 Summary of key commands:
|command | Description |
|----|----|
|```ssh user@server```| Connect via ssh|
|```ssh-keygen -t ed25519```| Generate SSH key pair|
|```scp -rp -P port local remote```| Securely copy file via SCP|
|```sudo apt install apache2```|Install apache web server|
|```sudo nano /etc/ssh/sshd_config```| Edit ssh configuration|
|```sudo systemctl restart sshd```| Restart SSH deamon|
|```sudo systemctl start apache2```|Start Apache service|
|```sudo systemctl stop apache2```|Stop apache service|
|```sudo systemctl restart apache2```|Restart apache service|
|```sudo systemctl enable apache2```|Enable apache to start at boot|
|```sudo systemctl disable apache2```|Disable apache from starting at boot|
|```sudo systemctl status apache2```|Check apache service status|
 


