# CLI command

## Command structure in terminal

command *-command* **arguments**

## Words Note

- ***inode*** - index node(индексный узел)

### Navigation

- `pwd` - print working directory

- `cd` -change directory

	- `cd` - change to home dir

	- `cd -` - change to last dir

	- `cd ~username` - change working dir to home dir of username

- `ls` - list

	- `ls /usr` - list of dir `usr`

	- `ls /home /etc` - list `/home` and `/etc`

	- `-l` - (long) key allow print more info

	- `-t` - (sort by time)

	- `--reverce` - reverce output

	- `-i` - print inode of file

Consider the output structure:

```
-rw-r--r-- 1 root root 3562 2022-03-11 11:04 filename.txt
```

|Place    |Appointment (назначение)| 
|---------|------------------------|
|-rw-r-r--|File permission, and first symbol indicates file type|
|1        |Number of hard link     |
|root     |Name of owner           |
|root     |Name of group that owns the file| 
|3562     |File size in byts       |
|2022-03-11 11:04|Date and time last edit of file|
|filename.txt|Name of file|

### Working with files and directory

- `file` - definition of file types

- `cp` - copy file/dir

	- `-a`,`--archive` - copy with all attributes

	- `-i`,`--interaction` - interactive

	- `-r`,`--recursive` - for copy directory

	- `-u`,`--update` - copy only missing file and update metdata of other file

	- `-v`,`--verbouse` - print process

- `mv` - moving ir rename file/dir

- `rm` - remove file/dir

	- `-f`,`--force` - ignore missed file and not request permission

- `mkdir` - make dir `mkdir dir1 dir2 dir3`

- `ln` - create hard and symbol link `ln -s file link`

	- `-s` - create symbolic link

### Group symbol

- `*` - any sequence (последовательность) of any characters

	- **Example:**

		- `*` - all name file

		- `*g` - all name begin g
		
- `?` - any one character

	- **Example:**

		- `Data???` - name started from 'Data' next three any symbol

- `[characters]` - any one character from  specified range

	- **Example:**

		- `[abc]*` - all name started from symbols: "a", "b", "c"
 
- `[!characters]` - any one character out of specified range

- `[[:class]]` - any one character belonding to thr specified class
### Built-in useful programm

- `less` - programm fo view and read files 
