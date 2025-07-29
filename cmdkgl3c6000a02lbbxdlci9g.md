---
title: "Essential Linux Commands: From File Creation to Permissions"
seoTitle: "Essential Linux Commands for DevOps Engineers: A Beginner’s Guide"
seoDescription: "Master essential Linux commands in this beginner-friendly guide. Learn file creation, directory management, user handling, permissions, and more"
datePublished: Sat Jul 26 2025 16:22:41 GMT+0000 (Coordinated Universal Time)
cuid: cmdkgl3c6000a02lbbxdlci9g
slug: essential-linux-commands-from-file-creation-to-permissions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1753718989078/9e51f85b-a570-4c6d-92ae-633862666c23.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1753719086965/51b617a9-7d42-4152-9472-768fe0294c34.jpeg
tags: linux, linux-for-beginners, linux-basics, linux-commands, file-permission, linux-networking, linux-terminal, linux-shell-scripting, linuxsystemadministration, softlink, file-management-in-linux, linux-users-and-groups, linux-usermanagement, linuxlearning-linuxforbeginners-linuxskills-linuxeducation-linuxtraining-linuxtips-linuxtutorials-learnlinux-linuxcertification-linuxadmin-linuxjourney-linuxmastery-linuxcommunity-sysadminlife-opensourceeducation, hardlinks-softlinks

---

Linux is a powerful operating system, and learning its basic commands can help you manage files, users, directories, and software easily. In this blog, we’ll explore the most commonly used Linux commands in a simple and beginner-friendly way.

## **🗂️ How to Create a File in Linux**

There are different ways to create files in Linux:

**1\. Using the** `cat` command

The `cat` command is used to create files, view content, and combine multiple files into one.

* You can create a single file.
    

```plaintext
azureuser@myvm:~$ cat > file1
Hi
I am Pankaj
azureuser@myvm:~$ cat file1
Hi
I am Pankaj
```

Press ‘ctrl+d’ to save the content of the file1.

* You can merge (concatenate) the content of multiple files into one.
    

```plaintext
azureuser@myvm:~$ ls
file1  file2
//Merging the content of file1 and file2 and redirecting the output to file3
azureuser@myvm:~$ cat file1 file2 > file3
azureuser@myvm:~$ cat file3
Hi
I am Pankaj
file2 content
```

* You can copy content from one file to another.
    

```plaintext
azureuser@myvm:~$ cat file2
file2 content
//Override the data of file1 to file2
azureuser@myvm:~$ cat file1 > file2
azureuser@myvm:~$ cat file2
Hi
I am Pankaj
```

* You can append/add content to an existing file
    

```plaintext
azureuser@myvm:~$ cat file1
Hi
I am Pankaj
azureuser@myvm:~$ cat >> file1
adding new data
azureuser@myvm:~$ cat file1
Hi
I am Pankaj
adding new data
```

* You can use `tac` to view the content from bottom to top.
    

```plaintext
azureuser@myvm:~$ tac file1
adding new data
I am Pankaj
Hi
```

**2\. Using the** `touch` command

The `touch` command is used to create empty files and update timestamps.

* You can create one or more empty files.
    

```plaintext
azureuser@myvm:~$ touch tfile1 tfile2
azureuser@myvm:~$ ls
file1  file2  file3  tfile1  tfile2
// Since tfile1 and tfile2 are empty, the cat command produces no output
azureuser@myvm:~$ cat tfile1
```

* You can update the access and modify time of a file.
    

**Time Stamps in Linux**

* stat command
    
    * `stat` command displays detailed information about the file `file1`, such as its size, permissions, owner, group, last access time, last modification time, and more
        

```plaintext
// to check the time stamp of a file
azureuser@myvm:~$ stat file1
  File: file1
  Size: 32              Blocks: 8          IO Block: 4096   regular file
Device: 801h/2049d      Inode: 258086      Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/azureuser)   Gid: ( 1000/azureuser)
Access: 2025-07-26 16:25:12.300405360 +0000
Modify: 2025-07-26 16:15:09.179520655 +0000
Change: 2025-07-26 16:25:12.300405360 +0000
 Birth: 2025-07-26 16:05:14.899247475 +0000
```

* **Access time**: Last time the file was opened.  
    Example: `touch -a file1`
    
    **Note:**
    
    The `touch -a file1` command updates **only the access time** of the file `file1`, without changing its content or the modification time.
    
    For example, before running the command, the `stat` output was shown above:
    
    Access: 2025-07-26 16:25:12.300405360 +0000
    
    After executing `touch -a file1`, the access time is updated to the current time.
    
    **Important**:  
    The **change time (ctime)** is also updated because it reflects changes to the file's metadata, such as access or modification times—even if the file content remains unchanged.
    

```plaintext
azureuser@myvm:~$ touch -a file1
azureuser@myvm:~$ stat file1
  File: file1
  Size: 32              Blocks: 8          IO Block: 4096   regular file
Device: 801h/2049d      Inode: 258086      Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/azureuser)   Gid: ( 1000/azureuser)
Access: 2025-07-26 16:33:27.708122788 +0000
Modify: 2025-07-26 16:15:09.179520655 +0000
Change: 2025-07-26 16:33:27.708122788 +0000
 Birth: 2025-07-26 16:05:14.899247475 +0000
```

* **Modify time**: Last time the file content was changed.  
    Example: `touch -m file1`
    
    **Note**: Only modify time changed
    

```plaintext
azureuser@myvm:~$ touch -m file1
azureuser@myvm:~$ stat file1
  File: file1
  Size: 32              Blocks: 8          IO Block: 4096   regular file
Device: 801h/2049d      Inode: 258086      Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/azureuser)   Gid: ( 1000/azureuser)
Access: 2025-07-26 16:33:27.708122788 +0000
Modify: 2025-07-26 16:42:37.350568502 +0000
Change: 2025-07-26 16:42:37.350568502 +0000
 Birth: 2025-07-26 16:05:14.899247475 +0000
```

