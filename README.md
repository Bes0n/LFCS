# LFCS
Preparation for Linux Foundation Certified System Administrator

- [Module 1: Essential Commands](#module-1-essential-commands)
- [Lesson 1: Installing Linux](#lesson-1-installing-linux)
- [Lesson 2: Learning Objectives](#lesson-2-learning-objectives)
- [Lesson 3: Using Essential File Management Tools](#lesson-3-using-essential-file-management-tools)
- [Lesson 4: Working With Text Files](#lesson-4-working-with-text-files)
- [Lesson 5: Learning Objectives](#lesson-5-learning-objectives)

- [Module 2: User and Group Management and Permissions](#module-2-user-and-group-management-and-permissions)
- [Lesson 6: Managing Users and Groups](#lesson-6-managing-users-and-groups)

## Module 1: Essential Commands

### Lesson 1: Installing Linux
We will use several distributions:
* CentOs
* Ubuntu
* SUSE - OpenSUSE

### Lesson 2: Learning objectives

###### Common linux commands 

* ``` logout ``` or ``` exit ``` - to log off from your current session. 
* ``` whoami ``` - name of logged in user
* ``` hostname ``` - full hostname
* ``` date ``` - current date and time
* ``` uname ``` - information about system
* ``` passwd ``` - change your password 
* ``` touch ``` - creating an empty file 
* ``` last ``` - shows logged users to the system

- Working with ``` man ``` command. 
By using ``` man ``` we will work with following sections:
1. User commands (1)
4. Devices (4)
5. Configuration files (5)
8. Sysadmin commands (8)

Examples:
- ``` man 8 useradd ``` - show information about command from section 8 
- ``` man -a passwd ``` - show information about command from all sections
- ``` man -k ``` - using manual with keyword, when you don't know which command to use 
- ``` appropos user ``` - same results as for ``` man -k ``` command 
- ``` man -k | grep 8 ``` - search for section 8
- ``` sudo mandb ``` - create or update the manual page index caches
- ``` su - ``` - switch for root user

###### Common bash features

- stdin or '<' redirect standard input
- stdout - your console, or redirect output to a file use '>' or '>>' to append
- stderr or 2> - for redirect error
- piping
    * ``` ls | less ``` input of ``` ls ``` filtered by ``` less ```
    * ``` ps aux | grep httpd ```
- ``` find /proc -name "cpu*" 2> /dev/null ``` - find cpu in /proc directory and send error output to the null device
- ``` history ``` - command line history, to use command from history simple write commands number from history ``` !28 ```
    * history stored in *.bash_history*, you can find this file by typing ``` ls -a ``` - where *-a* means to show hidden files. 

###### Using bash shell scripts
* ``` echo who > myscript ``` - create and add line to the file
* ``` echo ls >> myscript ``` - append to the file
* ``` chmod +x myscript ``` - make your script executable
* ``` ./myscript ``` - run your script 

###### Lab answers 
* ``` uname -r ``` - get kernel version
* ``` hostnamectl set-hostname ``` - change hostname 
* ``` nmtui-hostname ``` - change hostname from gui on CentOS
* ``` lvcreate --help ``` - all options in [] brackets are optional, all options in {} brackets are mandatory, must be used 

### Lesson 3: Using Essential File Management Tools
###### 3.1 Understanding the Linux File System Hierarchy

Hierarchy:
* / - root directory
    * /boot - files need to start your computer's OS
    * /home - loc of user home directories
    * /usr - operating system files 
    * /var - diverse information (log, cache)

* mount - connection between directory and device
    * ``` /dev/sdb1 ``` - 
        * /dev is device directory, 
        * sd - scsi disk
        * b - second scsi disk 
        * 1 - number of partition.

By using command ``` mount ``` we can mount different disks to the different directories.
Directories in linux defined by *FHS* - Filesystem Hierarchy Standards 

![img](https://github.com/Bes0n/LFCS/blob/master/images/img1.JPG)

###### 3.2 Listing files with ls command
- ``` ls -l ``` - long list of items
- ``` ls -a ``` - shows hidden items
- ``` ls -il ``` - shows inode number too
- ``` ls -lrt ``` - list items by last time modified
- ``` ls -l /etc ``` - get content of /etc directory
- ``` ls -R ``` - list entire directory structure (recursive)
- ``` ls -ld /etc ``` - get information of /etc directory directly

###### 3.3 Using Shell Wildcards
Three types of globbing:
- '*' - ``` ls a* ``` - will list all files starting with 'a' character. With any length
- ? - ``` ls ca? ``` - will list files which have 'ca' in the beginning and with last character, for instance 'cat' or 'car'
- [a-b] - ``` ls ca[bt] ``` or ``` ls ca[b-t] ``` - first will list with 'ca' and 'b' or 't', second will list 'ca' and starting from 'b' to 't'
Example: ``` ls [a-d]??* ``` - list word starting with 'a' to 'd', have '??' at least two characters and '*' any amount of characters in the end

###### 3.4 Copying files with cp
- ``` cp /etc/hosts . ``` - copy hosts files in home directory
- ``` cp -R /tmp . ``` - copy entire subdirectoy structure in home directory
- ``` cp /etc/hosts ~/data/ ``` - copy hosts file in home/data directory. Don't forget to put slash behind the directory

###### 3.5 Working with Directories
- ``` cd /tmp ``` - change directory
- ``` pwd ``` - print working directory
- ``` mkdir data ``` - create subdirectory data
- ``` mkdir -p files/pete ``` - create directory files with pete directory entire using '-p' - path option
- ``` rmdir videos/ ``` - remove empty directory
- ``` rm -rf ``` - remove directory forcely. Even if directory has a files in it. 

###### 3.6 Using Absolute and Relative Paths
Absolute path can be:
- ``` /tmp/data/files/pete ```
Relative path can be:
- ``` /files/photos/2017 ``` - no need to change directory from 'tmp' 
- ``` cd .. ``` - go to previous directory
- ``` cd ../.. ``` - go to two levels up on directory

We can copy items by using relative path: 
![img](https://github.com/Bes0n/LFCS/blob/master/images/img2.JPG)

- ``` tree /tmp/data ``` - get structure of the directory
- ``` cp hosts /tmp/data/photos/2016/ ``` - copy hosts to '2016' directory using **absolute** path
- ``` cp hosts ../../photos/2017/newfiles ``` - copy hosts to '2017' directory using **relative** path

###### 3.7 Moving Files with mv
``` mv /tmp/testfile ~ ``` - move file 'testfile' to your home directory
``` mv testfile anotherfile ``` - rename file 

###### 3.8 Removing Files with rm
``` rm anotherfile ``` - remove anotherfile
``` rm -r ``` - recursive removal 
``` rm -rf etc ``` - remove directory without prompt 
``` rm -rf / ``` - remove everything on your system (dangerous command)
``` rm -- -myfile ``` - remove files with dashes on the beginning

###### 3.9 Understanging Hard and Symbolic Links (soft links)
* Links
    * hard
    * symbolic

Hard Links:
- You can have several names to refer on one inode
- Must be stored on the same device
- Can't be linked to the directories

Symbolic Links:
- Refers to the name
- Become invalid if the name removed
- More flexible than hard link
- Can exist on different devices

![img](https://github.com/Bes0n/LFCS/blob/master/images/img3.JPG)

###### 3.10 Managing Hard and Symbolic Links
- ``` ln /etc/hosts myhosts ``` - create hard link
- ``` ls -l /etc/hosts myhosts ``` - directories will be in the same size
- ``` ls -il /etc/hosts myhosts ``` - list with inodes number
- ``` ls -s myhosts symhosts ``` - create symbolic link from hard link

symhosts symbolic link refers to the myhosts hard link:
![img](https://github.com/Bes0n/LFCS/blob/master/images/img4.JPG)

- ``` ln -s etc /etc ``` - create symbolic link to directory '/etc'

###### 3.11 Finding Files with find
- ``` find /etc -name hosts ``` - start searching in '/etc' directory and look for file with name 'hosts'
- ``` find /etc -name "*hosts*" ``` - look for file which contain 'hosts' name in it. But use double quotes
- ``` find / -user "student" ``` - find files which belong to 'student' user 

###### 3.12 Using Advanced find options
- ``` find /etc -name "*hosts*" -exec cp {} find/names \;``` - find all files in '/etc' with name *hosts* and cp all output from find to the directory 'find/names'. '\;' - must be used to exit from exec interpretor. 
- ``` find /etc -size +100k -exec cp {} find/size \; ``` - look for files more than 100 kilobytes and copy them into the directory 'find/size'
- ``` grep student /etc/* 2>/dev/null ``` - grep will look for files, which contains 'student' word inside
- ``` find /etc -exec grep -l student {} \; 2>dev/null ``` - find files through grep which contains 'student' word inside 
- ``` find /etc -exec grep -l student {} \; -exec cp {} find/contents/ \; 2>/dev/null ``` - cp all found files in 'find/contents/' directory and avoid any error messages. 


### Lesson 4: Working With Text Files
###### 4.1 Understanding How to work with vim

**vi** works on two modes:
* command mode
* input mode

We can switch from **command mode** to **input mode** by using:
- ``` i ``` 
- ``` o ``` - opening new line
- ``` O ``` - opening new line above the current position 
- ``` [Ins] ``` - same as ``` i ```
- ``` a ``` - append to the current cursor position 

We can switch from **input mode** to **command mode** by using:
- ``` ESC ```
- ``` ZZ ```
- ``` :wq ```

Copy and paste:
* ``` v :visual ```
* ``` d :delete ```
* ``` y :yank ```
* ``` p :paste ```

Undo: 
* ``` u :undo ```
* ``` Ctrl + R ``` - redo 

- ``` g ``` - top of the document
- ``` G ``` - bottom of the document 
- ``` /text ``` - search for text
- ``` n, N ``` - switch for next inside of search 
- ``` :300 ``` - go to line 300 
- ``` dd, x ``` - delete line 

###### 4.2 Creating text files with vim
- ``` :%s/one/ONE/g ``` - substitute *one* with *ONE*, **g** - means global. For all occurences. 


###### 4.3 Browsing text files with less
- ``` less /var/log/messages ``` - less based on the vim 
- ``` /root ``` - search for *root* word in less mode
- ``` n, N ``` - for next item
- ``` g, G ``` - for top and bottom of the document

###### 4.4 Displaying Text File Contents with cat and tac
- ``` cat myfile ``` - content of the file from first line last
- ``` tac myfile ``` - content of the file from last line first

###### 4.5 Using head and tail to see File Start and End 
- ``` head -n 10 /etc/passwd ``` - get first 10 lines of the files
- ``` tail -n 10 /etc/passwd ``` - get last 10 lines of the files
- ``` head -n 4 /etc/passwd | tail -n 1 ``` - get line 4 by using pipeline 
- ``` tail -f /var/log/messages ``` - *-f* automatically shows information once it's written

###### 4.6 Working with grep (generic regular expression parser)
- ``` grep -ilR student /etc 2>/dev/null ``` - find files which contain *student* word, **-i** insensitive, **-l** means show file name, **-R** means recursive, **2>/dev/null** - avoid any error messages.  
- ``` ps aux | grep cron ``` - search inside of processes for process name *cron*
- ``` ps aux | grep cron | grep -v grep ``` - inside of search don't show me *grep* output 

###### 4.7 Understanding Regular Expressions 
* Regular expressions are text patterns that are used by tools like grep and others
* Don't confuse regular expressions with globing
* ``` grep 'a*' ``` - put your regular expressions in single quotes
* grep, vim, awk, sed - tools which use regular expressions

![img](https://github.com/Bes0n/LFCS/blob/master/images/img5.JPG)

###### 4.8 Using Regular Expressions with grep
- ``` grep '^abc' grepfile1 ``` - get words starting with 'abc'
- ``` grep 'abc$' grepfile1 ``` - get words end with 'abc'
- ``` grep 'a.c' grepfile1 ```  - matching 'abc', 'a2c', 'aac', 'abc123'
- ``` man -k user | egrep '1|8' ``` - get extended grep for user manual with pattern 1 or 8
- ``` egrep 'ab{2}c' grepfile1 ``` - output will be 'abbc', 2 preceeding characters
- ``` grep 'a[bB]c' grepfile1 ``` - we can get 'abc' or 'aBc' or '123abc'
- ``` egrep '(123{3})' grepfile1 ``` - get group of items three times, output - '123123123' 
- ``` grep 'ab*c' grepfile1 ``` - no or more items between 'ab' and 'c', output can be - 'ac', 'abc', 'abbc', 'abbbbbc'
- ``` egrep 'ab+c' grepfile1 ``` - more items between 'ab' and 'c', output can be - 'abc', 'abbc', 'abbbbbc'
- ``` egrep 'ab?c' grepfile1 ``` - null or one preceeding character, can be - 'aac', 'ac', 'abc'

###### 4.9 Using Common Text Processing Utilities
- ``` cut -d : -f 3 /etc/passwd | sort -n ``` - filter out text from */etc/passwd* by using delimeter *:*, *-f 3* - is a third field. Sort by numbers use '-n'
- ``` cut -d : -f 1 /etc/passwd | sort ``` - filter out text from */etc/passwd* by using delimeter *:*, *-f 1* - is a first field. Sort by characters'
- ``` cut -d : -f 1 /etc/passwd | sort | tr [:lower:] [:upper:] ``` - translate output from lower to uppercase
- ``` echo hello | tr [a-z] [A-Z]``` - translate output from lower to uppercase
- ``` awk -F : '{print $1}' /etc/passwd ``` - same as *cut* but more powerful 
- ``` sed -i -e  '10d' grepfile1 ``` - streamline editor, *-i* interactor, *-e* edit. We removed line 10 from grepfile1

###### Lab Solutions
- ``` head -n 5 /etc/passwd | tail -n 1 ```
- ``` sed -n '5p' /etc/passwd ``` 
- ``` ps aux | awk '{print $1}' ```
- ``` grep '^root' /etc/* 2>/dev/null ```
- ``` grep '^...$' /etc/* 2>/dev/null ``` 
- ``` grep alex * | grep -v alexander  ```  

### Lesson 5: Learning Objectives
###### 5.1 Working as Root or a Local User
- ``` su - ``` - log on as root
- ``` sudo su - ``` or ``` sudo -i ``` - log on as root on ubuntu

###### 5.2 Using su to Perform Administration Tasks
- ``` su - username ``` - perform log on as regular user 'username'

###### 5.3 Using sudo to Perform Administration Task
- ``` sudo -i ``` - will get error that user is not in the sudoers file
- ``` id student ``` - get id of the user. uid, gid and groups
- ``` usermod -aG wheel student ``` - add 'student' user in 'wheel' group to perform sudo tests
- ``` visudo ``` - open configuration of sudo file 
- *Note: after adding your user in sudoers, you have to log off and log on, so your changes can be applied*

###### 5.4 Creating a simple sudo configuration
Access for specific users managed by **visudo** command. 
- ``` sudo passwd linda ``` - set up password for user
- ``` su - linda ``` - open linda shell 
- ``` linda ALL=/sbin/useradd ``` - provide access to linda user on ALL hosts to execute command *useradd* in visudo file

###### 5.5 Working on Linux from Graphical or Command Line Mode
- ``` w ``` - get information about active terminals
- ``` chvt ``` - switch to virtual terminal
- ``` chvt 7 ``` - switch back to graphical interface
- ``` pts/0 ``` - information about user logged through ssh session

###### 5.6 Connecting Remotely to Linux
- ``` sshd ``` - shell daemon
- ``` telnetd ``` - insecure and should not be used anymore
- ``` PuTTy ``` - remote ssh client for windows, nowadays powershell can be used
- ```  VNC ``` - remote desktop client for Linux 
- ``` ssh student@192.168.4.240 ``` - connect to linux remote machine with student user

###### 5.7 Understanding the Use of etc securetty
- ``` vim /etc/securetty ``` - list of secure TTY's. Here you can include or exclude list of terminals. 


## Module 2: User and Group Management and Permissions
### Lesson 6: Managing Users and Groups
###### 6.2 Understanding the Role of Ownership
Users as groups can have access to resources, files, directories e.t.c
- ``` id ``` - get information about users
- ``` id linda ``` - information about linda user 
- ``` gid=1000(student) ``` - means that primary group for student user is **student** group

###### 6.3 Creating Users with useradd and adduser
- ``` useradd -D ``` - create user by using default options
- ``` useradd -s /bin/zsh -c "my user" -m anna ``` - create user on CentOs
- ``` adduser kate ``` - you will be promted for all requrired information on Ubuntu 

###### 6.4 Creating Groups with groupadd
- ``` groupadd sales ``` - create group **sales**
- ``` usermod -aG sales anna ``` - add user to the group **sales**, where **-a** means append to the group

###### 6.5 Managing User and Group Properties
- ``` usermod -L anna  ``` - lock the user
- ``` useromd -U annd ``` - unlock the user
- ``` userdel -r ``` - remove user, it's home directory and mail spool
- ``` groupdel ``` - remove group
- ``` groupmod ``` - modify properties of the existing group 

###### 6.6 Configuring Defaults for Creating Users
We have */etc/default* directory, where *useradd* file can be modified. That one refers to the *useradd -D* option. Default user properties. 

- ``` /etc/login.defs ``` - mail spool location, password expire days, length, age. UID and GID information. 
- ``` /etc/skel/ ``` - items inside of skel directory will be copied to the home directory of newle created user
