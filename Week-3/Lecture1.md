## Knowing More About Commands

### ♟ ` which `

```
SYNOPSIS:
    which  <command>
```

* Print the path of ` command ` or check if a package exists or not.
* To print path of commands ` less ` and ` more `

	```terminal
	~$ which less
	/usr/bin/less
	```

	```terminal
	~$ which more
	/usr/bin/more
	```

* Here you got the path of ` less ` and ` more `. Actually the size of ` less ` is ` more `.

* To print the path of command ` which `!

	```terminal
	/etc$ which which
	/usr/bin/which
	```

* ` which ` is kind of reflexive!


### ♟ ` whatis `

```
SYNOPSIS:
    whatis <command>
```

* Print brief description of ` command ` as the first line in ` man ` page
* To print the description of ` which `

    ```terminal
    /etc$ whatis which
    which (1)            - locate a command
    ```

### ♟ ` type `

```
SYNOPSIS:
    type <command>
```


* Prints the type of the command.
* Is it
	- offered by shell?
	- offered by operating system?
	- alias?
* To print the type of commands ` type ` and ` ls `

    ```terminal
    ~$ type type
    type is a shell builtin
    ~$ type ls
    ls is aliased to `ls --color=auto'
    ```
* Note : commands displayed by ` help ` are all shell builtins.

### ♟ ` help `

* It includes keywords, syntax for commands, loops and symbolic expressions.

### ♟ ` info `

```
SYNOPSIS:
    info
    info <command>
```

* ` info ` - Prints documentation for commands.
* ` info <command> ` - Documentation of specific command ` command `.
* It is highly navigatable, just like a webpage.
* Links are marked in * and underline and can be navigated using arrow keys.

| ` keys ` | Description |
| :---:    | ---         |
| ` enter ` | Open a link |
| ` < ` or ` shift + , ` | Go back or previous |
| ` > ` | Go forward or next |
| ` M ` ` m ` | Search menu, similar to seach box |
| ` S ` ` s ` | Regex search |
| ` Q ` `q`| Quit |


## Utilities

### ♟ ` date `

```
SYNOPSIS:
    date [option]... [+FORMAT]

```

* prints the current date and time.
* option ` -R ` : date and time RFC5322 standard format, used in email communications.

    ```terminal
    ~$ date
    Saturday 17 December 2022 01:58:49 PM EET
    ~$ date -R
    Sat, 17 Dec 2022 13:59:05 +0200
    ```

<!-- ### ♟ ` ncal `  and ` cal `

```
SYNOPSIS:
    ncal [month] [year]

```

*  Displays calendar of current month by default.
* Both belong to the same BSD utility ` ncal `, orientation is the only difference.
* ` month ` in long, short text (case-insensitive) or number (1-12, works only when year is specified.) format.
* ` year ` in `YY` or `YYYY` format.
* Display calendar for November, 2022
```terminal
~$ cal nov 2022
   November 2022      
Su Mo Tu We Th Fr Sa  
       1  2  3  4  5  
 6  7  8  9 10 11 12  
13 14 15 16 17 18 19  
20 21 22 23 24 25 26  
27 28 29 30
```
* or
```terminal
~$ ncal nov 2022
    November 2022     
Su     6 13 20 27   
Mo     7 14 21 28   
Tu  1  8 15 22 29   
We  2  9 16 23 30   
Th  3 10 17 24      
Fr  4 11 18 25      
Sa  5 12 19 26
``` -->



### ♟ ` file `

```
SYNOPSIS:
    file <filename>
```

* Prints the type of file.
* Checking file type of ` znew `

    ```terminal
    ~$ file /usr/bin/znew
    /usr/bin/znew: POSIX shell script, ASCII text executable
    ```


### ♟ ` groups `

```
SYNOPSIS:
     groups
```

* Prints the group to which the current user belongs.
* Group with the name of current user is also created for privacy.

    ```terminal
    ~$ groups
    a sudo
    ```

### ♟ ` free `

```
SYNOPSIS:
    free [option]
```

* Displays memory information (memory and swap).
* System utilizes swap memory when it runs out of memory (RAM).
* Swap memory is part of hard disk.
* Option ` -h ` : human readable (typically Gi).

```terminal
~$ free -h
                total        used        free      shared  buff/cache   available
Mem:           1.9Gi       1.5Gi       101Mi       2.0Mi       279Mi       227Mi
Swap:          1.4Gi        50Mi       1.3Gi
```

# The ` echo ` command

```
SYNOPSIS:
  echo <string> 
