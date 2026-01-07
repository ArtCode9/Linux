# Commonly used tool: tee

⏵ We can combine a pipe and the tee program 
⏵ This allows us to write to a file... and output to stdout! 

```echo 'Hello World!' | tee hello.txt```

⏵ To append:  

```  echo 'Hello World!' | tee -a hello.txt  ```   
