# Extracting data: cut
⏵ The program cut allows us to process and extract data from a file or standard input  


⏵ We can use it for different modes: 

⏵ Cutting by bytes (-b): 


   -  ``` uptime | cut -b 1-10  ```

   - ⏵ Here, we select the bytes 1-10 from each line of the input 


⏵ Cutting by characters: 


   -  ``` uptime | cut -c 1-10 ```


   - ⏵ It otherwise works exactly as we would cut by bytes   

⏵ Cutting by fields: 

```
   cut -d ' ' -f 1                 
   uptime | cut -d ' ' -f 1        
```

⏵ And we select the first item 
⏵ In case the output starts with a whitespace character...  
⏵ ... then you would need to use -f 2
