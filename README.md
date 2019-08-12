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