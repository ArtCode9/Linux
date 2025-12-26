# Group Management

***groups help organize users and manage permissions effectively on linux***. this handout covers group creation, modification, deletion, and membership management.

--------------

## 1️⃣. Why use groups ?

Groups simplify permission management by assigning rights to a collection of users rather than individuals,
enabling:

- Controlled access to resources (files, printers, etc.)
- Enhanced system security
- Streamlined administration

-------------------------------
## 2️⃣.  Important Group Management Files

- ```/etc/group``` 
   - Stores group names, IDs (GID), and secondary group memberships.
- ```/etc/passwd``` 
   - Stores each user's primary group.

--------------------

## 3️⃣. Primary vs Secondary Groups

- Primary group →  Every user has exactly one primary group.
   - Default group ownership for new files.
   - Stored in ```/etc/passwd```
- Secondary groups → Users can belong to zero or more secondary groups.
   - Provides additional, granular permissions.
   - Stored in ``` /etc/group```

check user groups: 
   ``` groups username ```

check your own groups: 
   ``` groups```

-----------------------------------------

## 4️⃣. Managing Group Membership (```usermod```)

Change user groups
   - Add secondary group(s) to a user:``` sudo usermod -aG groupname username```
   - Set primary group (replace current primary group):``` sudo usermod 0g groupname username```
   - Replace all secondary groups (remove unspecified groups): ``` sudo usermod -G group1,group2 username```

Example: 
 - Add ```alice``` to the ```adm``` group:
 ``` sudo usermod -aG adm alice```
 - Remove user from a secondary group (must specify all remaining groups explicitly):``` sudo usermod -G plugdev,lpadmin alice```

 ----------------------

 ## 5️⃣.Easy Group Membership Management (```adduser``` & ```deluser```)

 Simpler commands (Ubuntu/Debian)
   - Add user group: ``` sudo adduser username groupname```
   - Remove user from group: ``` sudo deluser username groupname```

Example: 
``` 
sudo adduser alice adm
sudo deluser alice adm
```

Note: After changing groups, log out and log back in (or reboot) to ensure changes take effect.

-----------------------------

## 6️⃣. Creating Groups (```groupadd```)

Create custom groups with optional IDs.
   - Basic group creation (auto-assigned ID):
   ```
   sudo groupadd groupname
   ```
   - Custom group ID (GID):
   ```
   sudo groupadd -g 2500 groupname
   ```
Example: 
```
sudo groupadd -g 5000 developers
```
check group creation:
```
grep developers /etc/group
```

--------------

## 7️⃣.Modifying Groups(```groupmod```)

Modify existing groups: 
   - change group name:
   ``` sudo groupmod -n newname oldname```
   - chang group ID (careful !!) ``` sudo groupmod -g new_GID groupname```

Example: (rename group and change GID):
``` sudo groupmod -n webdev -g 6000 developers```

⚠️⚠️Warning: 
Changing GIDs can break file permissions, as existing files store group ownership by GID.

---------------------

## 8️⃣. Deleting Groups (```groupdel```):

Delete groups (not allowed for primary groups):
``` sudo groupdel groupname```
   - Does not delete files associated with the group.
   - Cannot delete groups assigned as a user's primary group.

Example:  ``` sudo groupdel webdev```

-----------

## 🔒Important System Groups

| Group Name |  Description |
|------------|--------------|
| ```root ``` | Full administrative privileges    | 
| ```sudo ``` | Allows members to use sudo    | 
| ```adm ``` | Access system log files    | 
| ```lpadmin ``` | Manage printers and queues    | 
| ```www-data ``` | Web server processes and file access    | 
| ```plugdev ``` | Mount and manage removable devices    | 

------
## 📌 Summary of key commands

| Command | Description |
|---------|-------------|
|```groups username ``` | List groups for user    |
|```sudo usermod -aG group user ``` |  Add secondary group(s)   |
|```sudo usermod -g group user ``` | Change user's primary group    |
|```sudo adduser user group ``` | Add user to group (Ubuntu/Debian)    |
|```sudo deluser user group``` |Remove user from group (Ubuntu/Debian)     |
|```sudo groupadd -g GID groupname ``` |Create new group with custom GID     |
|```sudo groupmod -n newname oldname ``` |  Rename group   |
|```sudo groupmod -g new_GID groupname ``` |  Change GID of existing group (caution!)   |
|```sudo groupdel groupname ``` | Delete group (except primary groups)    |


--------------------
### Motivation: Why do we need groups?
⏵ They help us with: <br>
   - Organizing users with similar access rights 
   - Simplifying permission management
   - Enhancing collaboration and resource sharing 
   - Controlling access to files and directories 
⏵ Thus, overall:
   - Strengthening system security

------------------------
### How do groups work? 

Each user has a primary, and zero to many secondary groups

Primary group:
   - Stored in ```/etc/passwd```
   - Default ownership for new files
   - We can test this : ``` touch file.txt```  ```ls -al file.txt```

Secondary group(s):  
   - Multiple memberships allowed
   - Stored in ```/etc/group```
   - This allows us to give this user fine grained access rights to our system
   - We can list a user's groups with the following command:
   ``` groups [username]```

----------------



