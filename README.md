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

ssh: used for connecting to Linux servers remotely\
ls: to list all files and directories\
file: to show type of file\
cat: reading a file\
exit: to exit the server\
on using `cat readme`, you get a string which is the password for the next level.

The password for the next level is: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

## level 1

**Level Goal** \
The password for the next level is stored in a file called - located in the home directory
~~~
ssh bandit1@bandit.labs.overthewire.org -p 2220
cat ./- 
exit -d
~~~

Initially, i tried `cd -`, which gave me the error\
**OLDPWD not set** \
On adding ./ before the -, i got the right output. The ./ is used to execute a compiled program in the current directory. here, it implies - is a file name in the directory.

The password for the next level is: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

## level 2
**Level Goal**
The password for the next level is stored in a file called spaces in this filename located in the home directory
~~~
ssh bandit2@bandit.labs.overthewire.org -p 2220
ls
cat spaces in this filename
cat spaces\ in\ this\ filename 
exit -d
~~~

Initially, `cat spaces in this filename` gave me the wrong output as it considered each word as a file, which it isnt. On using escaoe character '/' after each word, it considered the whole thing as the file name, giving us the password. 

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

cd: Used to change directory\
using ls here, gave us nothing as the file with the pw is hidden. So, we used `ls -a`. `ls -a` will list all files, including hidden files.

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

./ here implies that -file00 is the name of a file in the directory, and not a command or option. 
Since we have so many files to search and find out which is the ASCII file, it is impractical to use file commandon each file. We use `file ./-file0* `. Since all files share a similar name with the only difference being the number at *, the * will continue putting random numbers and running the command, and thus we can search all of them in one go.

The password for the next level is: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

## level 5
**Level Goal** \
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable\
1033 bytes in size\
not executable\

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
33 bytes in size\

~~~
ssh bandit6@bandit.labs.overthewire.org -p 2220
find / -user bandit7 -group bandit6 -size 33c
cat /var/lib/dpkg/info/bandit7.password
exit -d 
~~~

`find -user` lets us dearch for all files ownmed by a user. `-group` searches for files owned by a group.

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

the `sort` command is used to sort lines of text files.\
`uniq` command is used to  report or omit repeated lines. `-c` prefix lines by the number of occurrences. The only withba count of '1' is the file that contains the pw.

The password for the next level is: EN632PlfYiZbn3PhVK3XOGSlNInNE00t