* **Change time**: Last time the file’s metadata (like size or format) was changed.  
    Note: When a file is modified/Access, the change time is updated automatically.
    
    **Example:** In the above case, the **change time** (`ctime`) was also updated after running `touch -a file1` or `touch -m file1`.  
    The updated change time is:  
    `Change: 2025-07-26 16:42:37.350568502 +0000`
    
    ```plaintext
    azureuser@myvm:~$ stat file1
      File: file1
      Size: 32              Blocks: 8          IO Block: 4096   regular file
    Device: 801h/2049d      Inode: 258086      Links: 1
    Access: (0664/-rw-rw-r--)  Uid: ( 1000/azureuser)   Gid: ( 1000/azureuser)
    Access: 2025-07-26 16:33:27.708122788 +0000
    Modify: 2025-07-26 16:42:37.350568502 +0000
    Change: 2025-07-26 16:42:37.350568502 +0000
     Birth: 2025-07-26 16:05:14.899247475 +0000
    ```
    

---

**3.✍️ Text Editors in Linux**

**a.**`vi` **Editor**

* A standard editor used for programming and plain text.
    
* Press `i` to start writing.
    
* Press `Esc` and type:
    
    * `:w` to save
        
    * `:wq` or `:x` to save and quit
        
    * `:q` to quit
        
    * `:q!` to quit without saving
        

```plaintext
azureuser@myvm:~$ vi vifile.txt
azureuser@myvm:~$ cat vifile.txt
vi editor example
```

**b.**`nano` **Editor**

* A simple editor that doesn’t require pressing `i` to start editing.
    
* Press `ctrl+x` and type:
    
    * `y` to save
        
    * press ‘enter’ to exit out of the editor
        

```plaintext
azureuser@myvm:~$ nano nanofile.txt
azureuser@myvm:~$ cat nanofile.txt
nano editor example
```

---

**4.📢 Using the** `echo` **Command**

* To create a file with content: `echo "Welcome" > echofile`
    

```plaintext
azureuser@myvm:~$ echo "Welcome" > echofile
azureuser@myvm:~$ cat echofile
Welcome
```

* To add content to an existing file: `echo "Namaste" >> echofile`
    

```plaintext
azureuser@myvm:~$ echo "Namaste" >> echofile
azureuser@myvm:~$ cat echofile
Welcome
Namaste
```

* To empty a file: `echo > echofile`
    
    * This command clears the contents of the file named `echofile`. It does not produce any output on the terminal. If the file doesn't exist, it will be created as an empty file.
        

```plaintext
azureuser@myvm:~$ echo > echofile
azureuser@myvm:~$ cat echofile
```

---

## **📁 Directory and File Management**

* **Lists files and directories in long format (with permissions, owner, size, and date):**`ls -l`
    

```plaintext
azureuser@myvm:~$ ls -l
total 24
-rw-rw-r-- 1 azureuser azureuser  1 Jul 26 16:57 echofile
-rw-rw-r-- 1 azureuser azureuser 32 Jul 26 16:42 file1
-rw-rw-r-- 1 azureuser azureuser 16 Jul 26 16:11 file2
```

* **Lists all files, including hidden ones (those starting with** `.`)**, in long format:** `ls -la`
    

```plaintext
azureuser@myvm:~$ ls -la
total 64
drwxr-x--- 5 azureuser azureuser 4096 Jul 26 16:56 .
drwxr-xr-x 3 root      root      4096 Jul 26 16:02 ..
-rw------- 1 azureuser azureuser  263 Jul 26 16:35 .bash_history
-rw-r--r-- 1 azureuser azureuser  220 Jan  6  2022 .bash_logout
drwx------ 2 azureuser azureuser 4096 Jul 26 16:02 .ssh
-rw-r--r-- 1 azureuser azureuser    0 Jul 26 16:03 .sudo_as_admin_successful
-rw------- 1 azureuser azureuser  988 Jul 26 16:51 .viminfo
-rw-rw-r-- 1 azureuser azureuser    1 Jul 26 16:57 echofile
-rw-rw-r-- 1 azureuser azureuser   32 Jul 26 16:42 file1
-rw-rw-r-- 1 azureuser azureuser   16 Jul 26 16:11 file2
-rw-rw-r-- 1 azureuser azureuser   30 Jul 26 16:09 file3
```

* **Displays the list of previously executed commands:** `history`
    

```plaintext
azureuser@myvm:~$ history
    1  clear
    2  touch -a file1
    3  stat file1
    4  touch -m file1
    5  stat file1
```

* **Creates a new directory named** : `mkdir dir1`
    

```plaintext
azureuser@myvm:~$ mkdir dir1
azureuser@myvm:~$ ls
dir1
```

* **Creates nested directories in one command:** `mkdir -p dir6/dir7/dir8`
    
    * p → parent directories
        

```plaintext
azureuser@myvm:~$ ls
dir1  dir6
azureuser@myvm:~$ cd dir6
azureuser@myvm:~/dir6$ ls
dir7
```

* **Changes the current directory to dir1**: `cd dir1`
    

```plaintext
azureuser@myvm:~$ cd dir1
azureuser@myvm:~/dir1$
```

* **Moves up/ one step back from one directory level:** `cd ..`
    

```plaintext
azureuser@myvm:~$ ls
dir1  dir6 
azureuser@myvm:~$ cd dir1
azureuser@myvm:~/dir1$ cd ..
azureuser@myvm:~$
```

* **Prints the current working directory path:** `pwd`
    

```plaintext
azureuser@myvm:~$ pwd
/home/azureuser
```

