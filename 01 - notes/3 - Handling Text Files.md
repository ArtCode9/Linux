## Handling Text Files

### 1. Introduction to working with Text Files
----
***linux system heavily rely on text files for configuration , logging and data storage*** .
almost every aspect of the system from user settings to system behavior is defined in plain text files , makeing them a crucial part of linux administration.

For example, some common types of text files include:
- log files 
- Configuration
- Data Files
------
### 2. Viewing Files in Terminal

Command: cat <br>
The cat command prints the entire contents of one or more files:
```
cat file.txt
```
Note: Avoid using 
cat
 for large files as it prints the entire content at once.

Viewing Partial File Contents
- Head: View the first lines of a file
```
      head file.txt        #default first 10 lines
      head -n 3 file.txt   #First 3 lines only
```
- Tail: View the last lines of a file
```
      tail file.txt        #Default last 10 lines 
      tail -n 3 file.txt   #last 3 lines only
```
----------------
### Real-Time File Monitoring

use tail -f to monitor changes to log files in real-time:
```
      sudo tail  -f /var/log/syslog
```
- press Ctrl+C to exit
---------------

## 3. Editing Text Files (nano Editor)

linux has several txt editor. **nano** is user-friendly and recommended for beginners:
- Opening files with nano:

```
nano file.txt
```

### Nano basic Command:

| Shortcut | Description |
|-------- |-------------|
| Ctrl + O |  Save (write out) file|
| Ctrl + X | Exit Nano editor |
| Ctrl + F | Search within file |
| Ctrl + K | Cut line |
| Ctrl + U |  Paste line |
| Ctrl + C | Show current cursor position | 

- Saving to a new file: Press 
Ctrl + O 
, enter new filename, then confirm with 
Enter 

---------


## 4. Working with Large Files Efficiently

Checking File Size and Contents (wc)

Use 
wc
 (word count) to analyze file size and contents quickly:
```
      wc file.txt    # Prints lines, words, bytes
```

- specific info: 
    - Lines ->   wc -l file.txt
    - words ->   wc -w file.txt
    - Bytes ->   wc -c file.txt

- Multiple files at once :
```
   wc -l  file1.txt file2.txt
```

### Efficient Navigation with less

The less command is optimized for viewing large files without loading them entirely into memory:

```
         less file.txt
```

Navigation in less : 

| Shortcut | Description |
|-------- |-------------|
| Arrow Keys |  Move line-by-line |
| f | Move forward (page down) |
| b | Move backward (page up) |
| /search_term | Search forward for search_term |
| n/ N |  Move to next/previous search match |
| 50% | Jump to the middle (50%) of file | 
| q | Exit less |

-------------
##  5. Calculating Disk Usage (du)

Check ***disk usage*** with the du command.

- Check file size on disk (allocated space):
```
du file.txt
```
- Check real ("apparent") file size:
```
du -b file.txt
```
- Check folder size (with summary):
```
du -sb directory/
```
- list folder size recursively:
```
du -b directory/
```

Note: Disk space may slightly differ from apparent file size du to file system allocation blocks
----------------------
Appendix : 
###  Searching Inside Files (grep):

Search for text patterns inside files:

```
grep "error" file.txt 
```
Case-insensitive search: 
```
   grep -i "error" file.txt 
```
search recursively in a directory :
```
   grep -r "error" /var/log
```
