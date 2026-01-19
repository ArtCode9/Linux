# The shell environment

We should delve deeper into the shell environment

let's Explore topics such as :
   -  understanding environment variables
   -  Configuring the shell environment
   -  Utilising aliases to simplify commands

---------------------------

# Environment variable
### What are environment variables ?
used to store configuration information and settings

They influence the shell and program behavior

By convention :
   - Written in UPPERCASE letters

To view them: 
   - ```env```

To access them: 
   - ``` echo "${PATH}" ```

Not recommended: 
   - ``` echo ${PATH} ```
   - ``` echo "$PATH" ```

----------------------------------

# The PATH variable
the PATH variable :
   - one of the most crucial variables of the shell environment
   - Stores a list of directories
   - Used to locate executable programs

Directories are separated by colons(:):

   ``` PATH="/usr/local/bin:/usr/bin" ```

the order of entries matters:
   - Directories are searched from left to right
   - if two executable files have the same name only the first one gets executed.

-----------------------

# modifying the PATH variable:
We can modify the path variable:
   - Allows us to add a directory with additional executable files

How modify it:
   - Typically we append a directory to the PATH variable:
   - ``` PATH="${PATH}:/new/path" ```

Best practices:
   - System directories should be kept at the running 
   - Directories should only occur once
   - Regularly clean up your PATH variable.

-----------------------------

# Configuring the environment 
How to store the configuration

➡️ Bash loads configuration using specific startup files:
   - This allows us to automatically apply our configuration

➡️ Bash uses several startup files to manage these setting:
``` 
   /etc/profile
   ~/.bash_profile
   ~/.bash_login
   ~/.profile
   ~/.bashrc
```

➡️ The problem :

Which of these files should we use for our configuration?
   - The quick answer usually:
   ```  ~/.bashrc ```

-----------------------

# Bash startup modes

👤 Interactive login shell 
   - direct login to a computer
   - Example :
      - Real terminal on a local machine
      - ssh to a remote server
---------------
💻 Interactive non-login shell
   - the user is  logged-in already
   - Terminal in a desktop environment
   - we launch a subshell  in an existing terminal:
      ```bash```
-------------
🌐 Non-interactive login shell 
   - Very rare almost never used
   - we could send a command to a remote server without starting an interactive shell

   ``` echo 'command' | ssh server ```

---------------
📜 Non-interactive non-login shell

when executing a shell script
Example: 
   ```
      bash ./script.sh
      ./script.sh
   ```
--------------------------------

# Which file is loaded ? 

 👤interactive login shell (= direct login)
 - first system-wide configuration:
   ``` /etc/profile ```
 - After the first available file: 
   ```
      ~/.bash_profile
      ~/.bash_login
      ~/.profile
   ```
----------
💻 Interactive non-login shell (= logged in already)
   - It always loads the same file:
   ``` ~/.bashrc ```

------------
🌐📜 non-interactive shells
bash looks for an environment variables BASH_ENV
- if found: 
   - it will try to execute it without looking in PATH

-----------------------

Passing  environment variable to programs
  - Environment variable are inherited to child process
  - they inherit the environment of their parent
  - We can also set environment variable inline:
   
   ``` MY_VARIABLE=hello python3 file.py ```
   - This allow us to transfer configuration into our application

------------------
Heads-up

Bash also supports variables 

These variables are just regular bash variables, not environment variables

Here’s an example of an environment variable:

   ```  export MY_VARIABLE=value  ```

Once it is an environment variable, we can also change it:  

   ```  MY_VARIABLE=value  ```

And here’s an example of a bash variable:
 
 ``` MY_VARIABLE=value   ```

--------------------------------

# Using alias to simplify commands
we can use an alias to shorten commands 
 
to create a new alias:

``` alias godesktop = 'cd ~/Desktop' ```

List all existing aliases: 

``` alias ```

Remove an alias:

``` unalias godesktop ```

important : 
   - alias are temporary (Valid for the current session only)
   - to make alias permanent we need to add theme to a startup file

----------------------------------

Download this pdf for this lecture and add note to a 16-1

https://downloads.codingcoursestv.eu/060%20-%20linux/handouts/Managing%20the%20Environment.pdf

https://downloads.codingcoursestv.eu/060%20-%20linux/handouts/Managing%20the%20Environment.pdf