* **Moves up(steps back) three directory levels:** `cd ../../..`
    
    * **Current directory:** `/home/azureuser`
        
    * **After moving up three levels:** `/` (root directory)
        

```plaintext
azureuser@myvm:~$ pwd
/home/azureuser
azureuser@myvm:~$ cd ../../..
// moved to root directory
azureuser@myvm:/$ pwd
/
```

* **Jumps directly to the specified nested path:** `cd /home/azureuser/dir1`
    

```plaintext
azureuser@myvm:/$ cd /home/azureuser/dir1
azureuser@myvm:~/dir1$
```

* **Creates multiple directories at once:** `mkdir dir8 dir9 dir10`
    

```plaintext
azureuser@myvm:~$ mkdir dir8 dir9 dir10
azureuser@myvm:~$ ls
dir1  dir10  dir2  dir3  dir6  dir8  dir9  echofile  file1  file2  file3  nanofile.txt  tfile1  tfile2  vifile.txt
```

* **Creates a hidden file named** : `touch .file`
    
    * The `touch .file` command creates a **hidden file** named `.file`. In Linux, any file or directory that starts with a dot (`.`) is considered hidden and won’t appear in a normal `ls` listing.
        
        To view hidden files, use: `ls -la`
        

```plaintext
azureuser@myvm:~$ touch .file
azureuser@myvm:~$ ls -la
total 5
4 drwxrwxr-x 2 azureuser azureuser 4096 Jul 26 17:07 dir1
4 drwxrwxr-x 2 azureuser azureuser 4096 Jul 26 17:20 dir10
-rw-rw-r--  1 azureuser azureuser    0 Jul 26 17:21 .file
```

* **Creates a hidden directory named** : `mkdir .dir11`
    
    * Hidden files in Linux (those starting with a dot `.`) are **not primarily for security**, but they help **prevent accidental modification or deletion**, especially by inexperienced users.
        
        For example, some hidden files are **critical for system configuration**. If a user unintentionally deletes them, it could lead to system instability or even corruption.
        

```plaintext
azureuser@myvm:~$ mkdir .dir11
total 6
drwxrwxr-x  2 azureuser azureuser 4096 Jul 26 17:26 .dir11
```

---

**📤 Copy, Move, and Delete Files**

* Copy a file: `cp file1 file10`
    
    * cp → copy
        
    * file1 → source file
        
    * file10 → destination file
        

```plaintext
azureuser@myvm:~$ cat file2
Hi
I am Pankaj
azureuser@myvm:~$ touch file10
azureuser@myvm:~$ ls
 file10  file2
azureuser@myvm:~$ cat file10
//no output
azureuser@myvm:~$ cp file2 file10
azureuser@myvm:~$ cat file10
Hi
I am Pankaj
```

* Move a file: `mv file1 dir1`
    
    * it is just like cut and paste in windows
        
    * mv → move
        
    * file → source file
        
    * dir1→ destination file
        

```plaintext
azureuser@myvm:~$ mv file1 dir1
azureuser@myvm:~$ cd dir1
azureuser@myvm:~/dir1$ ls
file1
```

* Rename a file: `mv file2 newfile`
    
    * **There is no dedicated command to rename a file in Linux.**  
        Instead, we use the `mv` (move) command to **move the current file to a new name or location**, which effectively renames it.
        

```plaintext
azureuser@myvm:~$ ls
dir10 file10  file2
azureuser@myvm:~$ mv file2 newfile
azureuser@myvm:~$ ls
dir10 file10 newfile
```

* Remove an empty directory: `rmdir dir2`
    

```plaintext
azureuser@myvm:~$ ls
dir1 dir2
azureuser@myvm:~$ rmdir dir2
azureuser@myvm:~$ ls
dir1
```

* Remove nested empty directories: `rmdir -p dir6/dir7/dir8`
    
    * rmdir → remove directory
        
    * p → parent
        
    * Nested directory → `dir6/dir7/dir8`
        

```plaintext
azureuser@myvm:~$ ls
dir3  dir6
azureuser@myvm:~/dir6$ ls
dir7
azureuser@myvm:~/dir6$ cd dir7
azureuser@myvm:~/dir6/dir7$ ls
dir8
azureuser@myvm:~/dir6/dir7$ cd dir8
azureuser@myvm:~/dir6/dir7/dir8$ 

//Removing Nested directory
azureuser@myvm:~$ rmdir -p dir6/dir7/dir8
azureuser@myvm:~$ ls
dir3
```

* Remove with verbose output: `rmdir -pv dirTest/dirX/dirY`
    
    * This command removes **empty directories(last directory)** and shows messages for each one it deletes.
        
        * `-p` means: remove **parent directories** too, if they are empty.
            
        * `-v` means: show a **message** for each directory removed.
            
            ```plaintext
            azureuser@myvm:~$ mkdir -p dirTest/dirX/dirY
            azureuser@myvm:~$ ls
            dirTest 
            azureuser@myvm:~$ rmdir -pv dirTest/dirX/dirY
            rmdir: removing directory, 'dirTest/dirX/dirY'
            rmdir: removing directory, 'dirTest/dirX'
            rmdir: removing directory, 'dirTest'
            ```
            
        * ⚠️ The **last directory** (`dirY`) **must be empty**, otherwise the command will fail.
            
            * Example: Let’s create the same folder structure and add a file inside `dirY`
                
            
            ```plaintext
            azureuser@myvm:~$ mkdir -p dirTest/dirX/dirY
            azureuser@myvm:~$ cd dirTest/dirX/dirY
            azureuser@myvm:~/dirTest/dirX/dirY$ touch file1
            azureuser@myvm:~/dirTest/dirX/dirY$ ls
            file1
            azureuser@myvm:~/dirTest/dirX/dirY$ cd ..//..//..
            azureuser@myvm:~$ ls
            dirTest 
            azureuser@myvm:~$ rmdir -pv dirTest/dirX/dirY
            rmdir: removing directory, 'dirTest/dirX/dirY'
            rmdir: failed to remove 'dirTest/dirX/dirY': Directory not empty
            ```
            
