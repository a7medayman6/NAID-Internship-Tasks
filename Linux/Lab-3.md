# Lab 3 Task

1. 1. Create a user account with the following attribute
	username: islam
	Fullname/comment: Islam Askar
	Password: islam
```bash
sudo useradd -p islam -c "Islam Askar" islam
```

2. Create a user account with the following attribute
	Username: baduser
	Full name/comment: Bad User
	Password: baduser
```bash
sudo useradd --badname -p baduser -c "Bad User" baduser
```

3. Create a supplementary (Secondary) group called pgroup with group ID of 30000
```bash
sudo groupadd -g 30000 pgroup
```

4. Create a supplementary group called badgroup
```bash
sudo groupadd badgroup
```

5. Add islam user to the pgroup group as a supplementary group
```bash
sudo adduser islam pgroup
```

6. Modify the password of islam's account to password
```bash
sudo passwd islam
```

7. Modify islam's account so the password expires after 30 days
```bash
sudo chage -M 30 islam
```

8. Lock bad user account so he can't log in
```bash
passwd -l baduser
```

9. Delete bad user account
```bash
sudo userdel baduser
```

10. Delete the supplementary group called badgroup.
```bash
groupdel badgroup
```

13. Create a folder called myteam in your home directory and change its permissions to read only for the owner.
```bash
mkdir myteam
chmod o=r myteam
```

14. Log out and log in by another user
```bash
exit
su - islam
```

15. Try to access (by cd command) the folder (myteam)
```bash
cd myteam/
bash: cd: myteam/: Permission denied
```

16. Using the command Line
	Change the permissions of oldpasswd file to give owner read and write permissions and for group write and execute and execute only for the others (using chmod in 2 different ways)
	Change your default permissions to be as above.
	What is the maximum permission a file can have, by default when it is just created? And what is that for directory.
	Change your default permissions to be no permission to everyone then create a directory and a file to verify.

```bash
sudo chmod o=rw g=rx o=x oldpasswd
sudo chmod 651
```
- 666 for files and 777 for directories 
```bash
sudo chmod -rwx oldpasswd
```
17. What are the minimum permission needed for:
	Copy a directory (permission for source directory and permissions for target parent directory)
	Copy a file (permission for source file and and permission for target parent directory)
	Delete a file
	Change to a directory
	List a directory content (ls command)
	View a file content (more/cat command)
	Modify a file content
```bash

```
18. Create a file with permission 444. Try to edit in it and to remove it? Note what happened.
```bash
mkdir dir 
chmod 444 dir
cd dir
bash: cd: dir/: Permission denied
rm -r dir
rm: remove write-protected directory 'dir/'? y 
```

19. What is the difference between the “x” permission for a file and for a directory?
- for the files it means the right to execute it if it's a program
- for a directory it means the right to enter the directory i.e., cd dir

20. Issue the command "sleep 100" in background.
```bash
sleep 100
```
21. Kill the sleep command.
```bash
killall -9 sleep
```
22. Display your processes only
```bash
ps
```
23. Display all processes except yours
```bash
ps u -U $USERNAME -N
```
24. Use the pgrep command to list your processes only

```bash
pgrep -u $USERNAME
```
