# BANDIT-writeup
## level 0

**Level Goal** \
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

~~~
ssh bandit0@bandit.labs.overthewire.org -p 2220
password: bandit0
ls
file readme 
cat readme 
exit -d
~~~
`ssh` used for connecting to Linux servers remotely\
`ls` to list all files and directories\
`file` to show type of file\
`cat` reading a file\
`exit` to exit the server\
On using `cat readme`, you get a string which is the password for the next level.

The password for the next level is: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

## level 1

**Level Goal** \
The password for the next level is stored in a file called - located in the home directory
~~~
ssh bandit1@bandit.labs.overthewire.org -p 2220
cat ./- 
exit -d
~~~

Initially, I tried `cd -`, which gave me the error\
**OLDPWD not set** \
On adding `./` before the '-', I got the right output. `./` is used to execute a compiled program in the current directory. Here, it implies '-' is a file name in the directory.

The password for the next level is: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

## level 2
**Level Goal**\
The password for the next level is stored in a file called spaces in this filename located in the home directory
~~~
ssh bandit2@bandit.labs.overthewire.org -p 2220
ls
cat spaces in this filename
cat spaces\ in\ this\ filename 
exit -d
~~~

Initially, `cat spaces in this filename` gave me the wrong output as it considered each word as a file, which it isnt. On using escape character '/' after each word, it considered the whole thing as the file name, giving us the password. 

The password for the next level is: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

## level 3
**Level Goal** \
The password for the next level is stored in a hidden file in the inhere directory.
~~~
ssh bandit3@bandit.labs.overthewire.org -p 2220
ls
cd inhere
ls 
ls -a 
cat .hidden 
exit -d
~~~

The command `cd` is used to change directory. Using `ls` here gave us nothing as the file with the password is hidden. So, we used `ls -a`. `ls -a` will list all files, including hidden files.

The password for the next level is: 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

## level 4
**Level Goal** \
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.
~~~
ssh bandit4@bandit.labs.overthewire.org -p 2220
ls
cd inhere
ls
file ./-file0* 
cat ./-file07
exit -d
~~~

`./` here implies that -file00 is the name of a file in the directory, and not a command or option. 
Since we have so many files to search and find out which is the ASCII file, it is impractical to use file command on each file. We use `file ./-file0* `. Since all files share a similar name with the only difference being the number at *, the * will continue putting random numbers and running the command, and thus we can search all of them in one go.

The password for the next level is: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

## level 5
**Level Goal** \
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable\
1033 bytes in size\
not executable

~~~
ssh bandit5@bandit.labs.overthewire.org -p 2220
ls
cd inhere
find - type f - size 1033c
exit -d
~~~

The `find` command is used to search for files in a directory. \
`find -type` specifies the type of file to search for, which in our case is 'f' or 'regular file'. `- size` searches for files based on size. 'c' is for bytes.

The password for the next level is: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

## level 6
**Level Goal** \
The password for the next level is stored somewhere on the server and has all of the following properties:

owned by user bandit7\
owned by group bandit6\
33 bytes in size

~~~
ssh bandit6@bandit.labs.overthewire.org -p 2220
find / -user bandit7 -group bandit6 -size 33c
cat /var/lib/dpkg/info/bandit7.password
exit -d 
~~~

`find -user` lets us search for all files owned by a user. `-group` searches for files owned by a group.

The password for the next level is: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

## level 7
**Level Goal** \
The password for the next level is stored in the file data.txt next to the word millionth

~~~
ssh bandit7@bandit.labs.overthewire.org -p 2220
ls
cat data.txt | grep -i millionth
exit -d
~~~

the `grep` command is used to print lines that match patterns. ` -i` enables to search for a string case insensitively in the given file.
Pipe `|` is used to send the output of one command to another.

The password for the next level is: TESKZC0XvTetK0S9xNwm25STk5iWrBvP

## level 8
**Level Goal** \
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

~~~
ssh bandit8@bandit.labs.overthewire.org -p 2220
ls
sort data.txt | uniq -c
exit -d
~~~

The `sort` command is used to sort lines of text files.\
The `uniq` command is used to  report or omit repeated lines. `-c` prefix lines by the number of occurrences. The only line with a count of '1' is the password.

The password for the next level is: EN632PlfYiZbn3PhVK3XOGSlNInNE00t

## level 9
**Level Goal** \
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
~~~
ssh bandit9@bandit.labs.overthewire.org -p 2220
ls
strings data.txt | grep ^=
exit -d
~~~
It is stated that the password is stored in human readable format (strings) in data.txt. Thus, I used `strings data.txt` to find all strings in that file. Using `|`, I used its output on the `grep` command, which let me single out all files which begin with '='.
This gave me multiple matches but only one with the password format, and thus thats the password.

The password for the next level is: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

## level 10
**Level Goal** \
The password for the next level is stored in the file data.txt, which contains base64 encoded data
~~~
ssh bandit10@bandit.labs.overthewire.org -p 2220
ls
base64 data.txt --decode
exit -d
~~~
The `base64` command lets you base64 encode/decode data and print to standard output. Here, `base64 --decode` has been used to decode the file data.txt.

The password for the next level is: 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

## level 11
**Level Goal** \
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
~~~
ssh bandit11@bandit.labs.overthewire.org -p 222
ls
cat data.txt | tr 'a-z' 'n-za-m' | tr 'A-Z' 'N-ZA-M'
~~~
The `tr` command is used to transform and produce a modified output. In this case, `'a-z'` means modify all characterss between a to z and `'n-za-m'` shifts it by 13. n-z stands for the 13th letter from a to the last (z), and a-m is first letter to the one just before n (i.e m,12). This way, all 26 letters have been included. Simply repeat this for 'A-Z'. 

