## File Permissions

File permissions are critical for system security and access control. This handout covers how Linux
handles file permissions, numerical and symbolic methods to set permissions, and permissions specific to
directories.

### 1️⃣. Why File Permissions?

File permissions control who can: 
   - ***read*** (View content)
   - ***Write*** (modify or delete)
   - ***Execute*** (run as a program or enter a directory )

Permissions are assigned separately for:
   -  ***Owner***
   -  ***Group***
   -  ***Others***(everyone else) 

### 2️⃣. Permission Types :

|Permission  | Symbol | Numeric | Files | Directories |
|-----------|-------|-------|--------|--------|
|Read| r | 4 |View file contents|List directory contents|
|Write| w| 2 |Modify/delete file|Create/delete files in directory |
|Execute|x | 1| Execute file as program|Enter/traverse directory|
------------------------------

###  3️⃣. Viewing Permissions

Use ```ls -al``` to view permissions:
```ls -al filename.txt```

Example output:
```
-rwxr-xr-- 1 alice alice 4096 Mar 20 16:05 filename.txt
```
- First character: ```-``` for a file, ```d``` for directory
- Next three (```rwx```) -> Owner permissions
- Next three (```r-x```) -> Group permissions
- Last three (```r--```) -> Others permissions

------------------------------------------

### 4️⃣. Setting Permissions (Symbolic)

Use  ```chmod``` to change permissions symbolically.

Syntax: ```chmod [u|g|o] [+|-] [r|w|x]``` filename

Example: 
- Add execute for owner ```chmod u+x script.sh```
- Remove write permission for group```chmod g-w file.txt```
- Add read permission for others:
```chmod o+r public.txt```

---------------------
### 5️⃣. Numerical Permissions (chmod)

Numerical permission simplify setting permissions. Each digit ( ***0-7*** ) combines permissions.

- Read (4), Write (2), Execute (1)

| Numeric Value | Permissions | Description |
| -------------|------|-------|
|7|rwx|Read, write, Execute| 
|6|rw-|Read, write | 
|5|r-x|Read, Execute|
|4|r--|Read-only|  
|3|-wx|write, Execute| 
|2|-w-|write-only| 
|1|--x|Execute-only| 
|0|---|No permissions| 

---------------------

Example : (```chmod 754 file.txt```):
   - Owner (7) -> ```rwx``` (Read, write, execute)
   - Group (5) -> ```r-x``` (Read, Execute)
   - Others(4) -> ```r--``` (Read-only)

Usage: 
``` chmod 754 filename.txt```

---------------------------

### 6️⃣. Directory Permissions

Directories have special behaviors:

   - Read (r) -> List files in the directory
   - Write (w) -> Add/Remove files (require execute x)
   - Execute (x) -> enter directory (cd) and access files directly

Example: 
   - Five owner full permission, deny others:
   ```
   chmod 700 private_folder
   ```
   - Allow everyone to list files, but no write/execute:
   ```
   chmod 444 public_folder
   ```

***Important***: To create/delete files, directory must have ```write (w)``` and ```execute (x)``` permission set.

--------------------

### 7️⃣. Changing Ownership (```chown```)

Change file owner/group.

Syntax : ```chown user:group filename```

Examples:
   - change owner only: 
   ``` sudo chown alice file.txt```
   - change owner and group: 
   ``` sudo chown alice:developers file.txt```
   - Recursively change ownership (R):
   ```sudo chown -R user:group directory```
   - It is recursively applied to all files and subdirectories inside a given directory.

------------------------
### 8️⃣. Recursive Permissions

Apply permission changes to directories and all contents recursively.
   - Change permissions recursively (R):
   ```chmod -R 755 website_folder```


## 🚩 Important Security Recommendations

   - ***Do not use ```chmod 777``` carelessly*** : 
   It grants everyone full access, potentially dangerous.

   - Prefer restrictive permissions:
      - ```755```for directories (owner full, others read/execute).
      - ```644```for files (owner read/write , others read-only).
   - Regularly review permissions with ```ls -al```

---------------------------------------

📌 Summary of key Commands

| Command  |  Description |
|---------|------------|
|```ls -al filename ```| View detailed permissions   |
|```chmod u+x file ```| Add execute permission to owner   |
|```chmod g-w file ```| Remove write permission from group   |
|```chmod 755 directory ```|Set numeric permissions (e.g., web folder)    |
|```chmod -R 644 directory ```| Recursively set numeric permissions for all files   |
|```sudo chown user:group file ```| Change file ownership   |
|```sudo chown -R user:group directory ```| Change ownership recursively   |
---------------------------------------------


File permissions in linux: <br>
 Why do we need file permissions? <br>
 ⏵ Controls access to files and directories <br>
 ⏵ Determines who can read, write and execute files <br>

 How are permissions defined? <br>
  ⏵ We need to differentiate between user classes and permission bits

User classes : ```Owner (u)  Group (g) Others (o)``` <br>
Permission bits: ```Read (r / 4) Write (w / 2) Execute (x / 1)```

--------------

Accessing permissions: 
<br>

⏵ Example:  
   - ``` ls -l ```
   
⏵ Example permissions:  
   - ``` -rw-rw-r-- 1 jannis jannis ```

⏵ Let's split it: <br>
 - ```-```: This file is a regular file <br>
 - ```rw-```: The owner (jannis) can read and write to this file<br>
- ```rw-```: The group (users) can read and write to this file <br>
- ```r--```: Others are allowed to read this file <br>
- ```1```: Link count to this file (usually: 1 for regular files) <br>
-  jannis: The owner of this file <br>
-  jannis: The group of this file

---------------------------------------------

### Changing permissions

For this, we can use the chmod command: 
```
 chmod [class][+/-][permission] [file]
 chmod u+x file.sh 
```

 We can also specify the permissions in a numerical way: 
 ```
 chmod 754 file.sh
 ```
   - 7: the owner can read (4) + write (2) + execute (1)
   - 5: the group can read (4) + execute (1)
   - 4: All other can only read (4) thi file

To change the owner : 
```
chown [user] [file]
chown [user]:[group] [file]
chown root:root file.sh
```

----------------------------

================AI section add ===========

These are not beginner traps — these are real Linux permission concepts.

1️⃣ Special permissions (biggest omission)

Missing entirely:

SUID (s)

SGID (s)

Sticky bit (t)

These explain:

Why /usr/bin/passwd works

Why shared directories behave safely

Why /tmp is secure

You hinted at them accidentally with rws, which makes this omission more noticeable.

2️⃣ umask (default permissions)

You explain permissions well, but not:

Why new files are not executable by default

Why directories default to 755 or 775

That’s umask, and learners always ask about it later.

3️⃣ Difference between chmod -R on files vs directories

You warn about recursion, but not:

Why chmod -R 644 directory is dangerous

Why directories need x to be usable

This is a classic production mistake.

4️⃣ chgrp command

You explain group ownership but don’t mention:

chgrp (group-only ownership change)

Not critical, but completes the mental model.

5️⃣ ACLs (advanced but worth a mention)

Modern Linux often uses:

getfacl

setfacl

Even a one-line mention would signal “this is not the whole story”.

Minor conceptual clarifications

These aren’t wrong, just slightly simplified:

Write permission on a directory does not allow reading file contents

Deleting a file depends on directory permissions, not file permissions

Execute on a directory ≠ execute a program

You’re mostly right already — this would just sharpen precision.
