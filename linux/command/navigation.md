# Navigation

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

