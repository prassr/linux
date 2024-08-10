# Introduction to Linux

## What is OS?

* OS stands for Operating System.
* It is the software which manages the hardware and software resources of a computer and allows them to work together.

## What is Linux?

* Linux is a free and open-source operating system based on Linux Kernel.
* It is developed by Linus Torvalds in 1991.
* It is used on most of the platforms. Android uses a lite version of Linux kernel.
* Worlds top 500 supercomputers are powered by Linux. It is also widely used in embedded systems.

## What are the features of Linux?

* Linux is Open Source
* It is transparent
* It offers granular control
* Linux is knows for it's stability, security and flexibility.

## What is distribution or "Distro"?

* A distribution (distro) is a version or "flavor" of Linux.
* Linux is highly customizable.
* So,  of Linux are created for different set of users.
* These distributions come with Linux kernel, a set of different softwares and graphical user interface.
* A distribution may be built on top of other distribution
* eg. Linux Mint, Manjaro, Debian, Ubuntu, RedHat, OpenSuse, ParrotOS.

## The Shell

A shell is a command-line interface that interprets user's commands and scripts and help the operating system execute them. The commands we write are high level instructions. But, the operating system does not understand any of these directly. The interpreter converts them to machine level instructions often called assembly instructions which is typically hex code. This hex code is easily interpreted by the operating system, which then executes it with the help of the underlying hardware.

`bash` (Born Again SHell) `zsh` (Z Shell) are the of shells which are widely used. The other shells include `sh` (shell), `csh` (C Shell) and `ksh` (K Shell) and many other.

`bash` is the default shell for most of the distributions.

We will use `bash`.


## The Terminal

We often interact with a computer using graphical user interface. The other way to interact with the OS is using command line interface.

* A terminal, also known as command line interface (CLI), is a text-based interface used to interact with the computer.
* The user can interacts with the operating system using commands, instead of GUI.
* A terminal emulator is a program which provides terminal in a graphical environment.
* Some terminal emulators:
  - GNOME Terminal - Default terminal for GNOME
  - Terminal - Default terminal for macOS
  - GNU Screen - Terminal multiplexer
  - guake - Drop down terminal for GNOME
  - konsole - Default terminal for KDE
  - xfce4-terminal - Default terminal for Xfce
  - xterm - Standard terminal for X11
  - Termux - Terminal emulator for Android

Now with this introduction we are ready to dive in to become `su` (Super User).

Let's sail in the high sea of Linux...

# Files and Directories

In GNU-Linux, everything is represented as files including the IO devices. Hence, it is important to know how to view, navigate and create files or directories using command line interface.

A directory in Linux is equivalent to a folder in Windows

## Viewing the Files and Directories

In graphical environment like Windows, what we see after logging in? A window with icons for apps, files and folders, this is Desktop folder.

But, when we launch a terminal emulator (CLI), we see none of these! :)

The follwing scene takes place when we first launch the terminal.

### Knowing Where We Are

Location is important feature that we all use in our daily lives. It is important in Linux as well. In terminal, most of the times we will be in directories and not on geographical places, unless you name a few directories to begin with. :)

#### ♟ ` pwd `

A simple command used to see in which directory you are is ` pwd `.

```bash
$ pwd
/home/a
```

For each user Linux creates a special directory with the username called ` /home/<username> ` (= ` ~ `) directory called user's home directory. When we launch a terminal, it opens in user's home directory, we will see more about it later. But, as a beginner, this is good to know.

In the output above ` a ` is the username.

The directory where we are is called current or working directory.

` $ ` in the command is called command prompt. It can be any string. It is where you begin typing your commands. It is the indicator of the fact that the computer is awaiting for your command.

Note:

    1) The placeholders are always shown using <some_value>.
    2) [some_text] is used to indicate optional arguments.
    3) Since the output of any command in terminal comes on a new line, the output here is shown just below the command.

