# Linux-Fundamentals
Notes on the Linux module

What is Linux?

An open source operating system kernel (by Linus Torvalds).
Basis of most servers, cloud systems and networking devices.
It is distrubuted in distros for e.g Ubuntu,Debian.
It is cost effective secure and flexible.

Terminal & Shell

The terminal is the interface in which you type commands
The shell is the program that interprets these commands (Bash,Zsh)
You can check for the shell using: echo $SHELL
Commands are programs/binaries stored i directories listed in $PATH

Anatomy of a Command

Command+ Options + arguments
An example is: ls -a /home
where ls acts as a command -a as an option and /home as the arguemnt
The manual page can be used as a guide by running for e.g. man ls

File & Directory Basics
Navigation:
pwd:print working directory
cd <dir>:change directory
cd.. go up one level

Listing:
ls:list files
ls-la show hidden _details 

File Management:
touch file.txt: create empty file
echo "text" > file txt : write text into file
echo "text" >> file.txt: append into file
cat file.txt : read the file
cat file1 file2 > combined.txt: merge the files

Copy/MoveDelete:
cp file newfile
mv file/directory newname (can also move files/directories between directories)
rm file
rm -r dir/ remove directory recursively(and everything inside it basically)

Directories:
mkdir folder: creates directory    
rmdir emptyfolder removes empty directory
mkdir -p parent/child (nested): creates nested directories 

Viewing File Sections
head file.txt: shows the first 10 lines (-n 5 for first 5)
Tail file.txt: shows last 10 lines (-n 5 for last 5)
you can combine these so head -n 10 file.txt | tail -n5 : shows lines 6-10

File permissions:
represented as -rw-r--r--
where r=read w=write x=execute
in the catogries it shows as User|Group|Others
octal representations are as follows r=4 w=2 x=1
chmod 755 file : -rwxr-x-r-x
Symbolic representation chmod u+x file (add execute ability to user)
chmod g-r (remove read ability from group)
chmod u=rw,g=r,o=r file (permissions explicitly set)
Ownership:
ls-l shows owner and group
sudo chown user file -Changes user
sudo chgrp group file-changes group
sudo chown -R user:group dir/ - changes user and group simultaneously of the directory (this can be done for file without recursive and with the file name)

Users & Groups:
sudo adduser newuser - creates new user
sudo passwd newuser -creates password for new user
su -newuser : switches to new user
sudo usermod - aG sudo newuser: this adds the newuser to a group
Groups:
cat/etc/group- so cat will list  "/etc/group" so it lists all the groups that exist, their IDs, and their members.
sudo groupadd devops : creates a group called dev ops
Add user:sudo usermod -aG devops Newuser
Remove User: sudo gpasswd -d newuser devops

Root & Sudo
sudo <command> - Runs with elevated privellegates
sudo su - switches to the root shell
rm -rf/ : this destroys the entire system
logs are stored in /var/log/auth.log

Standard Streams & Redirection
stdin(0): input (keyboard, or < file.txt) for e.g. cat<file.txt 
stoudt(1) output (terminal or > file.txt) for e.g echo "hello" > file.txt
stderr(2) error output ( command file 2> error.txt) this saves error to a file  for e.g. ls non-existant 2> error.txt
You can combine them by using command  &> all outputs.txt for e.g ls non existant my_directory)copy &. all outputs.txt
and to discard the error command file 2> /dev/null for e.g ls nonexistant 2> dev/null

Enviromental Variables: Variables that store informatuon about the enviroment your shell runs in
View all you use printenv or env these tells you all the variables in your shell#
echo $HOME  this expands your home directory
echo $PATH shows the list of directories where the commands are searched for
you can set temporary variables using VAR=value
or to set permanent you add it to the shell so /.bashrc and /.zshrc and then source.zshrc to confirm 
some common vars $PATH .$HOME $USER (username) and $SHELL (your current shell)


Aliases
Shortcut for for long/frequent commands
use command alias 11="ls-lah"
you can type alias to view preset set aliases
to make these permanent add it  to /.bash.rc and /.zshrc  and the save using source.zshrc

Vim Essentials
Modes : Command (default) insert text (i) and esc to exit back to command (v) for visual to select text
Navigation
0=start of the line
$=end of line
/word=searches for the word
n= next match N=goes backwards
dd=delete line
yy=copy line
p=paste
u=undo
Ctrl+r=redo
Save/Quit
:wq!=save and quit
:q! quit without saving
:w! save only
! is used to add some forcefullness if the system denies your command


Overthewire Banditgame:

Level 0:First of all to enter the game you need to enter the game the through the port that is instructed.By running the command ssh bandit1@bandit.labs.overthewire.org -p 2220 you enter the server.Use the username and password given to login to the user.By running ls you find a file known as readme.You read its contents using cat , which gives you the password to the next level.

Level 1:Upon entering the level you run the ls command and find a file known as "-".You run cat./- which gives you the password for the next level. "./" was used due to the file begining with a hyphen as the cat command recognises "-" as part of the command.

