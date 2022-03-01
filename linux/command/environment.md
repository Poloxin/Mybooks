# Environment

- `set` - print all variable (environment and command shell)

- `printenv` - print variable of environment

- `alias` - print all alias

- `echo $HOME` - print  variable

## Login shell session

Session that ask login pass, read file for start:

|File           |Description                                                                      |
|---------------|---------------------------------------------------------------------------------|
|/etc/profile   |Config script for all users                                                      |
|~/.bash_profile|Private script for extensions value from /etc/profile                            |
|~/.bash_login  |If .bash_profile is missing read file /.bash_login. By default not exist .bash_l.|
|~/.profile     |IF .bash_profile and .bash_login aren't exist, read ~/.profile                   |



## Non-loginsession

Session not ask login and pass, read for start:

|File              |Description                                             |
|------------------|--------------------------------------------------------|
|/etc/bash.bashrc  |Common config script for all users                      |
|~/.bashrc         |Private file                                            |

- `source` - scan file and start changes 