* Remove non-empty directories: `rm -rf dir1`
    
    * rm → remove
        
    * rf→ remove forcefully
        

```plaintext
azureuser@myvm:~$ ls
dir1  dir10  dir3  dir8  dir9  dirTest 
azureuser@myvm:~/dir1$ ls
file1  test
azureuser@myvm:~/dir1$ cd ..
azureuser@myvm:~$ rm -rf dir1
azureuser@myvm:~$ ls
dir10  dir3  dir8  dir9  dirTest
```

* Remove empty directory: `rm -r dir1`
    
    * rm→ remove
        
    * r→ **recursive** – it tells `rm` to **delete the directory and everything inside it**, including subdirectories and files.
        
    * You only need to specify the **original directory or file name**, such as `dirTest` to move the nested directory
        

```plaintext
azureuser@myvm:~$ ls
dir10  dir3  dir8  dir9  dirTest  
azureuser@myvm:~$ cd dirTest
azureuser@myvm:~/dirTest$ ls
dirX
azureuser@myvm:~/dirTest$ cd dirX
azureuser@myvm:~/dirTest/dirX$ ls
dirY
azureuser@myvm:~/dirTest/dirX$ cd dirY
azureuser@myvm:~/dirTest/dirX/dirY$ ls
file1
azureuser@myvm:~/dirTest/dirX/dirY$ cd ..//..//..
azureuser@myvm:~$ rm -r dirTest
azureuser@myvm:~$ ls
10  dir10  dir3  dir8  dir9
```

---

**🧹 Clearing the Console**

* To clear the terminal screen and remove all previous commands from view, use:
    

```plaintext
azureuser@myvm:~$ clear
```

**📄 Viewing File Content in Different Ways**

* To check the **first page** of a file: `less file`
    
    * file → filename (eg : file2, file3 etc)
        
    * Press `q` to exit the view.
        

```plaintext
azureuser@myvm:~$ ls
dir10  dir3  dir8  dir9  echofile  file 
azureuser@myvm:~$ less file
1
2
2
3
3
4
5
6
7
8
file
```

* To check the **first 10 lines** of a file: `head file`
    
    * file → filename
        

```plaintext
azureuser@myvm:~$ head file
1
2
2
3
3
4
5
6
7
8
```

* To check the **last 10 lines** of a file : `tail file`
    
    * file → filename
        

```plaintext
azureuser@myvm:~$ tail file
r
u
u
n
n
n
ng
g
k
last page content
```

* To view a file **page by page** (useful for large files): `more file`
    
    * file → filename
        
    * press ‘Enter’ to view next page and ‘q’ to move out of the file
        

```plaintext
azureuser@myvm:~$ more file
1
2
2
3
3
4
5
--More--(45%)
```

* To sort the contents of a file in alphabetical order: `sort file`
    
    * file → filename
        

```plaintext
azureuser@myvm:~$ cat file2
a
v
g
b
z
t
azureuser@myvm:~$ sort file2
a
b
g
t
v
z
```

* To filter a specific word or alphabet from a file: `grep "man" file2`
    
    * Example:
        
        * **Word to find:** man
            
        * **File to search in:** file2
            

```plaintext
azureuser@myvm:~$ cat file2
a
v
g
b
z
t
man
cse
book
azureuser@myvm:~$ grep "man" file2
man
```

## **🌐 Network and System Information**

* Check IP and network: `ifconfig`
    

