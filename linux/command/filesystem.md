# Work with filesystem

- `mount` - mount file system

- `umount` - unmount file system

	- `/etc/fstab` - file, where is list file systems how it mounts after reboot

|Place|Value                     |Description |
|-----|--------------------------|------------|
|1    |Device                    |Name of device, partition or UUID(ID of file system)|
|2    |Mount point               |Mouint point  |
|3    |Type of fs                | Type of fs|
|4    |Parameters                |Mounting cat be by `only read` `non-exec`|
|5    |Dump frequency            |Can use only if in system installed dump, do dump of fs|
|6    |Orderly on check by `fsck`|Orderly after boot of system, `0` don't chech, `1` only for `/`, and `2`for other all|

- `df` - disk free, print disk usage of system.

- `fdisk` - tool for work with partition table

Before start set partition need unmount.

```
sudo umount /dev/sdb1
sudo fdisk /dev/sdb
```

- `mkfs` - make file system

**Example:**

```
sudo mkfs -t ext4 /dev/sdb1
```

if u want return lasr fs on disk print:

```
sudo mkfs -t vfat /dev/sdb1
```

- `fsck` - check unmountes file system on partition and try reesteblish(восстановить)

- `fdformat` - format floppy disk

- `dd` - data definition(определение данных)write data by blocks in blocked device. Trace data block between devices, cloning device. From `if` to `of`

**Example:**

```
sudo dd if=/dev/sdc of=/dev/sdb

sudo dd if=/dev/sdc of=image.img
``` 

- `blkid` - print info about fs: uuid

```
blkid /dev/sdc2
```