```

* ` echo ` command is used to print text onto the standard output.

* Print "Hello World!" using ` echo `

```bash
echo "Hello World!"
```

* ` -n ` option to ` echo ` omits the newline.
* ` -e ` option to ` echo ` enables backslash escapes. 


# Combining Commands and Files

* In GNU/Linux OS it is possible to combine multiple commands together a to achieve a task.

## Executing Multiple Commands

* ` command1; command2; command3; `
	- Command execution is independent of the exit status.
		
		```terminal
		~$ ls -d D* ; date; wc -l /etc/profile;
		Desktop  Documents  Downloads
		Saturday 24 December 2022 09:09:25 AM EET
		27 /etc/profile
		```
		
	- If any command fails it will not affect execution of other command.
		+ here ` ls /blah ` fails.
		
		```terminal
		~$ ls /blah ; date; wc -l /etc/profile;
		ls: cannot access '/blah': No such file or directory
		Saturday 24 December 2022 09:11:04 AM EET
		27 /etc/profile
		```
				
* ` command1 && command2 && command3 `
	- ` && ` is logical AND operator. 
	- A command is executed if exit status of previous command is ` true `.
	- ` command2 ` will be executed only if ` command1 ` succeeds.
	- If ` command2 ` succeeds ` command3 ` will be executed.
		
		```terminal
		~$ ls -d D* && date
		Desktop  Documents  Downloads
		Saturday 24 December 2022 09:40:19 AM EET
		```
		
	- If a command fails subsequent commands will not execute.
		
		```terminal
		/$ ls /blah && date
		ls: cannot access '/blah': No such file or directory
		```
		
* ` command1 || command2 || command3 `
	- ` || ` is logical OR operator.
	- A command is executed if exit status of previous command is ` false `
	- If ` command1 ` succeeds, the execution will stop.
		
		```terminal
		~$ ls -d D* || date
		Desktop  Documents  Downloads
		```
		
	- ` command2 ` will be executed if ` command1 ` fails. 
	- ` command3 ` will be executed if ` command2 ` fails.
		
		```terminal
		/$ ls /blah || date
		ls: cannot access '/blah': No such file or directory
		Saturday 24 December 2022 09:46:55 AM EET
		```


* ` && ` and ` || ` operators can be combined together to achieve fairly complex task.		

# File Descriptors

File Descriptors can be used to redirect output to either a file or a command.

The data is stream of characters.

There are 3 standard file descriptors.

* ` stdin `
	- Abbreviation for standard input.
	- Reference Number : ` 0 `
	- By default is pointer to input stream coming from keyboard.

* ` stdout `
	- Abbreviation for standard output.
	- Reference Number : ` 1 `
	- By default refers to screen where the output is displayed.

* ` stderr `
	- Abbreviation for standard error.
	- Reference Number : ` 2 `
	- By default refers to screen the error is displayed.


## Using ` cat ` to Listen ` stdin ` and ` stdout `
* When no option is given, 	
	- ` cat ` reads from ` stdin ` (` 0 `) and writes to the ` stdout ` (` 1 `).
		
	```terminal
	~$ cat
	Hello, how are you?
	Hello, how are you?
	I am fine.
	I am fine.
	Press <ctrl+D> to send EOF and gracefully exit.
	Press <ctrl+D> to send EOF and gracefully exit.
	~$
	```

# Redirection Operators
* ` command > file1 `
	- ` > ` is same as ` 1> `.
	- ` > ` is used to create an empty file or to empty the existing file.
		
		```terminal
		~$ > file.txt
		~$ ls -l file.txt
		-rw-rw-r-- 2 groot groot 0 Dec 24 10:14 file.txt
		```
		
	- ` > ` operator is used to redirect the ` stdout ` of ` command ` to ` file1 `.
	- New file1 will be created if it does not exist.
		
		```terminal
		~$ ls -1 /usr/bin > file1
		~$ ls -l file1
		-rw-rw-r-- 2 groot groot 13354 Dec 24 10:14 file1
		```
		
	- Contents of file1 will be overwritten.
	- Standard error is printed to the screen.
		
		```terminal
		~$ ls -1 /usr/blah > file1
		ls: cannot access '/usr/blah': No such file or directory
		~$ ls -l file1
		-rw-rw-r-- 2 groot groot 0 Dec 24 10:14 file1
		```
		
	- Since, you are creating a file write permission to the directory is required.
		
		```terminal
		/$ ls -1 /usr/bin > file1
		bash: file1: Permission denied
		```
		
	- Storing system hardware information in a file using [` hwinfo `]() command.
		
		```terminal
		~$  hwinfo > hwinfo.txt
		```
	
	- Using ` cat ` we can redirect the ` stdout ` (` 1 `) to write to (overwrite!) a file using ` > `.
		
		```terminal
		~$ cat > file1
		This is the first file I am creating on command line.
		We could use this feature to create text files on command line.
		You can exit using <ctrl+D>
		~$ ls -l file1
		-rw-rw-r-- 2 groot groot 146 Dec 24 11:50 file1
		```
		
	- Run ` cat file1 ` to see the contents of file1.
	
* ` command >> file1 `
	- ` >> ` is same as ` 1>> `.
	- ` >> ` is used to create file if does not exist. If the file exists, it does nothing.
		
		```terminal
		~$ >> file1.txt
		~$ ls -l file1.txt
		-rw-rw-r-- 2 groot groot 0 Dec 24 11:30 file1.txt
		~$ >> file.txt
		-rw-rw-r-- 2 groot groot 0 Dec 24 10:14 file.txt
		```
		
	- ` >> ` is used to *append* the ` stdout ` (` 1 `) of ` command ` to ` file1 `.
		
		```terminal
		~$ date >> file1
		~$ cat file1
		Saturday 24 December 2022 11:39:38 AM EET
		~$ date >> file1
		~$ cat file1
		Saturday 24 December 2022 11:39:38 AM EET
		Saturday 24 December 2022 11:40:45 AM EET
		```
		
	- You can put multiple redirections on same line separated with ` ; `
		
		```terminal
		~$ date >> file2; wc -l /etc/profile >> file2; file /usr/bin/znew >> file2;
		~$ cat file2
		Saturday 24 December 2022 11:44:57 AM EET
		27 /etc/profile
		/usr/bin/znew: POSIX shell script, ASCII text executable
		```

	- ` cat ` to *append* to the file using ` >> `.
		+ Exit using ` <ctrl+D> `
		
		```terminal
		~$ cat >> file3
		Attempt 1 : This is a way to create a new file and append text to it.
		~$ cat >> file3
		Attempt 2 : This is a way to append text to a file.
				We can inspect the content using cat or less command. 
		~$ cat file3
		Attempt 1 : This is a way to create a new file and append text to it.
		Attempt 2 : This is a way to append text to a file.
				We can inspect the content using cat or less command. 
		```
		
		
* ` command 2> file1 `
	- ` 2> ` is used to overwrite the  ` file1 ` with ` stderr ` of ` command `.
	- New ` file1 ` will be created if it does not exist.
	- ` 0 ` and ` 1 ` will have their default behaviour.
		+ ` /blah ` does not exist, hence ` ls ` will generate an error.
		```terminal
		~$ ls /blah 2> error.txt
		~$ cat error.txt
		ls: cannot access '/blash': No such file or directory
		```


* ` command > file1 2> file2 `
	- ` 1> ` or ` > ` redirects ` stdout ` of ` command ` to ` file1 `.
	- ` 2> ` redirects ` stderr ` of ` command ` to ` file2 `.
	- This prevents any output to be on the screen.
	- Contents of ` file1 ` and ` file2 ` will be overwritten.
		```terminal
		~$ ls . /blah > output.txt 2> error.txt
		~$
		```
		+ see the output of both files using ` cat `.
	- Try the following command and see the output in two files created.
		```bash
		ls -R /etc > output.txt 2> error.txt
		```

* ` command < file1 `
	- ` < ` (` 0< `) refers to ` stdin `.
	- Any command expecting input from keyboard can also read input from a file.
	- Using ` < `, ` command ` reads input from ` file1 ` instead of reading the default input stream.
	- All other file descriptors have their default behaviour.
		+ ` wc ` reads from ` file1 `
		+ understand the difference between ` wc <file> ` and ` wc < <file>`
		```terminal
		~$ ls -l file1
		-rw-rw-r-- 2 sanr sanr 236 Dec 25 07:58 file1
		~$ wc file1
			6  43 236 file1
		~$ wc < file1
			6  43 236
		```
	- Using ` < `, read (` cat `) and count lines, words and characters (` wc `) of the files ` output.txt ` and ` error.txt `. 


* ` command > file1 2>&1 `
	- ` stdout ` of  ` command ` is redirected to the file ` file1 `.
	- Then we have another redirection.
		+ ` stderr `, specified by file descriptor ` 2 `, of ` command ` is redirected to ` stdout ` using file descriptor ` 1 `.
	- as a result ` file1 ` contains output and error from ` command `.
	- Contents if any in ` file1 ` will be overwritten. 
	- Note that there should be no space in string ` 2>&1 `
	- Run the commands below and see the output.
	
		```bash
		ls . /blah > file1 2> file1
		cat file1
		```

		+ For commands above, the standard error is first written to file1 then it is overwritten by standard output.
	- Now run the commands given below and see the output.
		```terminal
		ls . /blah > file1 2>&1
		cat file1
		```

		+ file1 contains both standard error and standard output.

<!-- write about custom file descriptors 	-->


## The pipe operator

* ` command1 | command2 `
	- ` | ` is called the pipe operator.
	- This operator redirects the standard output of ` command1 ` to the standard input of ` command2 `
	- If ` command2 ` is expecting any input from keyboard or a file, ` | ` makes possible to take it also from ` command1 `
	- Thus, ` command2 ` processes output from ` command1 ` by taking it as input.
	- By default, standard error from both commands go to the screen.
	- As an example let's count the number of files in ` /usr/bin ` directory.
		+ The following code creates ` file1 ` and then counts.
			```terminal
			~$ ls /usr/bin > file1; wc -l file1
			1353 file1
			```
		+ We can do it more efficiently by using ` | `
			```terminal
			~$ ls /usr/bin | wc -l file1
			1353
			```

	- There is no limit on using pipe operator in terms of numbers.
	- Try the command below and get familiarize with this operator
		+ Read the content of ` /usr/bin ` directly without writing to a file.
			```bash
			ls /usr/bin | less
			```
We can combine the pipe operator with file descriptor redirectors.

* ` command1 | command2 > file1 `
	- The standard output from ` command1 ` is mapped to standard input of ` command2 `. 
	- The standard output of ` command2 ` is written to the file ` file1 `.
	- However, standard error from both commands is written to the screen.
	- Example : Count the number of commands in ` /usr/bin ` directory and store it to a file in one go.
		```terminal
		~$ ls /usr/bin | wc -l > file1
		~$ cat < file1
		1353
		```

What if we don't want to store the error to a file, but instead discard it?
* ` /dev/null ` 
	- It is a character special file.
	- It acts as a sink when any output is redirected to it.
	- Use: silent and clean scripts.
	
* ` command1 > file1 2> /dev/null `
	- The standard output of ` command ` is written to the ` file1 `.
	- The standard error is redirected to ` /dev/null ` using file descriptor ` 2 `, and it just disappears.

	- Let's see an example
		+ The code below prints standard error to the screen.
		```terminal
		~$ ls . /blah > file1
		ls: cannot access '/blah': No such file or directory
		```	
		
		+ We can redirect the standard error to ` /dev/null `.
		```terminal
		~$ ls . /blah > file1 2> /dev/null
		~$ 
		```
		+ Inspect the contents of file1 using ` cat ` command.
		+ Try code below and see the contents of file1.
		
		```bash
		ls -R /etc > file1 2> /dev/null
		```
		
What if we want to redirect the standard output to file and also display to the screen?

## ` tee ` command
* ` tee [-a] file1 `
	- It reads the standard input and writes it to standard output as well as to the file ` file1 `.
	- ` -a ` option is used to append to ` file1 `.
	- It can be used to write to multiple files at a time.
	- Multiple file names can be separated by space.
	- It does not write the error.
* ` command1 | tee file1 ... `
	- It is used to redirect output from ` command1 ` to the screen as well as write it to a file ` file1 `.
	
		```terminal
		~$ ls . | tee file1
		Desktop
		Documents
		Downloads
		file1
		Music
		Pictures
		Public
		snap
		Templates
		Videos
		```
		+ use ` cat ` to see the contents of ` file1 `.
	
	- Writing to multiple files.
		
		```terminal
		~$ ls . /blah | tee file1 file2 | wc -l
		ls: cannot access '/blah': No such file or directory
		10
		```
		+ Try the above command without ` wc -l `
		+ The content of ` file1 ` and ` file2 ` is identical.
		+ This can be inspected using [` diff `](#diff-command) command.
		```
		diff file1 file2
		```
	
	- Handling errors - redirect the output to "sink" for a command that raises error.
		+ here ` ls ` generates error as ` /blah ` file/directory is not found.
		```terminal
		~$ ls . /blah 2> /dev/null | tee file1 file2 | wc -l
		10
		```

