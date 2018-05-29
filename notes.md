![alt text](https://seeklogo.com/images/R/redhat-logo-259A623E59-seeklogo.com.png)
# Red Hat Certified System Administrator
[Exam Objectives](https://www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-rhcsa-exam "Exam Objectives")

#### **Reading Man Pages**
  * [] - optional
  * __ - required
  * ... - multiple files

#### **Input and Output Redirection**
  * \> - redirect and overwrite
  * \>> - appends file
  * 2> - redirect stderr to something and hide from stdout
    * 2 represents error
  * 2>&1 - redirects stderr to stdout
    * can be used as input with |
  * /dev/null - redirect here to dump into nothingness
  * `head` - first 10 lines to stdout
    * ex. head messages - first 10 lines of messages file
  * `tail -f` - continue appending as it's added to the file

#### **Using grep and regex to Analyze Text**
  * `grep '^#' /etc/ssh/sshd_config`
    * ^ - means to search for lines that start with #
    * searches that file and looks for lines that start with #
  * `grep -i 'rsaauth' /etc/ssh/sshd_config`
    * -i - ignore case
    * finds all occurances of rsaauth, ignoring case
  * `grep -v '^#' file`
    * -v - inverse
    * searches for every line that **DOESN'T** start with #
  * `grep 'world$' file`
    * $ - line ends with
    * searches for all lines that end with world
  * `grep [Ll]inuxacademy file`
    * [] - allows for multiple arguments
    * searches for lines that start with capital and lowercase L
  * `grep '[^linux] file`
    * [^linux] - when the carat is in [] it means to negate the following text
    * searches for everthing that does not include an l, i, n, u, or x.
  * `grep -E '(a)+' file`
    * -E runs egrep
    * searches for the occurance of 'a' as many times as it appears
  * `grep 'l...x' file`
    * 'l...x' - ... symbolizes any character
    * searches for a pattern that starts with l and ends with x with 3 characters inbetween them
  * basic and extended regular expressions
    * ? + { [ | () . * ^ $
    * ? - preceeding item is optional and matched once at most
    * \+ - preceeding item is matched one or more times

#### Accessing Remote Systems Using SSH 
  * ssh config - /etc/ssh_config
    * PermitRootLogin - allows the root user to login via ssh - commented out by default
      * best practice to disable because an attacker would need to compromise regular user to login, then gain root permissions
  * always restart `ssh` service - `systemctl restart sshd`
  * issue commands to remote server
    * `ssh user@hostname ls` - this will run ls on user's home directory
  * `scp` - file transfer that uses `ssh` protocol
    * `scp file.txt user@hostname:~/dir`
      * this will transfer file.txt to the remote server and put it in user's ~/dir directory
  * `sftp`
    * this is just `ssh` with `get` and `put` commands

#### Login and Switch Users in Multiuser Targets
  * multiuser target - multiple users on same system
  * `su` - switch user to interactive shell
  * `su - `, `su -l`, `su --login` - switch user to login shell
  * interactive shell v. login shell - login shell will load custom configs and profiles
    * .bash_logout - when user logs out, everything in this file is executed
    * bash_profile - contains customazions for your login shell, PATH, aliases, etc
    * bashrc - contains customizations for interactive shell
    * /etc/profile - global bash_profile

#### Archive, Compress, Unpack, and Uncompress Files using `tar`, `star`, `gzip`, and `bzip2`
  * `tar` - allows for creation and compression of archives
  * `gzip filename` - zips a file
  * `gunzip` or `gzip -d` - unzips file
  * compress directory and contents
    * need to create an archive first
      * `tar -cvf archive.tar dir1\ hello1 hello2`
        * c - create archive
        * v - verbosly
        * f - specify name of archive
    * `gzip archive.tar`
  * compress directory and contents w/ only `tar`
    * `tar -cvzf archive.tar.gz dir1/ hello1 hello2`
      * z - run through `gzip`  
  * list files within an archive
    * `tar -tf archive.tar`
  * compress directory and contents w/ `tar` and `bzip`
    * `tar -cvjf archive.tar.gz dir1/ hello1 hello2`
      * j - run through `bzip`  
  * extract a `tar` archive
    * `tar -xvf archive.tar`
      * x - extract
  * extract tar<span>.gz 
    * `tar -xzvf archive.tar.gz` 
  * <mark>if you extract an archive into a directory that contains files of the same name, the extracted files will overwrite what's in the directory</mark>
  * show differences between archived files and files in a directory
    * `tar -dvf archive.tar.gz`
      * d - shows difference between archive and current directory
  * view compression information of a `gzip` archive
    * `gzip -l archive.gz`
  * `star` - used for large datasets, making sure to not overwrite updated files
    * can use the `find` command to extract specific files from an archive
  * creating an archive with `star`
    * `star -c -f=archive.tar dir1\ hello1 hello2`
      * c - create archive
      * f - filename
  * list contents of archive with `star`
    * `star -t -f=archive.tar`
      * t - lists files in archive
  * extract archive with `star`
    * `star -x -f=archive.tar`
  * extract single file named hello1 from archive
    * `star -x -f=archive.tar hello1`

#### Create and Edit Text Files
  * `vim` is the only option here, `nano` is for virgins
  * cw - change word
  * cc - remove line and enter insert mode
  * R - replace mode - writes over existing text
  * replace first occurance of line with word
    * :%s/line/word
  * replace all occurances of line with word
    * :%s/line/word/g - g is global
  * `ls` inside current directory from within `vim`
    * :!`ls`
  * `ls` /etc/ from within `vim`
    * :!`ls /etc/`

#### Create, Delete, Copy, and Move Files and Directories
  * create directories recursively
    * `mkdir -p new-dir/dir1/dir2`
      * p - create parent directories 
  * `rmdir` - removes directories but not recursively

#### Create Hard Links and Soft Links
  * `ln` - creates symbolic and hard links
   * by default will create a hard link
  * soft links   
    * `ln -s /etc/motd motd`
      * creates a soft link from /etc/motd to motd in current directory
      * s - soft link
    * soft links will be broken if source target is moved/removed
    * symbolic links can link across filesystems
    * soft links are similar to shortcuts
    * permission are inheritied from source file, symlink permissions do not matter
  * hard links
    * link directly to a specific inode location on a filesystem
    * cannot link across filesystems
    * when permissions are changed on one hard link target it's applied to the other as well

#### List, Set, and Change Standard UGO/RWX Permissions
  * first bit is file/dir/symlink
    * d is dir
    * - is file
    * l is symlink
  * after that groups of 3 are used
    * first 3 are owner
    * second 3 are group
    * last 3 are other, everyone else on the system
  * rwx - read, write, execute
    * x - allows for execution of scripts
  * permissions are changed with `chmod`
    * octal or symbolic notation
    * `chmod u+x` - gives user execute permissions
    * `chmod u-x` - removes execute permissions from user
    * `chmod g+x` - gives group execute permissions
    * `chmod u+wrx` = gives user rwx permissions 
  * add a group
    * `groupadd finance`
    * not in roots path, launched from /usr/sbin/groupadd
  * list groups
    * `getent group`
    * `cat /etc/group`
  * change owner (user and group) of an object
    * `chown user:group object`
  * change only group of an object
    * `chown :group object`
  * <mark>to navigate into a directory you need execute privileges</mark>
  * add a secondary group to a user
    * `usermod -G object user`
      * G - secondary group
    * user will need to logout for changes to take effect
  * grant a group write permissions for an object
    * `chmod g+w -R object`
    * g+w - grant write to group
    * R - recursively
  * log user into another group as primary group
    * `newgrp groupname`
  * only allow directories to have execute permissions
    * `chmod ug+X -R object`
      * X - this changes it so only directories have execute
    * this is good if you have scripts located in directories but don't want to mass allow the execution of them
  * grant permissions for everyone (user, group, and other)
    * `chmod a+r object`
      * a - grants to it user, group, and other
  * octal permissions
    * allows for the use of numeric notation to set permissions
    * `chmod 777`
      * first character is owner
      * second character is group owner
      * third character is other
    * 777 results in rwx for everyone
    * the bits add up to 7
      * read = 4
      * write = 2
      * execute = 1
    * `chmod 440 -R directory`
      * R - recursive
 * setuid and setgid
    * setgid is a permission bit
    * when you are to exectute or open a file a new process is forked as the user who is executing the file
    * setgid allows you to execute a file with the permissions of whoever owns the file, not who is executing it
    * sticky bit represents setuid, shown as s (user) and S (group) in `ls` permissions
    * essentially, setuid means execute this file with permissions of the owner of the file, not as the user executing the file
    * setgid means execute with permissions of the group that owns it
    * `chmod u+s file` - will run with same permissions as user who owns file 
    * `chmod g+s file` - will run with same permissions as group who owns the file
    * `chmod 4500 file` - 4 represensts setuid on the user
    * `chmod 2500 file` - 2 represents setgid on group
    * `chmod 6500 file` - 6 will setuid and setgid for both user and group
    * sticky bit - prevents unauthorized users from deleting or renaming a file 
      * `chmod +t file`
      * `chmod 1777 file`
        * 1 - set sticky bit
      * `chmod 7777 file` setuid, setgid, and stickybit (just add them together)

#### List, Set, and Change Standard UGO/RWX Permissions: `umask`
  * `umask` - stands for user mask, allows for the setting of default permissions
  * show default `umask` permissions with `umask`
  * `umask` sets permissions for current session, logout clears them
  * deafult is 0022
  * 2 sets of `umask` permissions - privileged users and non-privileged
  * default for a file is 666
  * default for a directory is 777
  * `umask` will never give execute permissions on a file - it will for a directory though

#### Locate, Read, and Use System Documentation with `man`, `info`, and /usr/share/doc
  * documentation can be from `man` page, from `--help`, from `info`, from /usr/share/doc, or within the `rpm`
  * `man 5 passwd` - opens page 5 of man page
  * <mark>`apropos passwd` - searches through all man pages, has to be cached though</mark>
  * <mark>`mandb` - indexes everything in /usr/share/mani</mark>
  * `info` - alternative to man pages
    * searches /usr/share/info
  * from within `info` hit ? to see navigation shortcuts
  * `info --apropos=tee` - searches `info` for `tee`
  * sometimes template config files will live here as well
  * `locate passwd` searches cached database of entire system for anything related to passwd
  * `updatedb` - updates `locate` cache
  * if `locate` isn't installed, install the `mlocate` package
  * `which passwd` - shows absolute path of program
  * `whatis passwd` shows man pages for program - searches descriptions
  * `whereis` - locates binary and source files for program
  * `rpm -qd packagename` queries document files for the specified program

#### Finding Files with `locate` and `find`
  * `locate` - searches cached files in a database, db is updated by `cron`
  * `updatedb` - updates locate cache
  * `find` - much more powerful and can be complicated
  * `find /etc -name motd` - searches /etc for ANYTHING with the name of motd
  * `find /etc -user root` - finds everything in /etc owned by root
  * `find / -mtime -3` - finds everything in / that have been modified in last 3 days
  * `find / -mtime +3` - finds everything in / that have been modified in a time greater than the last 3 days
  * `find / -uid 1002` - finds everything in / owned by user 1002
  * `find / -user jeff -type f` finds all FILES owned by jeff
  * `find / -user jeff -type f -exec cat {} \;` - finds all FILES owned by jeff and cats them
    * {} means perform the exec on each file
    * \; ends command
  * `find / -user jeff -type f -exec cp {} /home/mary \;` - finds all FILES owned by jeff and copies them to marys home directory 
  * `find /home/ -user jeff -type f exec rm {} \.` - finds all FILES owned by jeff and removes each file

#### Boot, Reboot, and Shutdown a System
  * newer rhel systems are using systemd as init system
  * `init 0` - runlevel 0, shutsdown the system
  * `init 6` - runlevel 6, restarts the system
  * `init` is the deprecated way of doing this
  * `reboot` - calls `systemctl reboot`
  * `shutdown`
    * -r - reboot
    * -p - powers off
    * `shutdown -r +5 System going down for reboot` - reboots system in 5 minutes with message displayed to users
    * `shutdown -c` - cancels reboot
    * `shutdown -r 00:00` - schedules reboot for 12AM (24hr time)
  * when system is being shutdown its having its target changed
  * targets replace runlevels in systemd
  * /usr/lib/systemd/system - default targets
  * physically poweroff a system
    * `systemctl poweroff`
    * `poweroff`
    * `shutdown -p`
  * `shutdown` is the proper way to handle power management and reboots

#### Boot Systems into Different Targets Manually
  * systemd has parallel bootup - can start multiple services at the same time
  * systemd unit config files are called targets
  * list available targets
    * `systemctl list-units --type=target`
  * list different target types
    * `systemctl -t help`
  * systemd unit config files
    * target config files 
  * unit config files are located in /usr/lib/systemd/system
  * instead of writing startup scripts you write systemd unit services
  * WantedBy - this is where you specify that your service is a dependency of a certain target
  * `systemctl list-dependencies multi-user.target` - list dependencies of multi-user target
  * `systemctl get-default` - lists current target
  * targets
    * multi-user.target - multiple users can be logged into the system, most likely terminal
    * graphical.target - GUI 
    * emergency.target - boots into root terminal with fs mounted read only 
    * rescue.target - launches single user environment with minimal resources to troubleshoot and resuce system
    * reboot.target
  * AllowIsolate - means move system into this target and load the dependencies
  * `systemctl isolate multi-user.target` - moves into multi-user target
  * `systemctl set-default multi-user.target` - sets default target to multi-user
  * default target is just symlink to specific target file
  * interrupt the boot process and enter emergency or rescue
    * interrupt at grub and edit linux16 kernel line
    * add systemd.unit=rescue.target to the end
    * continue boot
  * 










#### Misc. Notes
  * LVM
  * runlevels have been deprecated with systemd - replaced with targets
  * `awk`
  * `tee`
  * `stat file` - shows status of a file
  * `umask` - learn this, seems hard
  * `yum group list` - lists package groups
  * look up inodes
  * SUDO - Substitute User and DO
  * look into setuid and setgid
  * `history` \<ctrl-r> - allows searching through history
  * `touch {file1,file2,file3}` - create multiple files with {}
  * `systemctl get-default` - returns a target
  * by deafult RHEL7 aliases `rm` to `rm -i` to force deletion prompt

[comment]: <> (<mark></mark> highlights text) 
[comment]: <> (&#46; - period)
[comment]: <> (<span> to fuck hyperlinks)
