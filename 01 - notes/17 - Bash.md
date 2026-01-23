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

# Word splitting 

Bash performs word splitting on our input.
This happens after our command has been rewritten by expansions

Example:
``` touch a.txt b.txt ```

this command will be split into 3 different words:

```
   touch
   a.txt
   b.txt
```

the first entry is then the program and the others become arguments to it

Where does  word splitting happen?
   - It occurs at any character that is listed in the variable IFS
   - By default it occurs at every space tab and newline character

Thus this would be equivalent:
``` touch a.txt   b.txt ```

------------------------
# How to disable word splitting ?

we can disable word splitting: 


we can wrap parts of the command into quotes:
```
   touch 'a file.txt'
   touch "a file.txt"
```

Without word splitting:

2 files would will been created('a' and 'file.txt')

However the quotes disable word splitting: 

Thus the filename will be : a file.txt

-----------------------------------------


### A quick heads-up
   - My college has come up with an excellent way to describe it: 
      - The more you know about programming the more confusing it becomes

   - Why is it like This? 
      - Bash handles quotes differently from other languages
---------------------------

 # How do quotes affect bash commands?

 What is the difference between the following command ?
 ```
      cat ${pwd}/*.txt
      cat '${pwd}/*.txt'
      cat "${pwd}/*.txt"
```
## No quotes: 
   - All available shell expansions are being applied
## Single quotes: 
   - All expansions are disabled word splitting is disabled
## Double quotes: 
   - Disables most expansions, including tilde expansion (~) filename, expansions(*), and word splitting.
   - However certain expansions are still enabled such as variable and parameter expansion
 
This would be the best practice!

#### Important!:::
Quotes in bash only control how command are expanded or where word splitting happens

they have no other function

### Thus, These commands are equivalent:
```
'echo' 'Hello'"world"
echo helloworld
echo "helloworld"
```

---------------------------

# Best Practice
Regrading quotes:
   - Always use the most restrictive quoting style possible
   - It is best to prefer single quotes: 'hello world'
   - if this is not feasible use double quotes
      ```
      echo "hello ${USER}"
      echo 'hello'"${user}"
      ```
Quotes can be omitted if the command is simple or expansions are needed:

No ambiguity(simple command):
   ``` ls -al ```

Her we want all expansions:
   ``` echo ~/file.txt ```

---------------------------------

# The danger of globbing:

Bash treats all files and parameters the same

But filenames can also act as parameters... let's say we had a file - 

What happens when ```rm * ``` is executed ?

1) ```*``` expand to all files including -rf
2) ```rm``` may think that -rf is a parameter
   - ```-r``` means: recursive
   - ```-f``` means: do not ask

What is the solution ? 

use ```./*``` instead of * to avoid this

💀 Dangerous:
```
   rm * 
```
🛟Safe: 

```
   rm ./*
```
-------------------------------------


# Command substitution: