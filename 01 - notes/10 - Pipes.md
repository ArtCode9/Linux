# Pipes:

## 🚀let's start with simple example
   - hwo can we count the number of files in a directory ?
   - This approach is inefficient and time-consuming
   - ***current approach***<br>
      - ```ls > output.txt```
      - ```wc -l output.txt```
      - ```rm output.txt ```
      - Requires temporary files and involves more steps than necessary

## However with pipes:
   - We can eliminate the temporary file:
      ```ls | wc -l ```

--------

# What is Pipe ? ```|```

A pipe is a mechanism that passes the output of one 
command as input to another command

- Pipes enable chaining command to build complex workflows
- General syntax:
   ``` command | command | ... | command ```

Command -> stdout(1)  ```|``` -> stdin(0) command -> stdout(1)