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

- `resize2fs` - file system occupy free space

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

- `wipefs -a` - wipe fs on dev


## LVM

### Create of LV

- `pvcreate` - create physical volume

```
pvcreate /dev/sda
```

	- `pvdisplay` disaplay info about pv

- `vgcreate` - create virtual group 

```
vgcreate < name >  /dev/sda /dev/sdb
```
	`vgdisplay` - display info about virtual group

- `lvcreate` - create logical volume

```
lvcreate < name of vg >  -n < name of lv >  [-L < size > or -l < sice in percent 80%FREE >]
```

Mount in `fstab` use *mapper name* `/dev/mapper/name_of_vg-name_of_lv`

```
ls -l /dev/mapper/name_of_vg-name_of_lv
```


### Extend of LV

1. Create pv new disk

1. Extend virtual group 

```
sudo vgextend < name > /dev/sdd
```	

1. Extend logical volume

```
sudo lvextend < name of group > / < name of logical value > +L < size > [-r Resize file system ]
```

### Snapshot

*Copy on right*

Create snapshot as logical value

```
sudo lvcreate -s (snapshot) -n < name of snap> -L <size of snap> < name of origin lv >
```

### Restore from snapshot

1

### Restore from snapshot

1. Unmount lvm 

2. Convert to snapshot 

```
sudo lvconvert --merg	< name_of_vgroup >/< name_of_lv >
```

## RAID

- `md` - Multiple Device driver aka Linux Software RAID

- `mdadm` - manage md

1. Create mirrors partition on disks

2. Create RAID by `mdadm`

```
sudo mdadm --create < name of RAID > --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
```

3. Save config of our RAID

Become root

Two variant : disks massive or partition massive, command in manual of mdadm 

```
sudo echo 'DEVICE /dev/hd*[0-9] /dev/sd*[0-9]' > /etc/mdadm.conf

mdadm --detail --scan >> mdadm.conf
```

```
echo 'DEVICE /dev/hd[a-z] /dev/sd*[a-z]' > mdadm.conf

mdadm --examine --scan --config=mdadm.conf >> mdadm.conf
```

4. Replace disk, if crash

```
sudo mdadm /dev/md127(name of raid)  --add /dev/sdb1
```
