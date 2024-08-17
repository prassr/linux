## Filesystem Hierarchy Standard
<!-- add description from linx -->

* ` / ` is the root of the file system.
* ` / ` is also the delimiter for sub-directories.
* ` . ` is current directory.
* ` .. ` is parent directory.
* Path for traversal can be absolute or relative.

- **` / `** : Root directory
  * **` /root `**  : Superuser's home directory
  * **` /home `**  : User specific profiles home directory
    - **` /home/a `** : groot's home directory
  * **` /boot `** : Static files of the boot loader
  * **` /dev `** : Device files (Every device is represented as file.)
  * **` /etc `** : Host specific system configuration.
  * **` /lib `** : Essential shared libraries and kernel modules
  * **` /media `** : Mount points for removable devices
  * **` /mnt `** : Mount points
  * **` /opt `** : Add on application software packages
  * **` /run `** : Data relevant to running processes
  * **` /sbin `** : Essential system binaries
  * **` /srv `** : Data for ftp/http services
  * **` /tmp `** : Temporary files
  * **` /usr `** : Secondary hierarchy
    - **` /usr/bin `** : User commands
    - **` /usr/lib `** : Libraries
    - **` /usr/local `** : Local hierarchy
    - **` /usr/sbin `** : Non-vital system binaries
    - **` /usr/share `** Architecture dependent data
    - **` /usr/include `** Header files included by C programs
    - **` /usr/src `** : Source code
  * **` /var `** : Variable data
    - **` /var/cache `** : Application cache data
    - **` /var/lib `** : Variable state information
    - **` /var/local `** : Variable data for /usr/local
    - **` /var/lock `** : Lock files
    - **` /var/log `** : Log files and directories
    - **` /var/run `** : Data relevant to running processes
    - **` /var/tmp `** : Temporary files preserved between reboots


### Type of Path Specification

There are two types of path specification.

#### 1. Absolute Path

It is a path specification in which the file path always starts with root directory following all the branches in hierarchy till the file name itself (the leaf).

There is exactly one absolute path for a file.

Example:

The absolute path for ` tux.jpg `.

```terminal
/root/home/a/Pictures/tux.jpg
```

#### 2. Relative Path

It is a path specification in which the file path does not start from root directory. The path is specified relative to the current directory.

You can specify relative path in many ways.

Example:

The relative path for ` tux.jpg ` from any sibling directory of ` Pictures `

```terminal
../Pictures/tux.jpg
```

# Files and Directories

## Management of Files and Directories

### Copying the files and directories

Often we need to copy the files from one place to another. For this we use ` cp ` command.

#### ♟ ` cp `

```
SYNOPSIS:
    cp [OPTION] SOURCE DEST
```

You can specify ` SOURCE ` as file or directory, DEST as directory. When the source is directory, destination must be directory. The destination directory must exist.

* Make a copy of a file

 Make a copy of ` hello.py ` as ` greet.py `.

 ```bash
 cp hello.py greet.py
 ```

* Copy a file to an existing directory.
  Here we will copy the file ` hello.py ` into directory ` greetings `

  ```bash
  cp hello.py greetings/
  ```

  * If the ` greetings ` directory does not exist, the command throws error.

  * ` / ` after directory name is indicates that the second argument is a directory. This is to make it explicit.

* Copy a directory to an existing directory.
  
  Using ` -R `, ` -r ` or ` --recursive ` option to ` cp ` command, we can copy contents of a directory to another directory.

  ```bash
  cp -r greetings/ Greet/
  ```
   * A copy of ` greetings ` directory is created inside ` Greet `.
   * It it does not exist then a new directory ` Greet ` is created which will have the contents of ` greetings ` directory.

* Updating the contents while copying
  
  Option ` -u ` (` update `) helps to copy files which are newer than the files in the destination or when the destination file is missing.

  ```bash
  cp -ru greetings/ Greet/
  ```

### Moving and Renaming Files

We should also know how to rename or move files and directories.

#### ♟ ` mv `

```
SYNOPSIS:
    mv [OPTION] SOURCE [DEST|DIRECTORY]
```

` mv ` command is used to rename SOURCE to DEST if destination is not an existing directory or move SOURCE (s) to DEST if it's an existing directory.


* Rename a file or directory if DEST is not an existing directory.

  Rename a file

  ```bash
  mv hello.py greet.py
  ```
  
  * ` hello.py ` is renamed as ` greet.py `.

  Rename a directory

  ```bash
  mv greeting/ Greeting
  ```

* Move a file to existing directory.

  ```bash
  mv greet.py Greet/
  ```
  
  The command above moves the files ` greet.py ` to ` Greet ` directory.


