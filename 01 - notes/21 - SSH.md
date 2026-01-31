## Working with a remote server:
The leading question in this chapter:
   - How can we deploy a simple html page to a web server ?

For this we'll need to explore:
   - How to connect to remote server (SSH)
   - How to authenticate easily (private / public key)
   - How to easily upload files to a remote server (through ssh)
   - How to install a webserver (apache2) on the remote server

-----------------------------------

# What is SSH ?
Secure shell: A cryptographic network protocol

Encrypts all data transmitted between client and server

Most common use case: 
   - Securely access a remote terminal

For this, we need the following:
   - SSH server:
      - Needs to be installed on the server (usually pre-installed on rented server)
      - Accepts incoming connections
   - SSH client:
      - Most operating systems already ship with one
      - Usually we can just use the program ssh
      - Even windows we don not need to install anything

----------------
# How to access  a remote server ?
we can login as a user of our choice

This user needs to exist on the remote server

Example: 
   ```
      ssh jannis@43.23.53.12
      ssh root@43.23.53.12
   ```
   - it may then ask us for the password to continue with the login

   - Quite Often:
      - The ssh server runs on a different port
      - This prevents random attacks from flooding our log files
      - In this case we need to specify it:
         ``` ssh -p 222 jannis@43.23.53.12```

---------------------



