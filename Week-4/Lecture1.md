# Process Management

* Helps to switch between tasks while we are in the command line environment.

### ♟ ` ps `

```
SYNAPSIS:
  ps [options]
```

* List the processes by current user.
* Output is unsorted by default.
* It displays 
	1. the process ID (pid=PID)
	2. the terminal associated with the process (tname=TTY)
	3. the cumulated CPU time in [DD-]hh:mm:ss format (time=TIME)
	4. the executable name (ucmd=CMD). 
		- With options, other important columns include.
			1. User id (UID)
			2. Parent process ID (PPID)
	 
```terminal
~$ ps
    PID TTY          TIME CMD
   4172 pts/0    00:00:00 bash
   4567 pts/0    00:00:00 ps
```

| ` command ` | options | Description |
| :--------:| :------:| ------------ | 
| ` ps `      |         | The user’s currently running processes |
| ` ps `      |  ` --forest ` | Pictorial view of which process launched which process |
| ` ps `      | ` -f `  | Full listing of the user’s currently running processes | 
| ` ps `      | ` -e `  | Listing of all processes, except kernel processes | 
| ` ps `      | ` -ef ` | Full listing of all processes, except kernel processes |
| ` ps `      | ` -A `  | All processes, including kernel processes | 
| ` ps `      | ` auxw `| Wide listing sorted by percentage of CPU usage, %CPU |


### ♟ ` sleep `

* Delay for a specified amount (` NUMBER `) of time.

	```bash
	sleep NUMBER
	```

* To ` sleep ` for 10 seconds.

	```terminal
	~$ sleep 10
	```

We will use ` sleep ` a simple process to demonstrate Linux process management.


### ♟ ` & `

*  A process is run in the background.

	```bash
	command &
	```

	```terminal
	~$ sleep 30 &
	[1] 5477
	```
 
* ` [1] ` denotes the command number that is pushed to background. Not to be confused with ` 5477 ` which is ` PID `

### ♟ ` fg `

* Bring a recent process running in the background to the foreground.

	```terminal
	~$ sleep 30 &
	[1]	5510
	~$ fg
	sleep 30
	```

### ♟ ` jobs `

* List the processes running in the background by the user.

	```terminal
	~$ sleep 30 &
	[1] 5583
	~$ jobs
	[1]+  Running                 sleep 30 &
	```

### ♟ ` bg `

```
SYNAPSIS:
  bg
```

* A process running in the foreground can be stopped using the key combination ` CTRL+Z `.
* To rerun the process in the background ` bg ` command can be used.
* From the above examples for the command ` jobs `, you can see a number like ` [number] `, this number can be used to used with `bg`. 

* Rerun the most recently stopped process in the background.

```bash
bg
```

* Rerun the process in the background with a number ` [1] `

```
bg %1
```

### ♟ ` kill `

* Kill a command using it's process id.

	```bash
	kill -9 <process id>
	```

	```terminal
	~$ sleep 200 &
	[1] 5507
	~$ kill -9 5507
	~$
	[1]+	Killed				sleep 200 &
	
	```

### ♟ ` pkill `

pass


### ♟ ` top `

* Prints summary and live snapshots of processes running onto the screen.
* It is in decreasing order of CPU utilization ` %CPU `.
* Use ` q ` key or ` ^C ` to quit, ` ^Z ` to suspend it (move to background).  
* It features ` free `, ` uptime ` and ` ps ` command as a single command.

	```bash
	top
	```

# Disk Usage and System Monitoring

### ♟ [`free`](../Week-3/Lecture1.md#-free)

### ♟ ` uptime `

* It can be used to see the CPU uptime and number of users.

```
uptime
```

### ♟ ` stat `

* ` stat <file> ` - Shows statistics (file or file system status) on ` file `.
* Typical output of ` stat ` for file ` znew `.

```terminal
/usr/bin$ stat znew
  File: znew
  Size: 4577      	Blocks: 10         IO Block: 4608   regular file
Device: 1bh/27d	Inode: 225090      Links: 1
Access: (0755/-rwxr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2022-12-18 15:12:06.475640237 +0200
Modify: 2022-09-05 15:33:59.000000000 +0200
Change: 2022-11-03 19:51:25.078671510 +0200
 Birth: 2022-11-03 19:51:25.014673255 +0200
```

* You can get the atomic output using ` -c ` option using ` FORMAT `.
* For example, get textual and octal permissions on file ` znew `

```
/usr/bin$ stat  -c "%a %A" znew
755 -rwxr-xr-x
```

* To know more visit the ` man ` pages.

### ♟ ` du `

* ` du <file> ` - Estimate file space usage.
* To see the disk usage of ` znew ` file.

```terminal
/usr/bin$ du znew
5       znew
/usr/bin$ du -h znew
5.0K    znew
```

* Try to figure out the difference between output by ` stat ` and ` du `. 

## ` df `

* ` df [-h]` - shows filesystem information in format [human readable] below.

```terminal
    Filesystem   1K-blocks    Used Available Use% Mounted on
```

### Roll of block size

* A block is the smallest unit of memory in terms of which files are stores on the system.
* Typical block size is 1K (1 Kibi byte).
* For example, A file of size 3.5 K will require 4 blocks. 3 blocks for 3 K and 4th block to store 0.5 K. The remaining 0.5 K memory of block will be kept empty.

