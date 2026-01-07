# grep

⏵ Grep is a tool that can find a pattern in an output or a file 
⏵ Basic usage: 

``` grep -F 'pattern' [file] ```

⏵ But it can also work on stdin: 

``` [command] | grep -F 'pattern'  ```

⏵ Heads-up:  
   - ⏵ By default, grep uses "basic regular expressions" 
   - ⏵ We can disable them through the parameter: -F

---------------------------

