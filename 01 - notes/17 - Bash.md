# Bash Expansions:

#### introduction: shell expansions
in this chapter: 
   - You will learn about shell expansions
   - they allow you to simplify complex operation in bash
   - it will also explain the difference between: 

   ```
   cat $PWD/*.txt

   cat "$PWD/*.txt"

   cat '$PWD/*.txt'
   ```

-------------------------------------------
# What is shell expansion?
   - Bash Dynamically rewrites the command before execution
   - this allow us to use variables patterns or special characters without each program needing to implement them itself
   - Examples: 
      - Dynamic variable replacement ($PWD, $HOME, ...)
      - Filename matching with wildcard(*.txt)
   - we can test This :
   ``` echo ~/*.txt ```

--------------------------

# Tilde expansion

This command lists our home folder:

``` ls ~ ```

   - The ~ character triggers the tilde expansion
   - This character is being expanded to the value of HOME

we can test this:
   ``` echo ~ ```

We could also use it with plus:

   Then it expands to the variable PWD
   ``` echo ~+ ```

-------------------------
# variable expansion

The variable expansion allows bash to dynamically replace variables with their values during execution.

Examples of usage:
```
echo $HOME
echo ${HOME}
echo "$HOME"
echo "${HOME}"
```
Bash rewrite the command for us and fills in the variables
it is best to always add double quotes around it (more on that later)

we should try to use curly braces:

This makes it more clear where the variable ends

```
echo "${HOME}path"
echo "$HOMEpath"
```
-----------------------------

# shell parameter expansion

we can also run string operations all from within Bash

it requires variable to be defined first
Examples:
   - Query the length of a string:
   ``` echo "${#HOME}" ```
   - Cut out a string (substring extraction):
   ``` echo "${HOME:start:length}" ```
   - Replace a  substring (all occurrences):
   ``` echo "${HOME//pattern/replacement}" ```

------------------------------------------

# Filename expansion (globbing)

```*``` -> The wildcard character: *

  - ``` echo *.txt ```
  - Matches 0 to any number of characters

```?``` -> The wildcard character: ?

   - ```echo file?.txt```
   -Matches any single character

```[]``` -> Specifying a character range:[...]

   - ```echo file[0-9].txt```
   - Matches any single character that within this range

------------------------------------------