Since, we already figured out in which directory we are, it is important to know what files and directories are available in that directory.

Now we will see how to view the files and directories in GNU-Linux.

### Listing the Files and directories

After we know which place we are at, we might want to know what streets are available which will take us to other places, what shops are available where we can buy something. With this analogy it is important to know what are the files and directories available in the working directory.

#### ♟ `ls `

The basic command used to view the files and directories in CLI is ` ls `.

```
SYNOPSIS:
    ls [OPTION] [FILE]
```

You may wonder why I am using `FILE` instead of `DIRECTORY`? A directory is a type of file. As it is already said, in Linux everything is represented as a file.

* Listing the files in current directory.
    
  By default `FILE` is current directory hence, no need to pass it as an argument.
  
  ```bash
  $ ls
  Desktop Documents Downloads Music Pictures Videos
  ```

    * As you can see the result is in the alphabetical order.
    * You can print this in reverse alphabetical order as well. For this you can use the ` -r ` or ` --reverse ` option as shown below.

    ```bash
    ls -r
    ```



* Listing the files in a particular directory.
    
  We will pass the name of the directory as an argument to the ` ls ` command. Let us list the contents of directory `Downloads`

  ```bash
  $ ls Downloads
  ```
    * As there is nothing in this directory, the output is not shown. :)
  
  * List the files along with hidden files.
  
  We use `-a` (`--all`) option to list the hidden files. A hidden filename starts with `.`

  ```bash
  $ ls -a
  .     .bashrc     Documents     Music         .profile
  ..    Desktop     Downloads     Pictures      Videos
  ```

    * Here, ` .bashrc ` and ` .profile ` are hidden files. We will explore more about them later chapters.

    <!-- * ` . ` and ` .. ` are special files. -->
    <!-- remove the below lines and put them into FileSystem Illustration -->

    * ` . ` and `..` are the hidden references for the current directory and the parent directory respectively.
    <!-- * These type of references are often called hard links or symbolic links. Here, these references are hard links. -->
    
* Recursively listing the contents of a directory
    
  In Linux, the files are in organized in hierarchy. So, we might want to know what files and directories within a directory and the directories within it and so on.

    This can be achived with ` -R ` (` --recursive `) option.

    ```
    $ ls -R
    ...
    Pictures:
    tux.jpg
    ```

Note:

    Whenever we have big output, we will truncate it using "...", we will only show a few lines, enough to know what the command is doing.


* Checking the size of the files

  We often want to know the size of the file. This can be checked using the ` -s ` (` --size `) option. It gives the number of blocks the file occupies in the memory. The typical block size is `1 KB` (1024 byte).

  ```bash
  $ ls -s
  total 24
  4 Desktop       4 Downloads     4 Pictures
  4 Documents     4 Music         4 Videos
  ```

    - Here, 4 is the number of blocks. The total number of blocks is shown in the first line of the output which is 24.

  When there will be large files, we might find it difficult to interpret big numbers quickly. We may want to put the numbers in human readable form, like 1K, 1M, 1G.
  
  This can be achieved with ` -h ` (` --human-readable`) option. This option is used with ` -s ` and ` -l ` options where both print number of blocks occupied by the file as the size by default.

  ```bash
  $ ls -sh
  total 24K
  4.0K Desktop       4.0K Downloads     4.0K Pictures
  4.0K Documents     4.0K Music         4.0K Videos
  ```

  * This shows that the representation of directories take 4 KB or 4 blocks in memory.

* Long listing the files
  
  Using `- l ` we can see the details about the file in long listing format.

  ```bash
  $ ls -l
  total 24
  drwxr-xr-x  2 a a  4096 May 23 20:17  Desktop
  ...
  ```

#### Long Listing Format