```plaintext
azureuser@myvm:~$ ifconfig
Command 'ifconfig' not found, but can be installed with:
sudo apt install net-tools
azureuser@myvm:~$ sudo apt install net-tools
azureuser@myvm:~$ ifconfig
enP43463s1: flags=6211<UP,BROADCAST,RUNNING,SLAVE,MULTICAST>  mtu 1500
        inet6 fe80::222:48ff:fe22:8615  prefixlen 64  scopeid 0x20<link>
        ether 00:22:48:22:86:15  txqueuelen 1000  (Ethernet)
        RX packets 56300  bytes 76705466 (76.7 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 55300  bytes 17330159 (17.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

* Check only IP: `hostname -i`
    

```plaintext
azureuser@myvm:~$ hostname -i
10.0.0.4
```

* Check OS version: `cat /etc/os-release` or `cat /etc/os-rel*`
    

```plaintext
azureuser@myvm:~$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.5 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.5 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```

---

## **📦 Software and Package Management**

**Note**: I have used Apache2 as an example. Please feel free to replace it with the software of your choice.

**In Ubuntu:**

* Install software: `sudo apt install apache2 -y`
    

```plaintext
azureuser@myvm:~$ sudo apt install apache2 -y
```

* Check if a software is installed: `which apache2`
    
    * `which apache2` checks if the `apache2` binary is in your system's PATH.
        
    * If Apache2 is installed and in the PATH, it will return the path to the executable (e.g., `/usr/sbin/apache2`).
        
    * If it's not installed, it will return nothing.
        

```plaintext
azureuser@myvm:~$ which apache2
/usr/sbin/apache2
```

* Update packages: `sudo apt update`
    

```plaintext
azureuser@myvm:~$ sudo apt update
Hit:1 http://azure.archive.ubuntu.com/ubuntu jammy InRelease
Get:2 http://azure.archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]
Hit:3 http://azure.archive.ubuntu.com/ubuntu jammy-backports InRelease
Get:4 http://azure.archive.ubuntu.com/ubuntu jammy-security InRelease [129 kB]
Fetched 257 kB in 0s (517 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
All packages are up to date.
```

* Start service: `sudo systemctl start apache2`
    

```plaintext
azureuser@myvm:~$ sudo systemctl start apache2
```

* Check service status: `sudo systemctl status apache2`
    
    * **If the output shows** `Active: active (running) since Mon 2025-07-28 08:43:47 UTC; 5min ago`, it means the Apache2 service is currently running on your system.
        

```plaintext
azureuser@myvm:~$ sudo systemctl status apache2
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2025-07-28 08:43:47 UTC; 5min ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 1598 (apache2)
      Tasks: 55 (limit: 9462)
     Memory: 5.4M
        CPU: 40ms
     CGroup: /system.slice/apache2.service
             ├─1598 /usr/sbin/apache2 -k start
             ├─1600 /usr/sbin/apache2 -k start
             └─1601 /usr/sbin/apache2 -k start

Jul 28 08:43:47 myvm systemd[1]: Starting The Apache HTTP Server...
Jul 28 08:43:47 myvm systemd[1]: Started The Apache HTTP Server.
```

* Stop service: `sudo systemctl stop apache2`
    
    * If the Apache service stops manually, you need to restart it using the command: `sudo systemctl restart apache2`
        
    * **If the output shows** `Active: inactive (dead) since Mon 2025-07-28 08:51:57 UTC; 7s ago`, it means the Apache2 service is currently not running on your system.
        

```plaintext
azureuser@myvm:~$ sudo systemctl stop apache2
azureuser@myvm:~$ sudo systemctl status apache2
○ apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: inactive (dead) since Mon 2025-07-28 08:51:57 UTC; 7s ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 2248 ExecStop=/usr/sbin/apachectl graceful-stop (code=exited, status=0/SUCCESS)
   Main PID: 1598 (code=exited, status=0/SUCCESS)
        CPU: 62ms

Jul 28 08:43:47 myvm systemd[1]: Starting The Apache HTTP Server...
Jul 28 08:43:47 myvm systemd[1]: Started The Apache HTTP Server.
Jul 28 08:51:57 myvm systemd[1]: Stopping The Apache HTTP Server...
Jul 28 08:51:57 myvm systemd[1]: apache2.service: Deactivated successfully.
Jul 28 08:51:57 myvm systemd[1]: Stopped The Apache HTTP Server.
```

* Restart service after manual stop: `sudo systemctl restart apache2`
    

```plaintext
azureuser@myvm:~$ sudo systemctl restart apache2
// check the status
azureuser@myvm:~$ sudo systemctl status apache2
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2025-07-28 08:59:03 UTC; 5s ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 4231 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCESS)
   Main PID: 4235 (apache2)
      Tasks: 55 (limit: 9462)
     Memory: 5.2M
        CPU: 24ms
     CGroup: /system.slice/apache2.service
             ├─4235 /usr/sbin/apache2 -k start
             ├─4236 /usr/sbin/apache2 -k start
             └─4237 /usr/sbin/apache2 -k start

Jul 28 08:59:03 myvm systemd[1]: Starting The Apache HTTP Server...
Jul 28 08:59:03 myvm systemd[1]: Started The Apache HTTP Server.
```

* Enable service on boot: `sudo systemctl enable apache2`
    

```plaintext
azureuser@myvm:~$ sudo systemctl enable apache2
Synchronizing state of apache2.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable apache2
```

* Disable service on boot: `sudo systemctl disable apache2`
    

```plaintext
sudo systemctl disable apache2
Synchronizing state of apache2.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable apache2
Removed /etc/systemd/system/multi-user.target.wants/apache2.service.
```

* Remove software: `sudo apt remove apache2`
    

```plaintext
azureuser@myvm:~$ sudo apt remove apache2
azureuser@myvm:~$ sudo systemctl status apache2
○ apache2.service
     Loaded: masked (Reason: Unit apache2.service is masked.)
     Active: inactive (dead)
```

* List installed packages: `apt list --installed`
    

```plaintext
azureuser@myvm:~$ apt list --installed
Listing... Done
adduser/jammy,now 3.118ubuntu5 all [installed,automatic]
apache2-bin/jammy-updates,jammy-security,now 2.4.52-1ubuntu4.15 amd64 [installed,auto-removable]
apache2-data/jammy-updates,jammy-security,now 2.4.52-1ubuntu4.15 all [installed,auto-removable]
apache2-utils/jammy-updates,jammy-security,now 2.4.52-1ubuntu4.15 amd64 [installed,auto-removable]
apparmor/jammy-updates,jammy-security,now 3.0.4-2ubuntu2.4 amd64 [installed,automatic]
------- many more
```

**Question -1:** What is the **difference between** `start` and `enable` when managing the any software( eg: apache2 ) service

**🔹** `start` – Start the Service **Now**

* **Command:** `sudo systemctl start apache2`
    
* **What it does:** Immediately starts the Apache2 service.
    
* **Effect:** Apache2 begins running **right now**, but it **won’t start automatically** after a reboot unless you also enable it.
    

**🔹** `enable` – Start the Service **on Boot**

* **Command:** `sudo systemctl enable apache2`
    
* **What it does:** Configures Apache2 to **start automatically** every time the system boots.
    
* **Effect:** Doesn’t start the service immediately, just sets it to start on future reboots
    

**Question -2:** What is the **difference between** `stop` and `disable` when managing the any software( eg: apache2 ) service

**🔴** `stop` Apache2

* **Command:** `sudo systemctl stop apache2`
    
* **Effect:** Immediately stops the Apache2 service.
    
* **Temporary:** Apache2 will **start again after a reboot** if it was enabled.
    
* **Use case:** You want to temporarily stop the web server without changing its startup behavior.
    

**🚫** `disable` Apache2

* **Command:** `sudo systemctl disable apache2`
    
* **Effect:** Prevents Apache2 from starting **automatically at boot**.
    
* **Does not stop** the currently running service.
    
* **Use case:** You don’t want Apache2 to start automatically when the system reboots.
    

---

## **👤 User and Group Management**

* Check current user: `whoami`
    

```plaintext
azureuser@myvm:~$ whoami
azureuser
```

* Show a message: `echo "hello" | sudo wall`
    
    * **Scenario:** Suppose you're working on your VM and your friend is also logged into the same VM. To show a message to your friend, you can use the echo command along with a method to target their terminal session.
        

```plaintext
azureuser@myvm:~$ echo "hello" | sudo wall