* Move a directory to an existing directory.

  ```bash
  mv Greet Greeting/
  ```

  The example above moves ` Greet ` directory to ` Greeting ` directory.


  If you want to spaces

* Rename ` greet.py ` as ` greetings.py `

You can use spaces in file names, in this case the file name must be enclosed within quotes or the spaces must be escaped.


Note:

* The last argument is the destination.

* Recursion assumed for ` mv ` and not ` cp `

## Managing Permissions

### ♟ ` chmod `

```
SYNOPSIS:
    chmod [option] MODE FILE
    chmod [option] OCTAL-MODE FILE
```

` chmod ` (**ch**ange **mod**e) command is used to change the is used to change the file mode (permission) bits.

The file mode can be changed in above two ways as shown in synopsis.

#### MODE has a format ` [ugoa][[-+=][perms]] `

* ` u ` stands for the user who owns the file.

* ` g ` stands for the group to which the file belongs.

* ` o ` stands for users who do not belong to file's group.

* ` a ` stands for all users.

* ` + ` adds the selected file mode bits using ` perm ` to the existing file mode bits.

* ` - ` cuases them to be removed. If used as ` -[ugoa] `, removes all permissions for ` u `, ` g `, ` o ` or ` a `.

* ` = ` only specified file mode bits are kept, all other bits are removed.

* ` perms ` can be either 0 or more characters from ` rwx `.

Examples:

* Add ` rw ` permissions on file `hello.txt` for all.

 ```terminal
 ~$ chmod a+rw hello.txt
 ```

* Remove ` w ` permission on file ` hello.txt ` for users within group and other users.

 ```terminal
 ~$ chmod go-w hello.txt
 ```

* Remove all permissions on file ` hello.txt ` for others.

 ```terminal
 ~$ chmod -o hello.txt
 ```

You can play with permutation and combination of MODE to get more insights.

The simplest way to change the file permissions is to use numeric mode using 1 to 4 octal digits (0-7) (`OCTAL-MODE` in synopsis).

As we have seen in previous lecture a OCTAL is representation of binary numbers in base 8.

We will see 3 digit representation only. In this case the left most digit (4th digit) is considered 0.

A single digit is derived by adding up the bits with values 4, 2 and 1.

The first digit selects permissions for the user who owns the file: read (4), write (2), execute (1).

The second digit selects permissions for the users in the file's group, with same values.

The third digit selects permissions for the users not in the file's group, with the same values.

Examples:

* Set read (4), write (2) and execute (1) permission for the owner of the file and only read (4), execute (1) permissions for both users in file's group and other users.

    ```bash
    chmod 755 hello.txt
    ```

` x ` permission on directory indicates that it is searchable.


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


## Knowing Files Better

### ♟ ` cat `

```
SYNOPSIS:
     cat <filename>
```

* Dumps the file output on screen for reading.
* Abbr. for concatenate.
* Navigation is difficult.
* To see the ` profile ` file content

    ```terminal
    /etc$ cat profile
    ```

### ♟ ` less `

```
SYNOPSIS:
    less <filename>
```

* open file for reading.
* Possible to ` scroll ` ` up ` or ` down ` through pages.
* To read a log file do
    
    ```terminal
    ~$ less /var/log/alternatives.log
    ```

### ♟ ` more `

```
SYNOPSIS:
    more <filename>
```

* Open file filename for reading page by page.
* It beautifully combines the features of [` less `](#less) and [` cat `](#cat).
* Can not scroll ` down ` to see content.
* Shows percentage of file read.
* To view the ` profile ` file content

    ```terminal
    /etc$ more profile
    ```

### ♟ ` head `

```
SYNOPSIS:
    head [option] <filename>
```


* Print the first 10 lines of the file.
* Can also specify number of lines using ` -n ` option.
* To print first 5 lines.

    ```terminal
    /etc$ head -n 5 profile
    ```

### ♟ ` tail `

```
SYNOPSIS:
    tail [option] <filename>
```

* Print the last 10 lines of the file.
* Can also specify number of lines using ` -n ` option.
* To print last 5 lines.

    ```terminal
    /etc$ tail -n 5 profile
    ```

### ♟ ` wc `

```
SYNOPSIS:
    wc [option] <filename>
```

* Print number of newline, word and byte for each file
* To print the number of newlines (` -l `), words (` w `) and bytes (` -c `) of ` profile `

    ```terminal
    /etc$ wc profile
    27  97 582 profile
    ```

    * the output is in the format `l w c filename`.

* To print newline (` -l `) count of ` profile `

    ```terminal
    /etc$ wc -l profile
    27 profile
    ```


