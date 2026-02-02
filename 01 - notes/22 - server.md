# Different types of server
Dedicated server

   - You rent an entire physical server for yourself
   - Ensures that no others run code on the same hardware
   - Particularly useful for privacy-sensitive applications
   - or when you require maximum (or predictable) resources

-----------------------

Virtual server

- You share a server with others
- Other people run code on the same hardware....
- ...but usually can not access your slice of the server
- best if you want to save costs

--------------------

# Managed vs. unmanaged server
Managed server

- Automated updates patches and security
- 24/7 managed by the hosting company
- Ideal for businesses lacking in-house staff
- but significantly less configuration options

Unmanaged server

- Full administrative control over configuration
- Requires self-managed updates and troubleshooting
- Suited for users with strong technical expertise
- Usually more affordable

---------------------

# Changing the port
By default the ssh server listens on port 22.

This causes some potential issues:
   - other computers may try hack our password...
   - ...and will randomly connect to our server
   - This pollutes the log and makes debugging more difficult

it is best to change the port:
   - for example to port 222
   - Heads-up:
      - if this port is blocked from firewall on the way to the server
      - the server may become unreachable
      - but we will also explore how to mitigate this 

------------------------

# SSH: Public / Private key
what is a key pair ?

 - we can imagine this as a combination of a key and lock...

 - just in a cryptographic way

---------------------
Key (technical term: private key):
   - Secret we should never this with anyone
--------------------
Lock (technical term: public key):
   - This can be public everyone can know about this
   - can be used to identify if the private key was used to sign a message
   - Together they are used for authentication
----------------
We can generate such pair:
   - ```ssh-keygen -t ed25519```
   - This key pair will then be stored in the folder ~/.ssh
--------------------------
The public key then needs to be placed on the server:
   - ```~/.ssh/authorized_keys```
   - Heads-up:
      - The permissions should be rather restrictive(600 = -rw-------)

Once this works, we can then turn off password authentication:
   - ``` /etc/ssh/sshd_config ```
   - We can set the following values:
      - ```kdbInteractiveAuthentication: no ```
      - ```PasswordAuthentication no ```
      - ```UsePAM no ```
-------------------------------------

# The command: systemctl
Most linux systems employ systemd to boot the system

Systemd is also responsible for launching background process

we can control it through the command systemctl

Here are some crucial commands:
   - To start a service:
      ```
      systemctl start apache2.service
      ```
   - To stop a service:
      ```
      systemctl stop apache2.service
      ```
   - To restart a service:
      ```
      systemctl restart apache2.service
      ```
   - To enable a service to be launched at boot:
      ```
      systemctl enable apache2.service
      ```
   - To disable a service from being launched at boot:
      ```
      systemctl disable apache2.service
      ```
------------------------------------------
# Copying files through SFTP
SFTP:
   - utilizes ssh to transfer files
   - can be utilized with most ssh servers

To transfer files through ssh we can use the program scp:
```
scp -rp [from] [to]
scp -rp ./Documents jannis@43.23.53.12
```
- ```-r```: Recursive (Allows us to transfer a whole folder)
- ```-r```: Retain last-modified timestamps
- Heads-up: if ssh is running on a different port we need to use -p: 
   - ```-p 222```

As an alternative to ```scp```:
   - Many graphical programs also offer sftp support
   - Example: File browsers on Linux, Cyberduck, FileZilla...

----------------