Broadcast message from root@myvm (pts/1) (Mon Jul 28 09:57:57 2025):

hello

Broadcast message from root@myvm (pts/1) (Mon Jul 28 09:57:57 2025):

hello
```

* Create a user: `useradd pankaj`
    
    * logged-in as root user (cmd: `sudo su`)
        

```plaintext
root@myvm:/home/azureuser# useradd pankaj
```

* Set password: `passwd pankaj`
    
    * logged-in as root user (cmd: `sudo su`)
        

```plaintext
root@myvm:/home/azureuser# passwd pankaj
New password:
Retype new password:
passwd: password updated successfully
```

* To view the created or existing users on a Linux system: `cat /etc/passwd`
    

```plaintext
root@myvm:/home/azureuser# cat /etc/passwd
azureuser:x:1000:1000:Ubuntu:/home/azureuser:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
pankaj:x:1001:1001::/home/pankaj:/bin/bash
```

* Create a group: `groupadd cse`
    
    * logged-in as root user (cmd: `sudo su`)
        

```plaintext
root@myvm:/home/azureuser# groupadd cse
```

* To view the group or existing group on a Linux system: `cat /etc/group`
    
    * **Note:** This file contains all the groups on the system, and by default, each user is also automatically associated with at least one group listed here
        

```plaintext
root@myvm:/home/azureuser# cat /etc/group
azureuser:x:1000:
ssl-cert:x:123:
pankaj:x:1001:
cse:x:1002:
```

* Add user to group: `gpasswd -a pankaj cse`
    
    * logged-in as root user (cmd: `sudo su`)
        
    * a→ add user
        

```plaintext
root@myvm:/home/azureuser# gpasswd -a pankaj cse
Adding user pankaj to group cse
// let's validate user
root@myvm:/home/azureuser# cat /etc/group
cse:x:1002:pankaj
```

* Delete a user: `sudo userdel username`
    
    * Add `sudo` at the beginning of the command if you are not logged in as the root user
        
    * **the user to be delected**: arup
        

```plaintext
root@myvm:/home/azureuser# userdel arup
```

* Delete a group: `sudo userdel username`
    
    * Add `sudo` at the beginning of the command if you are not logged in as the root user
        
    * **the group to be deleted:** ece
        

```plaintext
root@myvm:/home/azureuser# groupdel ece
```

* Add multiple users to a group: `gpasswd -M ajay,sameer,vijay cse`
    
    * \-M: stands for member user
        
    * Note: The user should be created before being added to a group
        
    * I have logged-in as root user.
        
    * Output: cse:x:1002:ram,peter,vijay
        

```plaintext
root@myvm:/home/azureuser# gpasswd -M ram,peter,vijay cse
pankaj:x:1001:
cse:x:1002:ram,peter,vijay
ram:x:1003:
peter:x:1004:
vijay:x:1005:
```

---

## **🔗 Links and Backups**

**Soft Link:**

**Create a soft link** **(just like window’s shortcut)**: `ln -s file1 softlinkfile1`

* A **soft link** is like a shortcut or pointer to another file.
    
* `ln` → the command to create links.
    
* `-s` → tells `ln` to create a **symbolic (soft) link** instead of a hard link.
    

```plaintext
azureuser@myvm:~$ ln -s file1 softlinkfile1
```

* It stores the **path** to the original file.
    
* Check if a file has a soft link: `ls -l`
    

```plaintext
azureuser@myvm:~$ ls -l
total 2
-rw-rw-r-- 1 azureuser azureuser   22 Jul 28 10:30 file1
lrwxrwxrwx 1 azureuser azureuser    5 Jul 28 11:57 softlinkfile1 -> file1
```

* If the original file is deleted, the soft link becomes **broken**.
    

```plaintext
azureuser@myvm:~$ rm file1
azureuser@myvm:~$ cat softlinkfile1
cat: softlinkfile1: No such file or directory
```

* **✅ Use case:**
    
    * Useful when you want to reference a file from multiple locations
        
    * Common in backups or shared configurations.
        

**Hard link:**

* **Create a hard link (for backup purpose)**: `ln file2 backupfile2`
    
    * A **hard link** is a direct reference to the **data** on disk.
        
    * Both the original file and the hard link share the same **inode**.
        
    * If you update ‘file2’, then ‘backupfile2’ will also be updated — and the same happens if you modify ‘backupfile2’ — only if they are linked using a hard link.
        
    
    ```plaintext
    azureuser@myvm:~$ ln file2 backupfile2
    azureuser@myvm:~$ ls -l
    total 28
    -rw-rw-r-- 2 azureuser azureuser   26 Jul 28 09:38 backupfile2
    -rw-rw-r-- 2 azureuser azureuser   26 Jul 28 09:38 file2
    ```
    
    * If the original file is deleted, the hard link still works — the data remains.
        
    
    ```plaintext
    azureuser@myvm:~$ rm file2
    azureuser@myvm:~$ ls
    backupfile2  file3 
    azureuser@myvm:~$ cat backupfile2
    a
    v
    g
    b
    z
    t
    man
    cse
    ```
    
    * **✅ Use case:**
        
        * Useful for backups where you want multiple names pointing to the same data.
            
        * Saves space because no duplicate data is created.
            

**🆚 Summary: Soft Link vs Hard Link**

Example: Imagine you have a **room** in your house where you keep your **bike**.

* A **hard link** is like giving your friend a **duplicate key** to that room.
    
    * Both of you can open the same room.
        
    * Even if you lose your key, your friend can still access the bike.
        
* A **soft link** is like writing a **note** that says:  
    *“My bike is in Room 101.”*
    
    * If the room is moved or deleted, the note becomes useless
        

🟢 Hard link = Another key to the same room (file content)  
🟡 Soft link = A shortcut pointing to the room (file path)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753721313241/9618d01f-43c1-4eac-8fc5-40273a2c0383.png align="center")

* **What Does an Inode Store?**
    
    * In Linux, an **inode** (index node) is a data structure used by the file system to store information about a file or directory **except its name and actual data**.
        
    * Each file or directory has an inode that contains:
        
        * File type (regular file, directory, etc.)
            
        * Permissions (read, write, execute)
            
        * Owner and group
            
        * File size
            
        * Timestamps (created, modified, accessed)
            
        * Number of hard links
            
        * Pointers to data blocks (where the actual file content is stored
            
* Remove file content: `> file1`
    

```plaintext
//viewing the content of file3
azureuser@myvm:~$ cat file3
content of file

