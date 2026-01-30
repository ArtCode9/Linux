# Escaping
⏵ Sometimes we want to disable Bash from performing the default actions 

⏵ Example: 

⏵ We autocomplete a filename that contains a whitespace character 

⏵ Bash might autocomplete it to: 

``` echo a\ file.txt```

⏵ But how does the backslash work? 

⏵ The backslash disables the normal behaviour of the next character 

⏵ Here: Prevents word splitting 


⏵ You can also use it to output a double quote: 
``` echo "\"" ```

⏵ But this would still be simpler: 
```echo '"'```

## Escaping and single quotes
⏵ Heads-up: 

⏵ In Bash, single quotes disable all expansions, and also all escapes 

 You cannot use a backslash to escape a single quote inside single 
quotes! 

⏵ Thus, this one does not print a single single quote: 
```echo '\''```

⏵ Instead, this command is not yet finished - as the last single quote has not been terminated yet
