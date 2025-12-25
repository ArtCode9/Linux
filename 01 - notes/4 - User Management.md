# User Management


Managing users is essential for securing your Linux system and controlling permissions. This handout
covers user creation, modification, deletion, privilege escalation, password management, and more.

----------------------
1️⃣. Types of User in Linux:

linux system have ***three main types of users*** :
- Root User (UID 0)
   - Highest privileges
   - Can perform any action
- Regular Users
   - limited privileges
   - can temporarily get elevated privileges via ``` sudo ```
- Service Users
   - Used by services (e.g web server)
   - Isolated from regular users for enhanced security
----------------------
2️⃣. Important User Management Files

- ```/etc/passwd```
   - Contains basic user info : username, UID, GID, description,home directory, and default shell.
   - Does not store password
- ```/etc/shadow```
   - Contains encrypted passwords and password-aging details
   - only readable by root or privileged users
- ```/etc/group```
   - Stores group info and membership
-----------------
3️⃣. Creating Users(useradd)

basic syntax:
```
   sudo useradd -m username
```
- ```m``` -> Create home directory ( /home/username)
- ```d /custom/home``` -> Set custom home directory
- ```s /bin/bash``` -> set default shell explicitly
- ```g primary_group``` -> set primary group
- ```G secondary_groups``` -> Add secondary groups (comma-separated) 

Example: <br>
``` sudo useradd -m -s /bin/bash alice```

check newly created user details:<br>
```cat /etc/passwd | grep alice```

----------------
4️⃣. Managing Passwords (passwd)

Set/change user password: 
``` sudo passwd username```

Display password status:
```passwd -S username```

set password expiry: 
```sudo passwd -n 7 -x 30 username```
   - ```n``` -> minimum days before changing again
   - ```x``` -> maximum days password is valid
-------------------
5️⃣. Modifying Users ( usermod )

modify user details: ```sudo usermod [option] username```

common option: 
   - ```c "Full Name"``` -> Set user description (full name)
   - ```s /bin/bash``` -> Change default shell
   - ```d /new/home -m``` -> Move Home directory to new location
   - ```l new_username``` -> Change Unix username
   - ```g new_primary_group``` -> Change primary group
   - ```G additional_groups``` -> add secondary group

Example: (changing shell and description)<br>
```sudo usermod -s /bin/bash -c "Alice B" alice```

-----------------------------------------
6️⃣. Deleting Users (userdel)

Basic deletion: ```sudo userdel username```

Options: 
   - ```r``` -> Remove home directory and mail
   - ```f``` -> Force removal even  if user is logged in

Example : ``` sudo userdel -r max```

--------------------------
7️⃣. Switching User ( su )<br>

Switch to another user: ```su username```<br>
Switch to root: ```su - ```

- Requires target user's password (not your current user's password).
--------------------------------
8️⃣. Temporarily Changing Privileges ( sudo )

Execute commands with root privileges (temporarily)
```
sudo command
```
Example : <br>

- install software -> ```sudo apt-get install vim```
- open root shell -> ```sudo -s```

Configure sudo access via: 

``` /etc/sudoers```  (edited safely via ```visudo```)

Allow user full sudo access:
```
username ALL=(ALL:ALL) ALL
```

Allow ***passwordless sudo*** for a specific command (careful!!!):

```username ALL=(ALL) NOPASSWD: /usr/bin/apt-get```

- use ```which``` command to find exact command path (e.g ```which apt-get```)
---------------------------
9️⃣. Sudo into another User( ```sudo -u```):

Execute commands as a different user (without their password):
   ```
   sudo -u username command
   ```
Start shell as another user: 
   ```
   sudo -u alice -s 
   ```

Example (Create a file as another user ):

   ```
   sudo -u alice touch /home/alice/file_sudo.txt
   ```

📌Summary of Key Command:

|  Command  | Description |
|---------|------|
|  ```sudo useradd -m username ```     |  Create a user with home directory     |
|  ``` sudo passwd username ```     | Set/change user's password      |
|  ```sudo passwd -n 7 -x 30 username ```|set min/max password age (days) |
|  ```sudo usermod -s /bin/bash username ``` | Change User's shell       |
|  ```sudo usermod -c "Full Name" username``` |   Change user's full name/description    |
|  ```sudo userdel -r username ```     |    Delete user and home directory   |
|  ```su - username ```     |   Switch to another user    |
|  ```sudo -u username command ```     | Run command as another user      |
|  ``` sudo -s```     |   Start a root shell session    |
|  ```sudo visudo```     |    Safely edit sudo configuration   |
------------------------------


### Elevating privileges: sudo
⏵ If we want to temporarily elevate our privileges...  
⏵ ... we can put a sudo (super user do) in front of our command

⏵ Example: 
⏵ ```sudo ls /root ```           
⏵ As a normal user, we don't have access to this directory...  
⏵ … but sudo elevates our privileges

⏵ We can also launch a shell: 
⏵ ```sudo -s  ```    

 And, we can also change to a different user:

  For this, we need to use the parameter: -u [username]<br> 
⏵ ```sudo -u alice  ```       


#### The dangers of sudo

⏵With great power comes great responsibility:  
⏵Always make sure you understand what a command does<br> 
⏵Especially if sudo is involved

⏵Example: <br>
⏵⚠⚠⚠ DO NOT EXECUTE! ⚠⚠⚠ <br>
⏵ ```sudo rm –rf / ```


--------------------------------
=================AI section ================
These are not nitpicks — these are real-world missing pieces.

1️⃣ Groups management as a topic (not just mentioned)

You mention groups, but you don’t teach how to manage them.

Missing commands:

groupadd

groupdel

groupmod

groups username

id username

Why it matters:

Permissions are group-based

Sudo, file access, services → all rely on groups

This is the biggest gap.

2️⃣ User IDs (UID/GID) concepts

You mention UID 0, but don’t explain:

UID vs GID

System users usually < 1000

Regular users usually ≥ 1000 (distro-dependent)

This helps learners understand system users, not just memorize commands.

3️⃣ Login shells & non-login users

You mention shells, but you don’t explain:

Why service users often use:

/usr/sbin/nologin

/bin/false

Why this improves security

This is important for hardening systems.

4️⃣ Difference between su and sudo

You explain both, but you don’t compare them explicitly.

A missing conceptual point:

su → full session, shared password

sudo → per-command, logged, auditable

Admins care about this distinction a lot.

5️⃣ Account locking / disabling users

Very common admin task, missing here.

Examples conceptually (not code repetition):

Lock account without deleting it

Disable login temporarily

Expire an account

This matters for:

Employees leaving

Security incidents

Temporary suspensions

⚠️ Minor clarity issues (conceptual, not grammar)

These are small but worth fixing mentally:

Regular users don’t “get elevated privileges” themselves
→ sudo grants command-level elevation, not user elevation

sudo -s vs sudo -i distinction is not mentioned

Passwordless sudo deserves an even stronger warning (audit & abuse risk)
