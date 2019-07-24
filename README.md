# LFCS
Preparation for Linux Foundation Certified System Administrator

- [Module 1: Essential Commands](#module-1-essential-commands)
- [Lesson 1: Installing Linux](#lesson-1-installing-linux)
- [Lesson 2: Learning Objectives](#lesson-2-learning-objectives)
- [Lesson 3: Using Essential File Management Tools](#lesson-3-using-essential-file-management-tools)
- [Lesson 4: Working With Text Files](#lesson-4-working-with-text-files)

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