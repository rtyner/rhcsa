# Understanding `umask`

1. View current umask permissions and then, for the current shell session, set umask permissions to 0.
2. Navigate to the /tmp directory and touch file1 and mkdir dir1. View current permissions.
3. Mask permissions for the "other" users to write a file when created, then touch file2 and view permissions.
4. Mask write access for group members and the write for "other" permissions, then touch file3 and view permissions.
5. Mask read and write permissions for the owner of a file, then touch file4 and mkdir dir3 and view permissions.
6. Mask all permissions, including execute permissions, on new directories, then touch file5.
7. Mask read/write access for group for non-privileged users and other permissions and make these changes persistent.

####

1. `umask`
2. 
