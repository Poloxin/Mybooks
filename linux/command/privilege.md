# Privilege

- `uid` - user id

- `gid` - group id

- `id` - info about user

- `/etc/passwd` - file that stores account information

- `/etc/group` - file that stores group information

- `/etc/shadow` - file that stores user's password

#### Where created user, created note in /etc/shadow then created note in /etc/passwd

#### In /etc/passwd defined uid, gid, name, path to home dirand path to loggin shell

## Read, write and execute 

|1.|2. |3. |4. |
|--|---|---|---|
|d |rwx|rw-|r--|

1. Type of file

1. Privilege for owner

1. Privilege for group

1. Privilege for other users

#### Attributes of permission

|Attributes|For files                                                         |For directors                                                   |
|----------|------------------------------------------------------------------|----------------------------------------------------------------|
|`r`       |Open and read file                                                |Allow read only if execute also                                 |
|`w`       |Allow write,rewrite file, if dir haven't w can't rename n delete f|Allow reate, delete and rename files in dir, if execute also    |
|`x`       |Allow execute programm, scrips only if `r`                        |Allow `cd` in dir                                               |

## Command

- `chmod` - change privilege mode, work with symbol and 8 number