Level 2:Upon entering the level you run the ls command and find a file called "--spaces in this filename--".By running cat-- "--spaces in this filename--" this seperates the hypen from the command which the cat command often gets confused by.This gives you the password to the next level.

Level 3:In this level you run the command ls to find a directory called inhere.Entering the directory using cd inhere, you run ls to see no file appearing.By running ls -a you can see hidden files.Where you see a file known as "...Hiding-from-you".Using the same trick as before, you run the command cat -- "...Hiding from you" this gives you the password to the next level.

Level 4:This level is prertty identical to level 3 but when you run ls the files show up.There are multimples files listed from 1 to 10.Assuming one of the files have the password,a command is needed to identify which one.By running the command file ./* this identifies where the password resides in."File" command is used to tell you data is inside the name file."./" means in this directory.The wild card is "*" acts as "everything" so by combining it with ./ it acts as a shell globbing.This comes out to show me all the data for everything in this directory .File 7 stands out so.The password for level 5 is revealed by running cat -- "-file07".

Level 5:So this level starts of similar to level 4 however instead of consisting of many files it consists of double the amount in directories.We are given the clue the that file with the password is exactly 1033 bytes of size.By using the command find . -size 1033c.This showed us the directory and file hence by running cat for this file the password was revealed.The final command used was cat maybehere07/.file2.

Level 6: In this level we had to locate a specific file we were given the size , the user permission and the group permission.Using the command find / -type f -size 33c -user bandit7 -group bandit6 2> /dev/null .Using "/" I searched the entire root directory as I couldnt locate it in within the bandit6 directory.Find is very handy as it can find exact files.The command ends with "2> /dev/null" so if any errors occur we can redirect them as they serve no purpose.Once the command was run the exact ancestor  directory leading to the file appeared. A simple cat command with its ancestor directory revealed the password for the following level.

Level 7: So in this level within the directory is file known as data.txt.Its a massive file with lots of words, however the pattern is that with every actual word was a password.I was told that next the word "millionth" would be the password.You could do sort -n data.txt which would put it in numerical order where you could scroll till you found the word.However the optimal method was to used the command grep "millionth" data.txt which instantly gave me the password which was next to the word millionth.

Level 8: In this level we are dealing with a line which contains the password and is only repeated once.So using the code sort put them in order using them with. The command sort data.txt | uniq only shows each line once.This wasnt enough as there were many different lines.Using sort data.txt | uniq -c would should each of one line and how may times they were duplicated this gave away the password as it was the only repeated once.The best code to use would have been sort data.txt |uniq -u as this gives you the only line repeated once which was our password.

Level 9:Ls showed me that the file data.txt was full of un readable jargon.So usings strings was useful how ever by itself it showed me lots of "human readable strings" so I used pipe to combine with with grep as I was told it precedes with an = sign so using strings data.txt | grep "=" it revealed the password.

Level 10:For this level the data was written in base64.Using the code base64 -d data.txt it revealed the password. "-d" comes up as decode without it the file is coded into base64.

Level 11: For this level the data in the file all the upper and lower case letters where shifted 13 letters.So the command tr was used to sort this out.This command revealed the password cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m' .'A-Za-z' this meant all letters pretty much for lower case and upper case.N-ZA-Mn-za-m this was used to shift all these letters down to 13 in which M is the 13 letter ence  a-m and n-z.So you basicaly start your alphabet from the 14th letter since they were all shifted hence 'N-ZA-Mn-za-m'.

Level 12: This level I was told it was hexdump of a file that had been repeatedly compressed.So first I was told to run the command mktemp -d to create a directory so that I can deal with it.So for I decoded the hex file and relocated it using xxd -r data.txt > /tmp/tmp.asdasd/data.txt2.The by using file to see the nature of the file I unzipped it.The file was of three different natures.Gzip compressed this means that to uncompress it I would have to mv data.txt data.gz and then run gunzip data.gz to decompress it.There was also bzip2 file so for this one you change it to ending .bz2 or you dont have to but it will rename it for you and it might get confusing. and the last one is tar archive.So for this you would tar -xvf data.txt where "x" means extract so needed "v" prints the name of the file being extracted without it would be done silently  and "f" for name what file to extract so all the three are used together.So these were repeated to stip the layers until the password was reached.

Level 13: For this level to reach level 14 you need to log directly into it without a password.Since the ssh private key was given (safer than a password) it was used.The command was ssh -i /home/bandit13/sshkey.private bandit14@bandit.labs.overthewire.org -p 2220 bandit14@bandit.labs.overthewire.org -p 2220.

Level 14: So for this level we need to obtain the password for thos curremnt level since we never used it to enter.By using cd /etc/bandit_pass the bandit14 password was located there>.Now to enter the local host I ran the command. nc localhost 30000 and placed the password retrieving the password for level 15.

Level 15:







