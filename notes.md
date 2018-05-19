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

#### Creat and Edit Text Files
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



#### Misc. Notes
  * `history` \<ctrl-r> - allows searching through history
  * `touch {file1,file2,file3}` - create multiple files with {}
  * `systemctl get-default` - returns a target
  * by deafult RHEL7 aliases `rm` to `rm -i` to force deletion prompt

[comment]: <> (<mark></mark> highlights text) 
[comment]: <> (&#46; - period)
[comment]: <> (<span> to fuck hyperlinks)
