# Transforming text: sed
 
⏵ The tool sed allows us to easily execute commands on a file or on stdin 

⏵ For example: 
```
sed 'command1; command2; ...'               
```
⏵ Those commands can modify the string, such as: 
   - Deleting lines, inserting lines,... 
   - Most common use case (replacing text): 
      - ⏵ Syntax:  
      ``` s/[pattern]/[replacement]/[flags]  ```

⏵ We usually use the g flag to replace all occurrences, not just the first one in each line 

⏵ To quickly change a misspelled the in a large text:  
   ``` sed 's/teh/the/g' document.txt ```

⏵ Heads-up: 

⚠️ Sed works slightly differently between macOS (FreeBSD sed) and Linux (GNU sed