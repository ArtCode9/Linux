# Bash Expansions

1. Introduction to bash expansions
shell expansions allow bash to dynamically rewrite commands before execution enabling:
   - simplified syntax for complex operations
   - Dynamic variable replacement
   - Powerful file selection mechanisms.

Expansions happen before the command is executed.

---------------------------

2. tilde Expansions(~)
The tilde symbol expands to your home directory path.
   - Basic usage
   ```
   echo ~
   # output: /home/username
   ```
   - Current directory expansions(~+):
   ```
   echo ~+
   # Output the current working directory
   ```
------------------
3. Variable and shell parameter expansion

Variable Expansion($)

replace a variable with it is stored value:

Syntax: 
``` echo "${HOME}"```

Always prefer curly braces {} for clarity

Example:
``` echo "Home is: ${HOME}"```

Shell parameter Expansion

perform simple operation on variable strings.

   - Length of variable(#)
   ```
   echo "${HOME}"
   # outputs length of Home variable(e.g. 11)
   ```
   - Substring extraction:
   ```
   echo "${HOME:0:5}"
   # outputs  first  5 characters
   ```
   - Replace string variable (//):
   ```
   echo "${HOME//home/users}"
   # Replaces all occurrences of  home with users
   ```
--------------

3. Filename expansion(Globbing)

use wildcards for matching filenames.

   - ****```*``` Matches zero or more characters
   ``` ls *.txt```
   - ```?``` matches exactly one character:
   ```
   ls file?.txt 
   # Matches: file.txt, fileA.txt, but not file12.txt
   ```
   - Square brackets [] match one character within a range:
   ```
   ls file[0-9].txt
   # Matches: file1.txt, file2.txt, not fileA.txt
   ```

---------------

4. Word splitting

Bash splits  commands into separate arguments based on whitespace (space , tabs, newlines)

Example: 
``` touch file1.txt file2.txt ```

Bash splits this into:
   - command -> touch
   - Arguments -> file1.txt, file2.txt

To disable word splitting (e.g for filenames with spaces), use quotes
``` touch "my file.txt"```

-------------------
5. Quotes in bash commands

quotes affect expansions and word splitting:

| Quote Type | Variable expansion | Filename Expansion| tilde expansion | word splitting |
|-----|----|----|----|----|
|No quotes|✅|✅|✅|✅
|single quotes('')|❌|❌|❌|❌|
|Double quotes ("")|✅|❌|❌|❌|
---------------------
Best practice : use the most restrictive quoting style('') possible.

Example:
```
echo '$HOME/*.txt'  # No expansions (literal output)
echo "$HOME/*.txt"  # Expands HOME, no filename expansion
echo ~/*.txt        # Expands HOME and filenames
```

------------

6. Dangers of Filename Expansion

Globbing ↔ Matching filenames using wildcard characters(e.g., *).

Example (list all .txt files):
``` ls *.txt```

⚠ Potential dangers:

If filenames are misunderstood as command arguments:

Example dangerous scenario:

```rm *```

Note: Be careful with wildcards! A file named -rf could be interpreted as a command parameter when using rm leading to unintended deletions.

Safe approach:

Prefix filenames explicitly to avoid misinterpretation:

``` rm ./*txt```

---------------------

7. Command Substitution ( $(command) )

Execute commands and capture their outputs directly into another command.

Syntax:
```echo "Today is $(date)"```


Example (file count):
```echo "There are $(ls | wc -l) files."```

Note: Prefer $() over the older command syntax

--------------

8. Escaping Characters (```\```)

Use backslash (```\```) to prevent special characters from begin interpreted by bash.

   - Example (filename with space):
      ```touch my\ file.txt```
   - Escaping quotes within quotes:
      ```echo "Hello \"World\""```
   - Single quotes disable escaping entirely:
      ``` echo 'This is a $variable'```

Important Note on Single Quotes ('') :
   - All expansions and escapes (```\```) are disabled.
   - Use double quotes " " when expansion is required.

------------------
 Summary of Key Commands

| Expansion Type | Example | Description |
|-----|----|---|
| Tilde(~) | echo ~ | Expands to home directory (/home/user)|
|Variable($)| echo "${HOME}" | inserts variable value|
|Shell Parameter (${}) |echo "${#HOME}" | Performs string operations|
|Filename Globbing (*) | ls *.txt|Matches filenames using wildcards |
| Command substitution| echo "$(date)"| Inserts command output|
|Word Splitting | touch file1 file2| Splits command based on whitespace|
|Escaping (```\```) |touch my\ file.txt | Escapes special characters|