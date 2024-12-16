### Level 0
In this level, you just have to login into the system with ssh command. use ```ssh banditlab.overthewire.org -p 2220 -l bandit0``` to login into the system. Nothing special here, -p is for port name, -l is for username.

### Level 1
The password is in readme file in home directory. Simply user ```cat readme``` command to get the password.

### Level 2
The password is in file named -. We cannot simply do ```cat -``` here because if using - after a command then the UNIX system will think that we are about pass an option to the command. To get the password we have to use `cat ./-` instead. Here we are specifying the full path of the file. 

### Level 3
The password is in a file named called spaces in this filename. To deal with spaces in CLI, simply wrap the name in double or single quotes. So the solution is `cat 'spaces in this filename'` 

### Level 4
The password in in a directory named inhere. the file is hidden so we have to first list the hidden file with `ls -a` and then `cat .hidden`

### Level 5
The password in in a file inside inhere directory. First list all the content of the directory with additional information using `ls -la` command. The l flag provides additional information:
1. The first character displays the type of file. 
	 - - normal file
	 - d directory
	 - l link file
	 - The next 9 chars specifies the permissions. Each group of 3 chars corresponds to permissions. The first 3 lines stands for user permissions, next 3 for group and last 3 for other permissions. Here r means read, w mean write and x means execute permission. 
2. Second field specifies the number of links for that file.
3. Third field specifies owner of the file. 
4. Fourth field specifies the group of the file. 
5. Fifth field specifies the size of file (in bytes)
6. Sixth field specifies the last modified date and time of the file.
7. Seventh field specifies the name of the file/directory itself. 
In this case, all the files have similar property so we'd have to cat each files to check for human readable text. The password is in -file07 file so we have to do `cat ./file07` 
However, this is not very optimal solution when dealing with many files. The optimal solution is however to use file command which gives the type of the file. Moreover, we have to list the type of file for all files so we use file wild card so the command is `file ./*` we could have just use `file *` but here in this case, the file names start with - so it will give problem as discussed in [[#Level 2]]. After running the command, we can see that all the files are of type data except for -file07 which is of type ASCII text which is human readable so the password is in that file. 
### Level 6
In this level we have to look for a file that is 1033 byes in size, is human-readable and not executable. For this we have to use the find command along with grep command. File command accepts options such as:
- -size: accepts size in bytes
- -type f: avoid looking for directories
- -readable: Looks for file with readable permission (not actually human readable)
- - executable: Looks for executable files. ! -executable excludes executable files from search.
-  -exec with '{}' as a path: meaning the chosen command will be executed on all the files. This could be used to execute another command like file.
Similarly, the grep command is used to filter the result obtained from the file command. For this we use pipe |. It accepts -V flag to do the opposite i.e. exclude the result matching the pattern. 

So the one line solution for this level is: 
```bash
find . -type f -size 1033c ! -executable -exec file '{}' \; | grep ASCII
```
