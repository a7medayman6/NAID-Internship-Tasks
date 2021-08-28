# Linux Lab 4 Task

- What is the option used to view the content of a compressed file.
```bash
tar -t file.tar
```

- Backup /etc directory using tar utility.
```bash
sudo tar -cvf etc-backup.tar /etc/
```

- List the inode numbers of /, /etc, /etc/hosts.
```bash
ls -i /
ls -i /etc
ls -i /hosts
```

- Copy /etc/passwd to your home directory, use the commands diff and cmp, and Edit in the file you copied, and then use these commands again, and check the output.
```bash
cd 
cp /etc/passwd .
echo "new imaginary user..." >> passwd
diff passwd /etc/passwd
cmp passwd /etc/passwd
```
- Create a symbolic link of /etc/passwd in /boot.
```bash
sudo ln -s /etc/passwd /boot/
```

- Create a hard link of /etc/passwd in /boot. Could you? Why?
	- can't because hard links must exist in the same device.