//removing the content of the file3
azureuser@myvm:~$ >file3
azureuser@myvm:~$ cat file3
```

---

## **🗜️ Archiving and Compression**

* **Archive files**: `tar -cvf dirX.tar dirX`
    
    * `tar` is an archiving tool used to combine multiple files or directories into one.
        
    * `-cvf` stands for:
        
        * `c`: create a new archive
            
        * `v`: verbose mode (shows the progress in the terminal)
            
            * Example:
                
                ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753707776747/fe2d15ec-1125-4973-a432-05aec3a2bcb1.png align="center")
                
        * `f`: specifies the filename of the archive
            
    * `dirX.tar` is the name of the archive file that will be created.
        
    * `dirX` is the name of the directory (or file) you want to archive.
        

```plaintext
azureuser@myvm:~$ tar -cvf dirX.tar dirX
dirX/
dirX/dirY/
dirX/dirY/dirZ/
dirX/dirY/dirZ/file3
```

* > **Note:** The `.tar` file is just an archive, not compressed by default. It is treated as a regular file by the system, not as a directory.
    > 
    > Example: -rw-rw-r-- 1 azureuser azureuser 10240 Jul 28 13:01 dirX.tar
    

```plaintext
azureuser@myvm:~$ ls -l
total 2
drwxrwxr-x 3 azureuser azureuser  4096 Jul 28 12:58 dirX
-rw-rw-r-- 1 azureuser azureuser 10240 Jul 28 13:01 dirX.tar
```

* Compress a file: `gzip dirX.tar`
    
    * Reduce file size
        
    * `gzip` compresses the file `dirX.tar` and replaces it with a new file named `dirX.tar.gz`.
        
    * The original `dirX.tar` file is removed by default after compression
        

```plaintext
azureuser@myvm:~$ gzip dirX.tar
azureuser@myvm:~$ ls -l
total 2
drwxrwxr-x 3 azureuser azureuser 4096 Jul 28 12:58 dirX
-rw-rw-r-- 1 azureuser azureuser  197 Jul 28 13:01 dirX.tar.gz
```

* Unzip a file: `gunzip dirX.tar.gz`
    
    * This command will decompress the `dirX.tar.gz` file and leave you with `dirx.tar`, which is still an archive
        
    * The original `dirX.tar.gz` file is removed by default after decompression
        

```plaintext
azureuser@myvm:~$ gunzip dirX.tar.gz
azureuser@myvm:~$ ls -l
total 2
drwxrwxr-x 3 azureuser azureuser  4096 Jul 28 12:58 dirX
-rw-rw-r-- 1 azureuser azureuser 10240 Jul 28 13:01 dirX.tar
```

* Extract a tar file: `tar -xvf dirX.tar`
    
    * To extract the contents of a `.tar` archive
        
    * `x`: extract the archive
        
    * `v`: verbose mode (shows progress)
        
    * `f`: specifies the archive file name
        
    
    > This command will extract all files and directories from `dirx.tar` into the current directory.
    

```plaintext
azureuser@myvm:~$ tar -xvf dirX.tar
dirX/
dirX/dirY/
dirX/dirY/dirZ/
dirX/dirY/dirZ/file3
```

* **Download a file from the web**: `wget https://www.pdfdrive.to/dl/a-programmers-guide-to-the-mind`
    
    * `wget` is a command-line utility used to download files from the web.
        
    * `https://www.pdfdrive.to/dl/a-programmers-guide-to-the-mind` is the actual URL of the file to download.
        
    * The file will be saved in your current working directory
        

```plaintext
azureuser@myvm:~$ wget https://www.pdfdrive.to/dl/a-programmers-guide-to-the-mind
azureuser@myvm:~$ ls
 a-programmers-guide-to-the-mind
```

---

## **🔐 File Permissions in Linux**

Linux is a multi-user operating system, and managing file access is crucial for security and collaboration. In this post, we’ll explore how to control file and directory permissions using commands like `chmod`, `chown`, and `chgrp`.

**Access Modes:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1753710495100/1124bf90-3f83-4654-8707-582fb18853aa.png align="center")

**🔍 Example of File Permission Format**

In Linux, file ownership and permissions are divided into three parts:

* **User (Owner)** – The first set of `rw-` means the owner of the file can **read** and **write** it.
    
