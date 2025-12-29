# Redirecting output into a file

---------------------

- let's say we have a command that generates some output
- How do we store this output in a file ?
- We can do this with the following operator:
```js
>
```

For Example: ```echo 'Bash is amazing' > file.txt```
- if the file does not exist it will be created
- Otherwise the file will be overwritten

To append to a file:
- We can use >> instead of > 
``` echo 'Bash is amazing' >> file.txt```

-------------------------------

# Standard Streams

## By default there are 3 communication channels:

### ⌨️standard input (stdin):0
   - input from the keyboard
### 💻standard output (stdout): 1
   - Normal program output displayed on the screen
### ⚠️Standard error (stderr): 2
   - Error messages displayed on the screen

------------------------------------

# OutPut redirection: > and >> 

## ***stdout***: Standard output
### What happens when we use > or >> ?
   - it changes where this  output goes
   - it now gets redirected into a file
### Example: 
   ```js 
   echo "test" > file.txt
   ```
------------------------------
# Redirecting stdout and stderr

##  So far, we have only redirected stdout (1): 
```js
   du -h IMG_9328.txt > output.txt
```

## However, there's also a more verbose way to do this: 
```js
    du -h IMG_9328.txt 1> output.txt 
```

##  We can use this way to also redirect stderr (2):
```js
    du -h IMG_9328.txt 2> error.txt 
```

## We can also combine those:
```js
   du -h IMG_9328.txt 1> output.txt 2> error.txt
```
----------------------------

# Redirecting all output into the same file

### How do we now redirect all output into the same file ?
- This we know already:
   - We can just redirect both output into the same file
   - But it may only work when appending to the file...
   - ...it may got overwritten otherwise
   ```js du -h file.txt 1>> output.txt 2>> output.txt```

----------

# Multiple redirects
- ⏵ But we can use a trick... 
- ⏵ ... we can just redirect stderr into the already opened file! 

Example : 
```js
du -h file.txt 1> output.txt 2>&1
```
- All output (stdout and also stderr) is redirected into output.txt

```js
du -h file.txt 2>&1 1> output.txt
```
----------------------------