The password for the next level is: JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

## level 12
**Level Goal** \
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

~~~
ssh bandit12@bandit.labs.overthewire.org -p 2220
mkdir /tmp/b12
cp data.txt /tmp/b12
cd /tmp/b12
xxd -r data.txt > bandit
file bandit
~~~
The hint mentioned that the file data.txt is a hexdump. So, we use `xxd -r` which is used to reverse a hexdump.\
To move ahead, I checked the file type and it produced the output\
**bandit: gzip compressed data**\
So, we decompress it using;
~~~
mv bandit bandit.gz
gzip -d bandit.gz
file bandit
~~~
As it had been compressed multiple times, we check the file type again and it gives the output:\
**bandit: bzip2 compressed data**\
We decompress it using;
~~~
mv bandit bandit.bz2
bzip2 -d bandit.bz2
file bandit
~~~
Check file type \
**bandit: gzip compressed data**\
and decompress.

Repeat this process till the file is in human readable form.
<img width="565" alt="Screenshot 2024-02-09 215917" src="https://github.com/saanvivi/BANDIT-writeup/assets/145047724/32971fbd-f847-4b6b-9e5e-3173807fe1cd">
<img width="558" alt="Screenshot 2024-02-09 220342" src="https://github.com/saanvivi/BANDIT-writeup/assets/145047724/ba10b3b5-f3c9-4d9b-a356-06fb9b6ea375">

Now that the file is in ASCII format,  the password can be read directly from it.
~~~
cat data8
exit -d
~~~
Commands used:\
`gzip -d` or `gunzip` or `zcat`: To restore gzip compressed files.\
`bzip2 -d` or `bunzip2`: Decompresses files compressed using bzip2.\
`tar -xvf`: Extracts files from archives. `-x` extracts files from an archive. `-v'` displays verbose output during the extraction process and `-f` specifies the filename of the archive.

The password for the next level is: wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

## level 13
**Level Goal** \
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on
~~~
ssh bandit13@bandit.labs.overthewire.org -p 2220
ls
ssh -i sshkey.private bandit14@localhost -p 2220
~~~
We're now in bandit14
~~~
cat /etc/bandit_pass/bandit14
exit -d
~~~
On running `ls` command, we get the sshkey.private file. The `ssh` command is used to securely log into a remote machine and execute commands on that machine. To do so, we need the private key, which we have supplied, the host, username, and port. `-i` allows us to  specify the file. This is particularly useful when you have multiple identity files or need to use a specific file for authentication.  

The password for the next level is: fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

## level 14
**Level Goal** \
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
~~~
ssh bandit14@bandit.labs.overthewire.org -p 2220
nc localhost 30000
~~~
The command `netcat` or `nc` is used for reading and writing data between two computer networks. Here, we used it to write to port 30000 on locahost. The data sent was the password from the previous level. The command gave an output contaning the password for the next level. 

The password for the next level is: jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

## level 15
**Level Goal** \
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…
~~~
ssh bandit15@bandit.labs.overthewire.org -p 2220
ncat --ssl localhost 30001
~~~
First I used `man nc | grep ssl` to see if I could find anything about that. No output. I then tried running the same command using `ncat` which showed me how to use `--ssl` to encrypt the message as ssl, similar to how I did it in the previous level. On writing the password to this level, it returns the password to the next level. 

The password for the next level is: JQttfApK4SeyHwDlI9SXGR50qclOAil1

## level 16
**Level Goal** \
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
~~~
ssh bandit16@bandit.labs.overthewire.org -p 2220
nmap -sV --version-light -v -p 31000-32000 localhost
~~~
<img width="508" alt="Screenshot 2024-02-04 200908" src="https://github.com/saanvivi/BANDIT-writeup/assets/145047724/ad26b754-e6ad-4045-916d-89d1b07a3c3e">

Two ports running ssl, one echo n one unknown. On checking both, I found that 31790 is the one that returned an RSA Private key.

<img width="467" alt="Screenshot 2024-02-09 221926" src="https://github.com/saanvivi/BANDIT-writeup/assets/145047724/c234a4a8-ae9c-4024-b919-ab58cdfe5173">

~~~
mkdir /tmp/b14
cd /tmp/b14
nano bkey.key
chmod 400 bkey.key
ssh -i bkey.key bandit17@localhost -p 2220
~~~
I created a new directory and file to store the RSA key in. Using `chmod` I changed the permissions so that it can be used. Then, I used the bkey.key file which now stored my ssh key to login to bandit 17. Now that I'm in bandit17, I used `cat /etc/bandit_pass/bandit17` to get the credentials.

The password for the next level is: VwOSWtCA7lRKkTfbr2IDh6awj9RNZM5e

## level 17
**Level Goal** \
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19
~~~
ssh bandit17@bandit.labs.overthewire.org -p 2220
diff passwords.old passwords.new
exit -d
~~~
The `diff` command compares files line by line. It was used to see what lines differ in the two files. The line in passwords.new that differed is the password.

The password for the next level is: hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg


## level 18
**Level Goal** \
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
~~~
ssh bandit18@bandit.labs.overthewire.org -p 2220 ls
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat ~/readme
~~~
This level is solved using the fact that `ssh` is not onlu used for connecting to Linux servers remotely, but also allows us to execute commands on remote machine without logging into that machine.\
We simply type the commands at the end of the ssh command you'd normally use for logging in to bandit 18.

The password for the next level is: awhqfNnAbc1naukrpqDYcF95h7HoMTrC