* **Group** – The second set of `rw-` means users in the same group can also **read** and **write** the file.
    
* **Others** – The last set of `r--` means all other users can only **read** the file.
    
* `-` → It's a file (not a directory)
    
* **Note:** The first `azureuser` is the **owner**, and the second `azureuser` is the **group**.
    

```plaintext
-rw-rw-r-- 1 azureuser azureuser     0 Jul 28 13:53 file1
```

**🛠️ How to Set Permissions Using chmod**

**Example:**

Old Permission of file : rw- rw- r--

New Permission of the file to be provided : rwx r-x r--

* for owner: rwx
    
* for group: r-x
    
* for others: r--
    

**Method 1:** Numeric Mode

Each permission is represented by a number:

`rwx` = 4 + 2 + 1 = **7**

`r-x` = 4 + 0 + 1 = **5**

`r--` = 4 + 0 + 0 = **4**

To apply these permissions to a file

```plaintext
azureuser@myvm:~$ chmod 754 file1
azureuser@myvm:~$ ls -l
total 1
-rwxr-xr-- 1 azureuser azureuser     0 Jul 28 13:53 file1
```

**Method 2:** Symbolic Mode

`u` → user (owner)

`g` → group

`o` → others

`+` → add permission

`-` → remove permission

`=` → set exact permission

u = u-wx (

g = g+w

o= wx

```plaintext
azureuser@myvm:~$ chmod u-wx,g+w,o=wx file1
```

**Method 3:** Assigning Specific Permissions

```plaintext
azureuser@myvm:~$ chmod u+r,g+rwx,o+x file1
```

**🔄 How to Change Ownership**

Before assigning ownership, make sure the file or directory exists and that you have the necessary permissions to change its owner

* **Change Owner:** `sudo chown pankaj file1`
    
    * before assigning owner: `azureuser`
        
    * ```plaintext
            azureuser@myvm:~$ ls -l
            total 1
            -r--rwx-wx 1 azureuser azureuser     0 Jul 28 13:53 file1
        ```
        
    * after assigning owner: `pankaj`
        
        ```plaintext
        azureuser@myvm:~$ sudo chown pankaj file1
        azureuser@myvm:~$ ls -l
        total 1
        -r--rwx-wx 1 pankaj    azureuser     0 Jul 28 13:53 file1
        ```
        
* **Change Group:**
    
    * before assigning group: `azureuser`
        
        ```plaintext
        azureuser@myvm:~$ ls -l
        total 1
        -r--rwx-wx 1 pankaj    azureuser     0 Jul 28 13:53 file1
        ```
        
    * before assigning group: `cse`
        
        ```plaintext
        azureuser@myvm:~$ sudo chgrp cse file1
        azureuser@myvm:~$ ls -l
        total 1
        -r--rwx-wx 1 pankaj    cse           0 Jul 28 13:53 file1
        ```
        

**Remove all permissions:**

* `chmod 000 file1`
    
    * result will show: ----------
        
    
    ```plaintext
    azureuser@myvm:~$ sudo chmod 000 file1
    azureuser@myvm:~$ ls -l
    total 1
    ---------- 1 pankaj    cse           0 Jul 28 13:53 file1
    azureuser@myvm:~$ cat file1
    cat: file1: Permission denied
    ```
    

---

## **🔁 Miscellaneous**

* **Restart system**: `sudo reboot`
    
    ```plaintext
    azureuser@myvm:~$ sudo reboot
    ```
    
* **🌳View directory structure:**
    
    Sometimes, you want to see the entire folder structure of a directory in a visual format. The `tree` command is perfect for this!
    
    * Step 1: Install `tree` : If it's not already installed, you can install it using:
        
        ```plaintext
        azureuser@myvm:~$ sudo apt install tree
        ```
        
    * **Step 2: Use** `tree` to View Directory Structure
        
        ```plaintext
        azureuser@myvm:~$ tree
        .
        ├── backupfile2
        ├── dir1
        ├── dir2
        ├── dir3
        ├── dir4
        │   └── dir5
        │       └── dir6
        ├── dirX.tar
        6 directories, 2 files
        ```
        
    * to see specific directory
        
        ```plaintext
        azureuser@myvm:~$ tree dir4
        dir4
        └── dir5
            └── dir6
        ```
        
    
    **🃏Using Wildcards in Linux**
    
* Wildcards are special characters that help match filenames or patterns. One common use is with the `cat` command to read files that follow a naming pattern.
    
    **Example:** View OS Release Info : `cat /etc/os-rel*`
    
    * `*` is a wildcard that matches any characters.
        
    * This command reads all files starting with `os-rel` in the `/etc` directory.
        
    * Typically, it displays the content of `/etc/os-release`, which contains information about your Linux distribution.
        
    
    ```plaintext
    azureuser@myvm:~$ cat /etc/os-rel*
    PRETTY_NAME="Ubuntu 22.04.5 LTS"
    NAME="Ubuntu"
    VERSION_ID="22.04"
    VERSION="22.04.5 LTS (Jammy Jellyfish)"
    VERSION_CODENAME=jammy
    ID=ubuntu
    ID_LIKE=debian
    HOME_URL="https://www.ubuntu.com/"
    SUPPORT_URL="https://help.ubuntu.com/"
    BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
    PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
    UBUNTU_CODENAME=jammy
    ```
    
    **🧠 Final Thoughts**
    
    This guide covered the most essential Linux commands every DevOps engineer or beginner should know. From creating files and managing directories to handling users, permissions, and packages, these commands form the foundation of working efficiently in a Linux environment. Whether you're just starting out or brushing up your skills, mastering these commands will help you navigate and manage Linux systems with confidence.
    
    \- - -
    
    *\- Written by Pankaj Roy | DevOps & Cloud Enthusiast*