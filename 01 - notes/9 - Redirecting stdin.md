# Redirecting stdin

can we also redirect a file into stdin?

Some programs also accept user input
for example: <br>
``` wc -l ```

let;s have a look at this in our terminal.

How to we send stdin to a program ?
we can also use redirects!
```wc -l < out.txt ```

However: 
   - most unix tools can work with files directly
   - this command should be preferred:
      ```wc -l out.txt```

-------------------------------