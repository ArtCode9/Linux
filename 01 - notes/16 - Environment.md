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

