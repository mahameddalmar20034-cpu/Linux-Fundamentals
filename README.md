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







