# LFCS
Preparation for Linux Foundation Certified System Administrator

- [Module 1: Essential Commands](#module-1-essential-commands)
- [Lesson 1: Installing Linux](#lesson-1-installing-linux)
- [Lesson 2: Learning Objectives](#lesson-2-learning-objectives)
- [Lesson 3: Using Essential File Management Tools](#lesson-3-using-essential-file-management-tools)

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

