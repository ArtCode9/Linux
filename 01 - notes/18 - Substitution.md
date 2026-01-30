# Command substitution
We can execute a command and use it's output in another command

### syntax:
``` $(command)```

### Example:
   - Basic Example:
   ```echo "$(cat file.txt)"```
   - Practical Example:
   ```echo 'The size of my home directory is: '"$(du -sh ~)"```
      - shows the size of the home directory
   - Counting files in a directory:
   ``` echo 'There'"'"'re '"$(ls | wc -l)"' files in the current directory'```