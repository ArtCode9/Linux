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

