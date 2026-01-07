# Sorting data: sort
⏵ If you want to sort the contents of a file and print it to stdout: 

```  sort [file]  ```

⏵ Or we can use it in a pipe: 


```  cat [file] | sort ```

------

# Finding unique entries: uniq

⏵ The uniq command identifies duplicate lines in a file 

⏵ Heads-up: 
   - ⏵ It only works on consecutive duplicate lines 
   - ⏵ We may have to sort the data first 

⏵ Example: 
```
ls | uniq                           
sort /proc/cpuinfo | uniq 
```