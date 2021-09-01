# Linux Lab 5 Task

## Using sed utility

1- Display the lines that contain the word “lp” in /etc/passwd file.

```bash
sed -n 's:lp:&:p' < /etc/passwd
```

2- Display /etc/passwd file except the third line.

```bash
sed '3d' < /etc/passwd
```

3- Display /etc/passwd file except the last line.

```bash
sed '$d' < /etc/passwd
```

4- Display /etc/passwd file except the lines that contain the word “lp”.

```bash
sed ':Ip:d' < /etc/passwd
```

5- Substitute all the words that contain “lp” with “mylp” in /etc/passwd file.

```bash
sed -n 's:lp:mylp:' < /etc/passwd
```

## Using awk utility

1- Print full name (comment) of all users in the system.  ***

```bash
awk -F: '{print $5}' < /etc/passwd
```

2- Print login, full name (comment) and home directory of all users.( Print each line preceded by a line number)

```bash
awk -F: '{print NR " "  $1 , $5 , $7}' < /etc/passwd
```

3- Print login, uid and full name (comment) of those uid is greater than 500

```bash
awk -F: '$4 > 500 {print " "  $1 , $5}' < /etc/passwd
```

4- Print login, uid and full name (comment) of those uid is exactly 500

```bash
awk -F: '$3 ~ /1000/ {print " " $3,  $1 , $5}' < /etc/passwd
```

5- Print line from 5 to 15 from /etc/passwd

```bash
awk 'NR>4&&NR<16 {print NR " " $0}' < /etc/passwd
```

6- Get the sum of all accounts id’s.

```bash
awk -F: '{sum += $3} END {print sum}' < /etc/passwd
```

---------------------------------------

1. Write a script called mycase, using the case utility to checks the type of character entered by a user:
	a. Upper Case.
	b. Lower Case.
	c. Number.
	d. Nothing.

```bash
#!/bin/bash

while true; 
do
	echo "Enter a character : "
	read C 

	if [[ $C =~ [A-Z] ]];
	then
		echo "Upper Case";
	elif [[ $C =~ [a-z] ]];
	then
		echo "Lower Case";
	elif [[ $C =~ [0-9] ]];
	then
		echo "Number";
	else
		echo "Nothing";
	fi
done
```

2. (Optional, Can be skipped)Enhanced the previous script, by checking the type of string entered by a user:
	a. Upper Cases.
	b. Lower Cases.
	c. Numbers.
	d. Mix.
	e. Nothing.
3. Write a script called mychmod using for utility to give execute permission to all files and directories in your home directory.

```bash
#!/bin/bash

sudo chmod -R +x ~/*
```

4. Write a script called mybackup using for utility to create a backup of only files in your home directory.

```bash
#!/bin/bash

# create a backup file
BACKUP_FILE="home.bak.tar"
touch extrafile.extra
tar cf $BACKUP_FILE extrafile.extra
rm extrafile.extra

for FILE in ~/*; 
do 
	echo $FILE;
	if test -f "$FILE" ; 
	then
		echo $FILE is a file
		tar rf $BACKUP_FILE $FILE
	fi 
done
```

5. Write a script called mymail using for utility to send a mail to all users in the system. Note: write the mail body in a file called mtemplate.

```bash
#!/bin/bash

if [ -z "$1" ];
then
    echo You did not supply a subject for the message.
    exit 1
else
    set subject=$1
fi

MAIL_TEMPLATE="mtemplate.txt"
if [ ! -f "$MAIL_TEMPLATE" ] 
then
   echo Mail Template does not exist.
   exit 3
fi
   

for user in $( awk -F: '{ print $1 }' /etc/passwd | tail +17 ); 
do
    # Mail the file
    echo Mailing to $user
    mail -s $subject $user < $MAIL_TEMPLATE
   
    sleep 2
done
```

6. Write a script called chkmail to check for new mails every 10 seconds. Note: mails are saved in /var/mail/username.

```bash
#!/bin/bash

COUNTFILE="./mailsCount.txt"
if [ ! -f  $COUNTFILE ]; 
then 
	touch $COUNTFILE
	echo 0 > $COUNTFILE
fi

PREV=$(cat $COUNTFILE)

if [ -f /var/mail/$USER ];
then
	MAILBOX=/var/mail/$USER
elif [ -f /var/spool/mail/$USER ];
then 
	MAILBOX=/var/spool/mail/$USER
else 
	echo "You don't have a mail file."
	exit 3
fi

CURRENT=$(grep "Message-Id:" $MAILBOX | wc -l | cut -d " " -f1)

echo $CURRENT > $COUNTFILE

if [ $CURRENT -ne $PREV ]; 
then
	echo "You've Got Mail!"
else
	echo "You didn't get any new mails"
fi
```

7. Create the following menu:
	a. Press 1 to ls
	b. Press 2 to ls –a
	c. Press 3 to exit
Using select utility then while utility.

```bash
#!/bin/bash

select opt in 1 2 3; 
do
	case $opt in 
		1)
			ls 
			;;
		2)
			ls -a
			;;
		3)
			exit 0
			;;
		*) 
			echo "Invalid Option"
			;;
	esac
done
```

8. Write a script called myarr that ask a user how many elements he wants to enter in an array, fill the array and then print it.

```bash
#!/bin/bash

read n 

declare -a arr=()

for i in $n; 
do
	read x
	arr+=($x)
done

for i in "${arr[@]}"; 
do
	echo $i
done
```

9. Write a script called myavg that calculate average of all numbers entered by a user. Note: use arrays

```bash
#!/bin/bash

read n 

declare -a arr=()
sum=0
for i in $n; 
do
	read x
	arr+=($x)
	
done

for i in "${arr[@]}"; 
do
	sum=$(($sum+$i))
done

echo "AVG : " $(($sum / ${#arr[@]}))
```
