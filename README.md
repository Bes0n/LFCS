# LFCS
Preparation for Linux Foundation Certified System Administrator

- [Module 1: Essential Commands](#module-1-essential-commands)
    - [Lesson 1: Installing Linux](#lesson-1-installing-linux)
    - [Lesson 2: Using Essential Tools](#lesson-2-using-essential-tools)
    - [Lesson 3: Using Essential File Management Tools](#lesson-3-using-essential-file-management-tools)
    - [Lesson 4: Working With Text Files](#lesson-4-working-with-text-files)
    - [Lesson 5: Connecting to a Server](#lesson-5-connecting-to-a-server)
- [Module 2: User and Group Management and Permissions](#module-2-user-and-group-management-and-permissions)
    - [Lesson 6: Managing Users and Groups](#lesson-6-managing-users-and-groups)
    - [Lesson 7: Managing Linux Permissions and Quota](#lesson-7-managing-linux-permissions-and-quota)
- [Module 3: Networking](#module-3-networking)
    - [Lesson 8: Configuring Networking](#lesson-8-configuring-networking)
    - [Lesson 9: Configuring the SSH Service](#lesson-9-configuring-the-ssh-service)
    - [Lesson 10: Configuring a Firewall](#lesson-10-configuring-a-firewall)
    - [Lesson 11: Configuring Time Services](#lesson-11-configuring-time-services)
- [Module 4: Operating Running Systems](#module-4-operating-running-systems)
    - [Lesson 12: Process Management](#lesson-12-process-management)
    - [Lesson 13: Managing Software Packages](#lesson-13-managing-software-packages)
    - [Lesson 14: Scheduling Tasks](#lesson-14-scheduling-tasks)


## Module 1: Essential Commands

### Lesson 1: Installing Linux
We will use several distributions:
* CentOs
* Ubuntu
* SUSE - OpenSUSE

### Lesson 2: Using Essential Tools

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
- ``` cd ``` - move to your home directory
- ``` cd ../.. ``` - go to two levels down on directory

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
- ``` find /etc -name "*hosts*" -exec cp {} find/names \;``` - find all files in '/etc' with name *hosts* and cp all output from find to the directory 'find/names'. '\;' - must be used to exit from exec interpretor. Where **{}** means output of **find** command
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

### Lesson 5: Connecting to a Server
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

###### 6.7 Managing Password Properties
- ``` passwd --help ``` - settings for passwd command
- ``` echo password | passwd --stdin brenda ``` - update password for brenda user. Can be scripted. 
- ``` chage brenda ``` - change age of the password for brenda user

###### 6.8 Understanding User Configuration Files
- ``` /etc/passwd ``` and ``` /etc/shadow ``` - information stored about users in these folders
- ``` vipw ``` - vi for passwd, modify contents of /etc/passwd directly

###### 6.9 Understanding Group Configuration Files
- ``` /etc/group ``` - group configuration files. Primary groups don't have members because they declared already in */etc/passwd* as primary group. We can manage members here of secondary groups. 

###### 6.10 Understanding Login on External Authentication Sources
Setting up remote authentication can be difficult. Can be done on **Active Directory** or **LDAP** 

###### 6.11 Configuring Login on External Authentication Sources
First of all we need to install proper software

- ``` yum groups install "Directory Client" ``` - software required for external authentication 
- ``` authconfig ``` or ``` authconfig-gtk ``` - gtk is graphic utility. To run gui verion *authconfig-gtk*

![img](https://github.com/Bes0n/LFCS/blob/master/images/img6.JPG)

###### 6.12 Configuring Resource Access Restrictions
- ``` cd /etc/security ``` then ``` vim limits.conf ``` - here we can configure limits of resources provided to the users.

![img](https://github.com/Bes0n/LFCS/blob/master/images/img7.JPG)

As you can see from image here we can configure number of maximum processes, maxlogins, cores usage and so on.

### Lesson 7: Managing Linux Permissions and Quota
###### 7.1 Understanding Basic Linux Permissions
- Basic Permissions (file or directory):
    * Read **(4)** - you can read file or list items in that directory
    * Write **(2)** - modify contents of the file, create or delete files inside of directory
    * Execute **(1)**  - you can run the file. You need read permission to execute the script. To access directory to use *cd* we need execute permission. 

- Ownership:
    * Users
    * Group
    * Others

- ``` chmod 760 file ``` - where **7** - permission for user, **6** - permission for group, **0** - permission for others.

As we understand number **7** is a sum of **4**(read) + **2**(write)+ **1**(execute). So **7** is a full permission. So user will have full access permission. 

**6** means that group will have **4**(read) and **2**(write) permissions

**0** menas that others will don't have any permissions for that file 

###### 7.2 Managing Basic Linux Permissions
- ``` chgrp  sales mydirectory ``` - make group **sales** as an owner of **mydirectory** directory
- ``` chown anna mydirectory ``` - make user **anna** as an owner of **mydirectory** directory
- ``` chown linda:sales mydirectory ``` or ```chown linda.sales mydirectory```  - make **linda** user and **sales** group as an owner of **mydirectory** directory in one command 
- ``` chmod g+w account ``` - add write group permission to account directory
- ``` chmod o-rx account ``` - remove read and execute permissions from account directory for others

###### 7.3 Understanding Advanced Linux Permissions
Advanced permissions:
- **suid** (4) - set user id. Run file as owner. Dangerous permission.
- **sgid** (2) - set group id. Run as group owner. Also dangerous permission. Inherit directory group owner. 
- **sticky** (1) - sticky bit. Has no meaning on files. Delete if only owner for directory. 


###### 7.4 Managing Advanced Linux Permissions
- ``` chmod u+s playme ``` - set permissions as represantive to file. 
- ``` /bin/passwd ``` - using same permissions set by **suid**

- ``` chmod g+s * ``` - set group id for directory to use shared directory. Group ownership will be set from parent directory. 
- ``` chmod +t * ``` - add sticky bit to the files. File can't be removed by other users if sticky bit applied inside of shared directory. 

###### 7.5 Understanding Access Control Lists
Two types of ACL:
* normal - take care of files that already exists 
* default - take care of files that will be created

- ```setfacl -R -m g:sales:rx file``` - set **-m** modify access list **-R** recursively to **file** for group **sales** with **rx** read-execute permissions
- ```setfacl -R -m d:g:sales:rx file``` - **d** column added for default ACL

To use ACL we need filesystem acl. Without this option we couldn't use ACL

###### 7.6 Managing Access Control Lists
- ```setfacl -R -m g:sales:rx account``` - group **sales** need read and execute for **account** directory
- ```getfacl account/``` - get information about access list

```
# file: mydirectory/
# owner: root
# group: sales
user::rwx
group::rwx
group:sales:r-x
mask::rwx
other::---
```

- ```setfacl -m d:g:sales:rx account``` - default actions, which will be applied to any items created in **mydirectory**

```
# file: mydirectory/
# owner: root
# group: sales
user::rwx
group::rwx
group:sales:r-x
mask::rwx
other::---
default:user::rwx
default:group::rwx
default:group:sales:r-x
default:mask::rwx
default:other::---
```


###### 7.7 Understanding Extended Attributes
Extended Attributes - properties of files only. 
Commands: 
* chattr
* lsattr 

###### 7.8 Managing Extended Attributes
- ```chattr +i file1``` - add immutable attribute to the **file1**
- ```lsattr file1``` - get information about attribute. 
```
[root@centos mydirectory]# lsattr file1 
----i----------- file1
```

We can't do anything to the immutable file. 
```
[root@centos mydirectory]# echo hello >> file1
-bash: file1: Permission denied
[root@centos mydirectory]# rm -f file1 
rm: cannot remove ‘file1’: Operation not permitted
```

Except: 
- ``` chattr -i file1 ``` - remove immutable attribute from the **file1**

###### 7.9 Understanding Linux File System Quota
Put limitation to the user for using disk space. 

###### 7.10 Managing Quota on Ext File Systems
- ```yum install -y quota``` - install required software
- ```vim /etc/fstab``` - mounting systems quota automatically
- ```chmod -R 777 /quota``` - full access for /quota directory
- ``` mount -o remount quota ``` - to be sure that file system mounted with the right option. 
- ``` quotacheck -mavug ``` - running quotacheck. 
- ```quota -vu lisa``` - checking what is user **lisa** using 
- ``` repquota -aug ``` - get information about quota limits for users

###### 7.11 Managing Quota on XFS File Systems
- ``` xfs_quota --help ``` or ```man xfs_quota```

###### 7.12 Finding Files with Specific Permissions
- ```man find``` - look for **perm**
- ```find . -perm 0600 -exec ls -l {} \; ``` - find files in /etc with special permissions and list items. 
- ``` find . -perm /4000 -exec ls -l {} \; ``` - items which have set user id permission mode. 

## Module 3: Networking
### Lesson 8: Configuring Networking
###### 8.1 Summarizing IPv4 Basics
![img](https://github.com/Bes0n/LFCS/blob/master/images/img8.JPG)

###### 8.2 Summarizing IPv6 Basics
![img](https://github.com/Bes0n/LFCS/blob/master/images/img9.JPG)

- Predefined IPv6 Addresses
![img](https://github.com/Bes0n/LFCS/blob/master/images/img10.JPG)

- Obtaining an IPv6 Address 
![img](https://github.com/Bes0n/LFCS/blob/master/images/img11.JPG)

###### 8.3 Applying Run time Network Configuration
- ``` ip ```- monitor your network in run time. 
- ```ip link show``` - information about network interfaces
- ```ip address show``` - get all ip addresses
- ```ip address add dev ens33 10.0.0.10/24``` - add secondary IP address for devices named **ens33**. After reboot this IP will gone. You need persistent IP address. 
- ```ifconfig | help``` - shouldn't be used anymore
- ```ip route show``` - get information about routes

###### 8.4 Understanding Network Device Naming
- **biosdevname** - uses device names that reveal information about physical location. 
![img](https://github.com/Bes0n/LFCS/blob/master/images/img12.JPG)

###### 8.5 Applying Persistent Network Configuration in CentOS
- ```cat /etc/redhat-release``` - check your release version
- ```nmtui``` - network manager user interface
- ```nmcli``` - network manager command line
- ```man nmcli-examples``` - you can look for different examples
- ```rpm -qa | grep bash-completion``` - need for tabulation. To complete written commands
- ```nmcli connection modify ens33 ipv4.addresses 192.168.4.240/24 ipv4.gateway 192.168.4.2 ipv4.dns 8.8.8.8``` - set static ip address, gateway and DNS. 
- ```nmcli connection up ens33``` - enable network interface
- ```cd /etc/sysconfig/network-scripts``` - network configuration stored in this directory. 

###### 8.6 Applying Persistent Network Configuration in SUSE
- ```yast``` - generic SUSE configuration tool. From this configuration tool we can manage system settings. 

###### 8.7 Applying Persistent Network Configuration in Ubuntu
- ```cd /etc/network/``` - network interfaces directory

![img](https://github.com/Bes0n/LFCS/blob/master/images/img13.JPG)

- ``` ifdown ens33 ``` and then ```ifup ens33``` - reload network interface to apply changes to the network interface. 

###### 8.8 Managing Host Names
- ``` /etc/hostname ``` - where hostname information stored
- ``` uname -a ``` - get information about machine 
- ``` cd /proc/sys/kernel ``` - information about hostname also written here.  
- ``` vim /etc/hosts ```- configuration of hostname resolving

###### 8.9 Managing Host Name Resolution
- ```vim /etc/resolv.conf``` - configuration file of dns. 

```
# Generated by NetworkManager
search mydns.example.com example.com
nameserver 100.253.0.10
nameserver 110.225.100.10
```
*Note: if you can see that dns configured by NetworkManager better don't touch it directly.*

- ```vim /etc/nsswitch.conf``` - this file defines which file will be read first. **hostname**, **resolv.conf** or **myhostname**

```
#hosts:     db files nisplus nis dns
hosts:      files dns myhostname
```
*As we can see hostname comes first, dns second and myhostname is last*

###### 8.10 Using Common Network Tools
- ```ping``` - test response of other hosts

Let's ping google.com

```
64 bytes from bud02s27-in-f14.1e100.net (172.217.19.110): icmp_seq=1 ttl=52 time=21.7 ms
64 bytes from bud02s27-in-f14.1e100.net (172.217.19.110): icmp_seq=2 ttl=52 time=21.6 ms
64 bytes from bud02s27-in-f14.1e100.net (172.217.19.110): icmp_seq=3 ttl=52 time=21.4 ms
64 bytes from bud02s27-in-f14.1e100.net (172.217.19.110): icmp_seq=4 ttl=52 time=21.8 ms
```

- ```dig``` - verify dns related issues. If command not found install **bind-utils**
- ```dig google.com``` - let's check for google.com dns name 
```
; <<>> DiG 9.9.4-RedHat-9.9.4-74.el7_6.2 <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 481
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             135     IN      A       172.217.19.110

;; Query time: 19 msec
;; SERVER: 120.253.20.10#53(120.253.20.10)
;; WHEN: Mon Aug 05 14:30:24 CEST 2019
;; MSG SIZE  rcvd: 55
```
*Where IN means an Internet, A means an Answer.* 

- ``` dig nosuchdomainindig.com ``` - search for non-existing domain

``` 
; <<>> DiG 9.9.4-RedHat-9.9.4-74.el7_6.2 <<>> nosuchdomainindig.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 47450
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;nosuchdomainindig.com.         IN      A

;; AUTHORITY SECTION:
com.                    827     IN      SOA     a.gtld-servers.net. nstld.verisign-grs.com. 1565008545 1800 900 604800 86400

;; Query time: 19 msec
;; SERVER: 150.253.20.10#53(150.253.20.10)
;; WHEN: Mon Aug 05 14:37:01 CEST 2019
;; MSG SIZE  rcvd: 123
```

*Note: from **status: NXDOMAIN** we can see that such domain does not exist*

- ``` yum install nmap ``` - install nmap - provides information about ports.
- ``` nmap 10.0.2.15 ``` - get information about open ports. 
```
Starting Nmap 6.40 ( http://nmap.org ) at 2019-08-05 14:41 CEST
Nmap scan report for centos.example.com (10.0.2.15)
Host is up (0.000010s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
```

### Lesson 9: Configuring the SSH Service
###### 9.1 Configuring the SSH Service
- ```/etc/ssh/``` - directory where ssh configuration files stored. 
- ```/etc/ssh/sshd_config``` - server configuration config and sshd process configuration
- ```/etc/ssh/ssh_config``` - configuration for the ssh client

Important lines for **sshd_config** file:
```
# If you want to change the port on a SELinux system, you have to tell
# SELinux about this change.
# semanage port -a -t ssh_port_t -p tcp #PORTNUMBER
#
#Port 22

#PermitRootLogin yes
```

*Note: here we can change default port for connection and permit root login. **PermitRootLogin** must be set to **no***

**ssh_config** - configuration for ssh client. If you want to modify settings for all users on your system. 

```
# Host *
#   ForwardAgent no
#   ForwardX11 no
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
```

###### 9.2 Starting and Enabling the SSH Service
- ```systemctl status sshd``` - get information about **sshd** service 

```
● sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2019-08-06 11:52:45 CEST; 36min ago
     Docs: man:sshd(8)
           man:sshd_config(5)
 Main PID: 4927 (sshd)
   CGroup: /system.slice/sshd.service
           └─4927 /usr/sbin/sshd -D

Aug 06 11:52:45 centos.example.com systemd[1]: Stopped OpenSSH server daemon.
```

*Note: enabled means that this service will start on startup*

- ```systemctl stop|start|restart sshd``` - to stop, start and restart your service. If you make any change in configuration file you need to restart your service.
- ```systemctl disable|enable sshd``` - disable or enable sshd service for startup behaviour. 

###### 9.3 Using ssh to Connect to SSH
- ```ssh student@192.168.4.240``` - log on as *student* on *192.168.4.240*
- ```ssh -X student@192.168.4.240``` enable graphical interface while connect by ssh. You can run any graphical application by simply running name of the application. For instance: ```gedit &```
- ``` ssh-keygen ``` - will generate public and private keys, which can be used to authenticate on the server by using these keys instead of password prompt. Private key can be secured by **passphrase**
- ``` ssh-copy-id student@192.168.4.240``` - transfer your public key to remote host, so you can log on using private key, without password prompt.

###### 9.4 Using scp to Securely Copy Files Over the Network
- ```scp /etc/hosts 192.168.4.240:/tmp``` - copy **/etc/hosts** to the **192.168.4.240** host in **/tmp** directory
- ```scp 192.168.4.240:/etc/passwd .``` - copy **/etc/passwd** from remote host **192.168.4.240** to your home directory. 

###### 9.5 Managing File Synchronization using rsync
- ```rsync -avz /tmp student@192.168.4.240:/home/student/tmp``` - will syncronize local **/tmp** directory on remote host **192.168.4.240**. Useful if you need to syncronize large amount of data.

### Lesson 10: Configuring a Firewall
###### 10.1 Understanding Linux Firewalling
- **netfilter** - linux kernel firewalling functionality. 
- **iptables** - utility which takes care of firewalling
    - firewalld - on RedHat
    - ufw - on Ubuntu
    - susefirewall - on SUSE

![img](https://github.com/Bes0n/LFCS/blob/master/images/img14.JPG)

###### 10.2 Configuring a Firewall with firewalld
- ```firewall-cmd --list-all``` - get current configuration of firewall on **CentOs**
```
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: ssh dhcpv6-client
  ports:
  protocols:
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

- Where:
    - **interfaces** - is your current network interface to which role assigned
    - **services** and **ports** - which service or port to configure. 

- ``` firewall-cmd --get-services ``` - list of services that's provided which exists by default 
- ```cd /usr/lib/firewalld/services/``` - directory where services configuration files stored. Written by user firewalld.
- ``` firewall-cmd --add-service samba ``` - add samba services and allow required ports. But after firewall-cmd restart, added service will be disappear. It's because of different between runtime configuration and persistent one. 
- ```firewall-cmd --add-service samba --permanent``` - add samba service to firewalld configuration, but now permanently. 
- ```firewall-cmd --reload``` - reload firewalld configuration. 
- ```firewall-cmd --help | grep add-port``` - get information what you need to add a port, or port range
- ```firewall-cmd --add-port 4000-4005/tcp``` - open **TCP** ports from **4000** to **4005** in runtime configuration. For pestistent you just need to add **--permanent** key. 

###### 10 3 Configuring a Firewall with ufw
- ```sudo ufw enable``` - enable ubuntu firewall. 
- ```sudo ufw allow ssh``` - enable SSH access
- ```sudo ufw status``` - get status of your firewall and list of ports. 
- ```sudo ufw reject out ssh``` - outgoing ssh traffic is now rejected 
- ```sudo ufw delete reject out ssh``` - delete created firewall rule. 
- ```sudo ufw deny proto tcp from 192.168.4.245 to any port 22``` - denied traffic from **192.168.4.245** to port **22**
- ``` sudo ufw reset ``` - reset firewall to default settings
- ```sudo ufw app list``` - get list of available applications on firewall 
- ```sudo ufw app info OpenSSH``` - will show you info about OpenSSH application and port information
- ```sudo ufw logging on ``` - switch on logging 

###### 10.4 Configuring a Firewall with SUSEfirewall
- ```yast2``` - graphical version of **yast**
Click on **firewall** and start from configuration of **Interfaces**. After selection of zone we have to configure services which is located in **Allowed Services**. Add required service to the list of allowed services. Or we can use advanced configuration. Define custom ports and so on. 

###### 10.5 Understanding iptables Basics
In **iptables** we're working with chains
* Input
* Output
* Forward - for routing. 

- ```iptables {-A|I}``` - where **A** for append, **I** for insert. 
- ``` -j LOG|ACCEPT|DROP|REJECT``` - action for packet, **LOG** - write packet to the log file and do next actions, **ACCEPT** - accept this packet, **DROP** - silently drop packet (useful for external networks), **REJECT** - reject packet and inform about that to packet sender.  

##### 10.6 Configuring a Firewall with iptables
- ```systemctl stop firewalld``` - disable firewalld on centos
- ``` iptables -L ``` - check status of iptables
- ``` iptables -P INPUT DROP ``` and ```  iptables -P OUTPUT DROP ``` - configure iptables to reject any input/output behaviours. 
- ``` iptables -A INPUT -i lo -j ACCEPT ``` and ``` iptables -A OUTPUT -o lo -j ACCEPT ``` - allow incoming and outgoing connection for internal loop back interface - **lo** 
- ``` iptables -L -v ``` - to get much more details about configured rules. 
- ``` iptables -A INPUT -p tcp --dport 22 -j ACCEPT ``` - allow traffic with the destination port **22**
- ```iptables -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT``` - allow answers to get out from system. Load **state kernel module**. 
- ```iptables -A OUTPUT -p tcp --dport 22 -j ACCEPT``` - allow all traffic going out to port **22**
- ```iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT``` - allow answers to get out from system. Load **state kernel module** 
- ```iptables -A OUTPUT -p tcp --dport 80 -j ACCEPT``` - allow outgoing web traffic. 
    - ```yum install elinks``` - when we will try to install package, we going to receive errors *couldn't resolve name*. That one related to the DNS
- ```iptables -A OUTPUT -p udp --dport 53 -j ACCEPT``` - allow DNS.
- ```iptables-save``` - will be written to stdout
- ```iptables-save > /etc/sysconfig/iptabes``` - write your config to **iptables** file. So this config will be found after reboot.
- RedHat specific configuration:
    - ```systemctl disable firewalld``` - disable firewalld
    - ```yum install iptables-services``` - install **iptables-services**, because that one is not installed by default. 
    - ```systemctl enable iptables``` - service will start automatically after that. 

##### Lab
- ```iptables -P INPUT DROP``` - set up default policy to **DROP** all **INPUT** traffic
- ```iptables -P OUTPUT DROP``` - set up default policy to **DROP** all **OUTPUT** traffic
- ```iptables -A INPUT -i lo -j ACCEPT``` - **-A** - append to the default policy. Accept any **INPUT** (**-i**) connections for **lo** interface.
- ```iptables -A OUTPUT -o lo -j ACCEPT``` - **-A** - append to the default policy. Accept any **OUTPUT** (**-o**) connections for **lo** interface.
- ```iptables -A INPUT -p icmp -j ACCEPT``` - enable **icmp** protocol for **INPUT** incoming connections.
- ```iptables -A OUTPUT -m state --state ESTABLISHED,RELATIVE -j ACCEPT``` - allow answers to get out from system. Load **state kernel module** 
- ```iptables -A OUTPUT -p tcp --dport 80 -j ACCEPT``` - allow outgoinig HTTP for yum. 
- ``` iptables -A OUTPUT -p udp --dport 53 -j ACCEPT``` - allow DNS.

### Lesson 11: Configuring Time Services
###### 11.1 Understanding Time on Linux
Time in linux: 
- ``` hwclock ``` - hardware closk, BIOS.
    - ```hwclock``` - set hardware clock and synchronize with system clock. 
- ``` system clock ``` - system cloak appears after boot.
    - ``` date ``` - to set system clock

- ``` NTP ``` - Network Time Protocol, used to synchronize your time. 
    - ``` ntpd ``` or ``` chronyd ```- used to sync with ntp server

*Time set in UTC (Universal Time Coordinate)*  
*Difference between system time and ntp time shouldn't be more that **10 mins**. Otherwise your local host will refuse to syncrhonize with NTP*

![img](https://github.com/Bes0n/LFCS/blob/master/images/img15.JPG)

###### 11.2 Configuring Local Time on Linux
- ```hwclock``` - output will be ```2019-08-13 16:06:10.200221+0200```
    - ```hwclock --systohc``` - sync system time to the hardware time
    - ```hwclock --hctosys``` - sync hardware time to the system time 
- ```date``` - output will be ```Út srp 13 17:00:23 CEST 2019```
    - ```date -s 17:15``` - set up system time to *17:15*
- ```timedatectl``` - time and date configuration on CentOS

###### 11.3 Understanding the NTP Protocol
- Concept of ```stratum```. And the most reliable NTP service has a value ```stratum 0```

Stratum reliability:
    - ```Stratum 0``` - is an atomic clock. 
    - ```Stratum 1``` - server which sync with **Stratum 0**
    - ```Stratum 2``` - client which sync server and has **Stratum 1**
Better do not use NTP's with **stratum 10** - which means local clock, or **stratum 16** - which means clock hasn't set up yet. 

###### 11.4 Configuring Time Synchronization with ntpd
- ```ntpd``` - Time Synchronization Daemon. 
- ```chrony``` or ```chronyd``` - new time synchronization daemon with nano secs ability. 

Configuration of ntpd located in **/etc/ntp.conf**  
Where:  
    - ```server 0.opensuse.pool.ntp.org iburst``` - means which server use to sync and **iburst** - will synchronize time forcely if local time has big difference with NTP server.   


Internal hardware clock for synchronization, local clock has **stratum 10**, you can change it to **stratum 5**:
```
## Undisciplined Local Clock. This is a fake driver intended for backup  
## and when no outside source of synchronized time is available.  
##  
# server 127.127.1.0            # local clock (LCL)    
# fudge  127.127.1.0 stratum 10 # LCL is unsynchronized  
```

When you uncomment **server** and **fudge** options, restart ntpd service:  
- ```systemctl restart ntpd```
- ```ntpq -p``` - display information about NTP. Where we can see that local clock is used and stratum is **5**
```
     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
 LOCAL(0)        .LOCL.           5 l   24   64    1    0.000    0.000   0.000
```

###### 11.5 Configuring Time Synchronization with chronyd
- ``` chrony ``` - default ntp solution for RedHat and Fedora family 
- ```yum install chrony``` - to install it if you don't have. 
- ```systemctl status chronyd``` - get status of **chrony** daemon
- ```/etc/chrony.conf``` - configuration file of **chrony**  

```
# Use public servers from the pool.ntp.org project.
# Please consider joining the pool (http://www.pool.ntp.org/join.html).
server 0.centos.pool.ntp.org iburst
server 1.centos.pool.ntp.org iburst
server 2.centos.pool.ntp.org iburst
server 3.centos.pool.ntp.org iburst
```

- ```chronyc sources``` - To verify what **chrony** is doing

```
210 Number of sources = 4
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^? mail.deployis.eu              0   6     0     -     +0ns[   +0ns] +/-    0ns
^? zearla.netinform.hu           0   6     0     -     +0ns[   +0ns] +/-    0ns
^? 185.82.232.254                0   6     0     -     +0ns[   +0ns] +/-    0ns
^? 84.2.44.19                    0   6     0     -     +0ns[   +0ns] +/-    0ns
```

- ``` chronyc tracking``` - to get more details
```
Reference ID    : 00000000 ()
Stratum         : 0
Ref time (UTC)  : Thu Jan 01 00:00:00 1970
System time     : 0.000000000 seconds fast of NTP time
Last offset     : +0.000000000 seconds
RMS offset      : 0.000000000 seconds
Frequency       : 0.000 ppm slow
Residual freq   : +0.000 ppm
Skew            : 0.000 ppm
Root delay      : 1.000000000 seconds
Root dispersion : 1.000000000 seconds
Update interval : 0.0 seconds
Leap status     : Not synchronised
```

From output you can see **Leap status     : Not synchronised**, what means we didn't synchronised yet. This is because of the **iptables**. Let's add rule to the chain. 

- ```iptables -A INPUT -p udp --dport 123 -j ACCEPT``` - allow incoming time traffic. 
- ```iptables -A OUTPUT -p udp --dport 123 -j ACCEPT``` - same for **OUTPUT** traffic

Let's run ``` chronyc tracking ``` again. **Leap status** is **normal** now:
``` 
Reference ID    : 51007CFD (mail.deployis.eu)
Stratum         : 4
Ref time (UTC)  : Wed Aug 14 10:08:45 2019
System time     : 0.000000461 seconds fast of NTP time
Last offset     : -0.000689063 seconds
RMS offset      : 0.000689063 seconds
Frequency       : 3.080 ppm fast
Residual freq   : +0.000 ppm
Skew            : 512.361 ppm
Root delay      : 0.042404659 seconds
Root dispersion : 0.036888056 seconds
Update interval : 1.7 seconds
Leap status     : Normal
```

###### Lab solution
- ``` hwclock --systohc ``` and ``` hwclock --hctosys ``` - sync hardware and system clock and visa versa. 
- check iptables to allow **ntp** port **123**
- run ``` chronyc sources ``` and ```chronyc tracking``` to be sure that everything works properly.
- modify your **/etc/chrony.conf** file and uncomment following lines (to allow local clients use your ntp server in network):  
```
# Allow NTP client access from local network.
allow 10.0.10.0/16
```

Go to your client and configure ``` /etc/ntp.conf ```. Where as a **server** you need to specify your NTP server and comment out pool or servers:  
```
server 10.0.10.11 iburst
server 127.127.1.0              # local clock (LCL)
fudge  127.127.1.0 stratum 5    # LCL is unsynchronized
```

Reboot **ntpd** service and check ntpq status ``` ntpq -p ```. Stratum **16** means that it's unreachable and **.INIT** - initializing status. Slowly it's going to synchronize:  
```
     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
 10.0.10.11      .INIT.          16 u    -   64    0    0.000    0.000   0.000
 LOCAL(0)        .LOCL.           5 l   24   64    1    0.000    0.000   0.000
```

## Module 4: Operating Running Systems
### Lesson 12: Process Management
###### 12.1 Understanding Linux Processes and Jobs
![img](https://github.com/Bes0n/LFCS/blob/master/images/img16.JPG)

- Kernel starts with **PID** number 1: **systemd** (was **init** before)
- **Systemd** starts a lot of **kernel threads** which indicated by **[]** brackets. 
- processes can be monitored by **ps** command
- processes managed by user in **bash shell** also called as a jobs. Can be put in background and foreground. 
- **thread** - task that can be started by an individual process. Or it a subtask of one single process. For instance **apache** can create spawn a lot of **threads**

###### 12.2 Managing Interactive Shell Jobs
- ``` sleep 600 ``` - run sleep commands for 600 seconds
- ``` ctrl + z ``` - to stop job
- ``` bg ``` - to run stopped job in the background. 
- ``` sleep 600 & ``` - where **&** means run command in background
- ``` jobs ``` - monitor currently running jobs. 
- ``` fg ``` - run last job to the foreground. 
- ``` fg 1 ``` - move specific job to the foreground
- ``` ctrl + c ``` - cancel running job

###### 12.3 Monitoring Processes with top
- ```top``` -  provides all required information about processes. 

![img](https://github.com/Bes0n/LFCS/blob/master/images/img17.JPG)

Here we can see **time**, **uptime**, number of the logged on users and load average (5 10 15 minutes):    
``` top - 15:36:03 up  3:45,  1 user,  load average: 0.00, 0.01, 0.05 ```  

Third line shows us CPU load. By pressing **1** we can see load for one cpu. Where **us** means user space, **sy** means system space, **ni** - nice, priority modified, **id** - idle, **wa** - waiting for I/O (hard disk):  
```%Cpu0  :  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st```   

Second line shows to us currently running tasks:  
```Tasks:  94 total,   1 running,  93 sleeping,   0 stopped,   0 zombie```  

Processes column:  
```PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND```
- **S** - means status (R - running, S - sleeping)
- **VIRT RES SHR** - memory usage, Virtual memory(claimed memory), Resident memory (real usage), SHR(Shared memory)
- **PR** - priority
- **PID** - unique Process ID
- ``` top -u student ``` - processes started by specific user **student**

###### 12.4 Changing top Display Properties
- ``` top ``` and then type
    - ``` f ``` - for fields. Information about fields you can see in top. You can manage which fields to show, remove, sort and so on. 
    - ``` z ``` - for changing color of top
    - ``` W ``` - for saving configuration to **'/root/.toprc'**. this setting will available if you going to type ``` top ``` command again. 
![img](https://github.com/Bes0n/LFCS/blob/master/images/img18.JPG)

###### 12.5 Requesting Process Properties with ps
- ``` ps aux ``` - list all processes
- ``` ps aux | grep sshd ``` - find process **sshd**
- ``` ps -ef ``` - **PPID** - parent process id, we can see which process is the parent one.  
- ``` [kthreadd] ``` - process in square bracket means **kernel thread**. Can't be managed as a regular process. 

![img](https://github.com/Bes0n/LFCS/blob/master/images/img19.JPG)

- ``` ps -e -o pid,args --forest | less ``` - use filtering option, to show **output**, only **PID** and **arguments** in a forest view
- ``` ps aux --sort pmem ``` - sort processes using pmemory

###### 12.6 Changing Process Priority
- while in **TOP** command press **R** to change priority of the process. Where we need to enter **PID to renice**. 
- Nice range is starting from **-20** to **+90**. 
    - **-20** - is not going to be nice to other processes
    - **+90** - process will be nice to other processes
    *Note: regular user can run only positive numbers for nice, root can use also negative valuesq*
- ``` nice [OPTION] [COMMAND [ARG]] ```
- ``` nice -n 5 dd if/dev/zero =of/dev/null & ``` - going to start process with **nice** value **5**
- ``` renice -n 5 14053 ``` - renice already running process and set **nice** value to **5**

###### 12.7 Managing Processes with Signals
- ``` man 7 signals ``` - read about signals. 
    - ``` SIGTERM (15) ``` - nice way to ask process stop it's activity. Gracefull stop. 
    - ``` SIGKILL (9) ``` - roughly end the process. 
- ``` top ``` and then press ``` K ```, enter PID to kill the process. We have to enter **PID** and select **signal**. In our case we need **SIGKILL**
- ``` kill 14053 ``` - kill proces with **PID** number **14053**
- ``` killall dd ``` - kill all processes in match **dd**
- ``` kill -9 14231 ``` - **SIGKILL** for **14231** PID
- ``` pidof dd ``` - PID of command **dd**
- ``` kill $(pidof dd)``` - kill all **PIDs** of **dd** command

### Lesson 13: Managing Software Packages
###### 13.1 Installing Software from Source

- ``` tar (Tar Balls) ``` - tar archiver
- ``` tar xvf nmapgui-1.0.2.src.tar.gz ``` - where **x** means extract, **v** verbose, **f** - file. 
If you're working with source file, most time we have **Makefile** in source code. Also we have **README.txt** which is important to read.  

###### 13.2 Installing Software from Tar Balls
- ``` tar xvf nmapgui.src.tar.gz -C /tmp ``` where **-C** means location where to extract
- ```file nmapgui-1.0.2.src.tar.gz``` - if you don't know what type of data it's, run ``` file ``` command.  
```
nmapgui-1.0.2.src.tar.gz: gzip compressed data, was "nmapgui-1.0.2.src.tar", from Unix, last modified: Tue Sep  6 23:49:00 2005
```  
- ``` gunzip nmapgui-1.0.2.src.tar ``` - we can unzip archive with **gunzip**. In the end we will have file **nmapgui-1.0.2.src.tar**
- ``` file nmapgui-1.0.2.src.tar ``` - we will see as the result  
```
nmapgui-1.0.2.src.tar: POSIX tar archive (GNU
```  
- ``` tar tvf nmapgui-1.0.2.src.tar | less ``` - to see content of the archive.

###### 13.3 Creating and Compressing Tar Balls
- ``` tar cvf etc.tar /etc ``` where 
    - **c** - create
    - **v** - verbose
    - **f** - file 
    - **etc.tar** - name of the archive
    - **/etc** - what to archive
*Note: as you can see, there is no any compression and the .tar file is really big* 

- ```gzip etc.tar``` - let's add compression by using **gzip**. 
- ```gunzip etc.tar.gz``` - to get original file **etc.tar** back
- ```bzip2 etc.tar ``` - another archiver named **bzip2**
- ```tar xvf etc.tar.bz2 -C /``` - extract **etc.tar.bz2** to the root directory.
    - ```-u``` - this option only append files newer than copy in archive
    - ```-p``` - extract   information   about   file  permissions (default for superuser). What means if you want to save permissions during extraction use this options. That one is default option for root user. But for regular user you need to use **-p** option. 

###### 13.4 Understanding Software Dependencies
- ``` rpm -ivh nmap-frontend-6.40.noarch.rpm ``` - normal installation of the .rpm package.  
Dependency issue fixed by **META package handler**:
    - **apt** - Ubuntu
    - **yum** - RedHat
    - **dnf** - Fedora
    - **zypper** - SUSE

###### 13.5 Managing Libraries
- ```ldd /usr/bin/passwd``` - run to see which libraries required to run this command. 
- ``` ldd $(which ls) ``` - to find out is the specific library present.
```
linux-vdso.so.1 =>  (0x00007ffdb91f6000)
        libuser.so.1 => /lib64/libuser.so.1 (0x00007fee9dc39000)
        libgobject-2.0.so.0 => /lib64/libgobject-2.0.so.0 (0x00007fee9d9e9000)
        libglib-2.0.so.0 => /lib64/libglib-2.0.so.0 (0x00007fee9d6d3000)
        libpopt.so.0 => /lib64/libpopt.so.0 (0x00007fee9d4c9000)
        libpam.so.0 => /lib64/libpam.so.0 (0x00007fee9d2ba000)
        libpam_misc.so.0 => /lib64/libpam_misc.so.0 (0x00007fee9d0b6000)
        libaudit.so.1 => /lib64/libaudit.so.1 (0x00007fee9ce8d000)
        libselinux.so.1 => /lib64/libselinux.so.1 (0x00007fee9cc66000)
        libpthread.so.0 => /lib64/libpthread.so.0 (0x00007fee9ca4a000)
        libc.so.6 => /lib64/libc.so.6 (0x00007fee9c67d000)
        libgmodule-2.0.so.0 => /lib64/libgmodule-2.0.so.0 (0x00007fee9c479000)
        libcrypt.so.1 => /lib64/libcrypt.so.1 (0x00007fee9c242000)
        libpcre.so.1 => /lib64/libpcre.so.1 (0x00007fee9bfe0000)
        libffi.so.6 => /lib64/libffi.so.6 (0x00007fee9bdd8000)
        libdl.so.2 => /lib64/libdl.so.2 (0x00007fee9bbd4000)
        libcap-ng.so.0 => /lib64/libcap-ng.so.0 (0x00007fee9b9ce000)
        /lib64/ld-linux-x86-64.so.2 (0x00007fee9e05f000)
        libfreebl3.so => /lib64/libfreebl3.so (0x00007fee9b7cb000)
```

- ```ldconfig``` - to run update of the libraries. 
- ```ld.so.cache``` - cache of the libraries.
- ```ld.so.conf.d``` - configuration with path to the cache **ld.so.cache**
When you run packages install - **ldconfig** runs automatically and solve dependencies problems  

###### 13.6 Managing Packages on Red Hat and SUSE with rpm
- ```rpm ``` - Red Hat Package manager
    - ```rpm -qa``` - query all. 
    - ```rpm -qa | grep http``` - find is **http** installed
    - ```rpm -qi httpd``` - get information about installed package
    - ```rpm -ql httpd``` - list of files that installed from this package
    - ```rpm -qc httpd``` - list of configuration files
    - ```rpm -qd httpd``` - get documentation
    - ```rpm -qpi nmap-fronted-6.noarch.rpm``` - get information about package that not installed yet. 
    - ```rpm -qp --script nmap-fronted-6.noarch.rpm``` - get information about scripts which will be executed during package installation. 
    - ```rpm -qf /etc/nanorc ``` - will show where file comes from
    - ```rpm -qi nano``` - if you don't where file comes from. 
    - ```rpm -ql nano``` - files from the package.

###### 13.7 Managing Packages on Ubuntu with dpkg
- ```dpkg``` - debian package manager
    - ```dpkg --get-selections``` - list all installed packages
    - ```dpkg -L vim``` - show files in the package
    - ```dpkg -S /usr/bin/eject``` - from which package file comes from. 
    - ```dpkg -S eject ``` - same as above command
    - ```dpkg -p vim``` - get information about content of the package

###### 13.8 Using the yum Meta Package Handler
- ```yum search nmap``` - look if package is available
- ```cd /etc/yum.repos.d/``` - repository directory.
```
-rw-r--r--. 1 root root 1664 Nov 23  2018 CentOS-Base.repo
-rw-r--r--. 1 root root 1309 Nov 23  2018 CentOS-CR.repo
-rw-r--r--. 1 root root  649 Nov 23  2018 CentOS-Debuginfo.repo
-rw-r--r--. 1 root root  314 Nov 23  2018 CentOS-fasttrack.repo
-rw-r--r--. 1 root root  630 Nov 23  2018 CentOS-Media.repo
-rw-r--r--. 1 root root 1331 Nov 23  2018 CentOS-Sources.repo
-rw-r--r--. 1 root root 5701 Nov 23  2018 CentOS-Vault.repo
```  

- ```yum info nmap``` - get some information about package **nmap**
- ```yum install nmap-frontend``` - yum is going to resolve dependencies. During installation **transaction check** runs to see if the dependencies are available in repository for installing package.
- ```yum provides */sealert``` - to find out which package provides **/sealert**
```
setroubleshoot-server-3.2.30-3.el7.x86_64 : SELinux troubleshoot server
Repo        : base
Matched from:
Filename    : /usr/bin/sealert
```

- ```yum remove kernel``` - couldn't be removed because **kernel** is running and protected package. 
- ```yum remove bash``` - same for **bash**, dependencies will be processed and hit some protected packages like **systemd** and **yum**. So remove is not possible.
- ```yumdownloader vsftp``` - if you want only download package, without installation and then run ```rpm -qp --scripts vsftp``` - to see which scripts will be run. So you can analize there is nothing nasty inside. 

###### 13.9 Using the apt Meta Package Handler
- ``` apt-cache search ldap ``` - search for packages that contain **ldap** name in it. 
- ```apt-cache depends ldap-utils``` - get dependencies lists of the **ldap-utils**
- ```apt-cache rdepends ldap-utils``` - get reverse dependencies of the package
- ```apt-cache stats``` - get statistics about the packages
- ```apt-get update``` - to synchronise your repository with online database. 
- ```apt-get install nmap``` - install **nmap**. Which packages will be installed.
- ```apt-get check``` - check if there any broken installation
- ```apt-get clean``` - cleans package cache

###### 13.10 Using the zypper Meta Package Handler
- ```zypper search nmap``` - search for **nmap** package
- ```zypper install nmap``` - install **nmap** package
- ```yast``` - packages can be installed from GUI.
    - software patterns can be used from **yast**.

### Lesson 14: Scheduling Tasks
###### 14.1 Understanding Linux Task Scheduling
Three different solutions for running tasks:
- ```at```- run task once at specific time
- ```crond``` - task scheduler. 
- ```timers``` - systemd timer is the same as **crond**

Most important is **crond** working with configurations file.  
Main directory of **crond**:  
- ```/etc/crontab```
- ```/etc/cron.d/``` - you will put your time specific files here, to run them. 
- ```crontab -e -u``` - create user specific cron job.  
    - ```/cron.hourly``` \ 
    - ```/cron.daily``` - all managed by **anacron**. Helper of cron. 
    - ```/cron.weekly``` /
    - ```/cron.monthly``` /