- ` drwxr-xr-x  2 a a  4096 May 23 20:17  Desktop `
	* ` d ` : file type, ` d ` for directory. [More on file type](#file-types).
	* ` rwxrwxrwx ` : Owner, group and other permissions. [More on permissions](#file-permission-string).
	* ` 2 ` : number of hard links.
	* ` a ` : Owner of the file.
	* ` a ` : Group of the owner.
	* ` 4096 ` : Size of the file in Bytes.
	* ` May 23 20:17 ` : Last modified timestamp for file (considered here as separate columns).
	* ` Desktop ` : file/directory name.
	* ( ` -> /storage/shared/Documents/ ` ) : Optional column for symbolic links.


#### File Types

* ` - ` : Regular file
* ` d ` : Directory / Folder
* ` l ` : Symbolic [link](#type-of-links)
* ` c ` : Character file (e.g. terminal ` tty `)
* ` b ` : Block file (e.g. Hard Disk (` sda `))
* ` s ` : Socket file
* ` p ` : Named pipe

#### File Permission String

* It is a 9 character string, starting after file type.
* Each character is switch to binary digit 0 or 1.
* Order : ` r ` - read (4), ` w ` - write (2), ` x ` - execute (1). Numbers in parenthesis are binary place values in decimal.
* Sum of bit values gives octal representations for permissions specific to user, group or other.
* ` w ` : Permission required to create, modify or delete a file within a directory.
* ` x ` : When set on directories, a user can search or change to them.
* ` - ` : off
* ` ? ` : unknown
* e.g. ` rwxrwx--- ` or `770`
	- Owner permissions, character [1-3] (7)
	- Group permissions, character [4-6] (7)
	- Other permissions, character [7-9] (0)

| characters | octal |
| :---: | :---: |
| ` --- ` | 0 |
| ` --x ` | 1 |
| ` r-- ` | 4 |
| ` r-x ` | 5 |
| ` rw- ` | 6 |
| ` rwx ` | 7 |


## Navigating The Directories

After knowing what streets are available for the places visit from the current location, we might want to go there and explore more.

So far we have seen how to list the contents of a directory, to explore the directory we must visit it just like the places.

#### ♟ ` cd `

` cd ` command is used the **c**hange the **d**irectory. It is used to change the working directory.


```
SYNOPSIS:
    cd [DIR]
```
  
  With `DIR` we are being explit here. The default value of ` DIR ` is the value of the shell variable ` HOME `.


* Changing the working directory
    
    From any directory, the below command will take you to your home directory.

    ```bash
    cd
    ```

    If you want to navigate to ` Downloads `, put it in front of ` cd `.
    
    ```bash
    cd Downloads
    ```
    
    The below command will take you to the previous working directory.
    
    ```bash
    cd -
    ```
      
    - ` - ` represents your old working directory, it is the value taken from shell variable ` OLDPWD `.


## Management of Files and Directories

The most important task we perform on a computer are organizing files in directories by creating new files, modifying the existing files and deleting existing files or directories. For this it is important to learn how to create modify and delete the files.

#### Creating directories

#### ♟ ` mkdir `

A directory can be created using the ` mkdir ` command (**m**a**k**e **dir**ectory).

```bash
SYNOPSIS:
    mkdir [OPTION] [DIR]
```

`DIR` is the name of the directory which you would like to create.

  * Create a directory named `Linux`

    ```bash
    mkdir Linux
    ```
  
  * Create a Directory `Week-1` within `Linux` directory
  
    ```bash
    mkdir Linux/Week-1
    ```
    
  * What if `Linux` directory did not exist?
    
    ` -p ` (` --parents `) option will create parent directories if they don't exist.
    
    ```bash
    mkdir -p Linux/Week-1
    ```

#### Creating Files

We can create files using various commands. The command which is most relevent here is ` touch ` command

#### ♟ ` touch `

This command is used to change the timestamps of the file like access time, modification time to the current time. If the file does not exist it creates an empty file.

```
SYNOPSIS:
    touch [OPTIONS] [FILE]
```

* Create a markdown file named ` notes.md ` in current directory (you can specify your desired path)
    
    ```bash
    touch /home/a/notes.txt
    ```

    * Here I have specified the full path explicitly. See [path specifications](#).


#### ♟ ` > ` and ` >> `
  
  ` > ` and ` >> ` directives are write and append directives respectively. They are used to direct the contents of files or commands to other files or to the new files. But, we can use them to create files.

  ```
  SYNOPSIS:
    [command] >  <filename>
    [command] >> <filename>
  ```

  Here ` command ` is optional

  
  * `>` creates a new file. Deletes content if the file already exists (works in write mode).
  
  ```bash
  > notes.txt
  ```
  
  * `>>` creates a new file. If the file already exists, doesn't do anything (works in append mode).
  
  ```bash
  >> notes.txt
  ```

#### Removing Files and Directories

It is often required to remove unnecessary files. For this we use ` rm ` command.

#### ♟ ` rm `

` rm ` command is used to remove files or directories.

```
SYNOPSIS:
    rm [OPTIONS] ... [FILE] ...
```

  You may specify multiple files after the command.

  * Removing a file

  ```bash
  rm notes.txt
  ```
  
  * Removing a directory

   ` -r ` (` --recursive `) option is used to remove a directory.
  
  ```bash
  rm -r <dirname>
  ```

    * Be careful with this command

  * As a beginner you should run these commands in safe mode. With ` -i ` option, you can prompt for confirmation before removal.

   ```bash
   ~$ rm -ir Linux
   rm: remove directory 'Linux'?
   ```
   * With ` y ` or return key, you will affirm to remove the file, use ` n ` or any other character to cancel the deletion or ` Ctrl+C ` to cancel the operation.  
  
  * Force remove a file.
    
    Use `-f` option to force remove a directory or a file.

#### ♟ ` rmdir `

This command is used to remove empty directory. If the directory is not empty it will throw an error.

More on file management in next chapter

## Wildcards

Wildcards are special characters used as placeholders for a character or a set of characters.

The following are the wildcards:

* ` * ` matches 0 or more characters
* ` ? ` matches a single character.
* ` [chars] ` match one of the characters specified as ` chars `

#### Using wildcards

* With ` ls ` command, ` * ` matches all files and directories, as a result, it prints the contents of the those directories.

  ```bash
  $ ls *
  ...
  Downloads:
  Pictures:
  tux.jpg
  ```

  * This can be interpreted as there is ` Downloads ` directory which is empty, and ` Pictures ` directory which contains file ` tux.jpg `.

* ` ? ` can be used to specify character unknown or minimum number of characters or exact number of characters and can be used along with ` * `.

  ```bash
  ls ????
  ```

  * It lists the files which has exactly 4 characters.

  ```bash
  ls ???*
  ```
  * It matches the files with at least 3 characters.

* ` [chars] ` can be used to match characters specified within the brackets as ` chars `. It can be used with other wildcards.

  ```bash
  ls Do[wc]*
  ```

  * Lists the files that start with ` Do ` and contains ` w ` or ` c` as the third character.

  * What will be the output?

You can use any combination of the wildcards as needed. Now explore how they can be used with other commands.

## Manual Pages

GNU-Linux provides guide or manual pages for the commands.

#### ♟ ` man `

```
SYNOPSIS:
    man [section] [command]
```

This command is used to view manual of the command

* To view the manual of ` ls ` command

   ```bash
   man ls
   ```

#### ` man ` page sections

There are 8 section in the manual. The table below lists the section number and the types of pages they contains.

| Section | Type of pages |
| :-------: | ------------- |
| 1 | Executable programs of shell commands |
| 2 | System calls provided by kernel |
| 3 | Library calls |
| 4 | Special files usually found in ` /dev ` |
| 5 | File formats and conventions |
| 6 | Games |
| 7 | Miscellaneous: macro packages, conventions |
| 8 | System administration commands |
| 9 | Kernel routines |

Explore Yourself:

`who`, `whoami`


