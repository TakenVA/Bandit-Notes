**SSH** \- Encryption method using public and private keys

**ls** \- See what's in the current directory, hides files that start with a dot. . for current and .. for parent directories. 

**cat** \- prints a files contents to the screen

**\-a** \- flag that means “all” 

**(-)** \- What follows is like a command of sorts that takes input

. means this current directory

/ means the file names (Whatever follows) in this directory

**cd** will change the directory

**stdout \-** normal output, stream 1

**stderr \-** errors, stream 2

**2\> \-** redirects the stream 2 to somewhere else

**/dev/null \-** is a special black hole file that discards anything written into it

**wc \-l \-** Stands for “lines” it simple counts lines

**grep \-** Kind of like CTRL \+ F in a document. It prints every line that contains the search word and skips all other. It prints the line that the word is contained in.

**grep \-i \-** ignores upper/lower case letters

**grep \-n \-** shows line numbers

**grep \-v \-** shows lines that do not match

**grep \-r (directory) \-** searches every file under a directory

**uniq \-**  removes or reports duplicate lines but one when duplicate lines are next to each other.

**sort \-** outputs a files lines in alphabetical order

**\| (pipe) \-** takes the output of one command and feeds it to the next

**uniq \-u \-** prints only lines that appear exactly once, the u being “unique”

**uniq \-c \-** prints out the count in front of each line that has duplicates. 

**strings \-** scans a binary file and prints out only the sequences of printable characters (by default, 4 or more in a row). 

**Base64 \-** It’s a way of representing data using only letters and numbers such as \+, /, and sometimes \= padding at the end. It’s used to send binary data through systems that only handle text (email attachments, web tokens, and so on). It is **NOT** encryption, it is encoding. It can be reversed by anyone which is why it’s a common thing to spot in security work.

**base64 \-d \-** base64 is the command and \-d means decode, without it the command would encode instead

**tr \-** translate, it swaps characters one-for-one. You give it two sets and each character in the first set gets replaced by the character in the same position in the second set. 

**\<** \- feeds the file into the commands input, feeds the right side into the left.

**Hexdump \-**  text representation of a binary file where each byte is written as two hex characters. 

**mktemp \-d \-** make temp directory , it creates a directory with a random name and prints it.

**cp \-** copies a file and its shape is cp \<source\> \<destination\>

**\~ \-** Short for the home directory.

**xxd \=** makes hexdumps and **\-r** reverses one back into the binary 

**\> \-** feeds the left side into the right

**ssh \-i \-** means to use this identity \<key file\> to authenticate. So with a private key it asks to authenticate with the private key instead of a password. The server has a matching public key on file for you. the \-i is the identifier which expects a path to a file.

**localhost \-** means the computer you’re on, the target, the server you’re logged into. So for example bandit, when you do localhost while on the bandit server it will be using the ports that are the bandits. If you just do localhost from the vm nothing would listen from your own ports.

**scp \-** secure copy it copies files between two computers over an SSH connection so the transfer is encrypted and uses the same login system as ssh. The shape is the same as cp: scp \<source\> \<destination\> in scp \-p is for something else “preserve” so you use \-P for port since \-p was already taken

**chmod \-** It stands for change mode, in linux every file has permissions that control who can read it, write to it, or execute it. chmod changes it. Permissions are set for three groups of people, the owner, the group, and the others (everyone on the system). Each group gets a number from adding up these values.   
Read \= 4  
Write \= 2  
Execute \= 1  
So if the owner had 6 and the others have nothing then that means that the owner can read and write. SSH will deliberately refuse to use a private key with loose permissions. Since if the permissions are loose and other parties can have access to the private key then they could copy it. So if it is not strictly set then it will print UNPROTECTED PRIVATE KEY FILE\! If it was chmod 444 that means everyone could read the file.

700 looks like \-rwx------

r is read  
w is write  
x is execute

These are sort of like permissions

For example 444 would look like this: 

Owner : r \- \-   
Group : r \- \-   
Others : r \- \-

641 would look like this

Owner : r w \-  
Group : r \- \-  
Others : \- \- x

**nc \-** netcat, its a tool that opens a raw connection to a host and port and lets you type into it like a bare-bones chat window. It is formatted like nc localhost \<port number\>

**ls / \-**  shows you the top level directories

**/etc \-** holds system configuration, this is where sensitive information usually lives which is why attackers check this first. 

**/home \-**  holds users files 

**/var \-** holds logs and variable data

**/tmp \-** is a scratch space

**ls \-l \-** ls l  stands for “long format” regular ls would one show names, but ls \- l shows each file with details about each such as permissions and such.

**openssl \-** this is a tool kit for cryptography since nc doesn’t know how to do a TLS handshake open ssl will be able to. After it does this negotiation it will behave like nc for the channel but now it will be encrypted. 

**s\_client \-** a subcommand of openssl, it acts as a TLS client, like a “secure netcat”

**\-connect localhost:\<port number\>** \- gives the host and port joined by a colon which is a different style from the nc which just uses a space. If you add **\-quiet** to the end it will suppress the handshake output and turn off the interactive commands. 

**nmap \-** port scanner, it knocks on each port and reports which ones have something listening

**\-p 3100-3200 \-** limits the scan to that range, without it nmap scans only the most common 1000 ports and would miss yours

**nmap \-sV \-** sV means “service version detection” Its slower so you have to give it a minute. Ports that speak TLS show up as ssl/... in the SERVICE column. Plain-text ones show something like echo NOTE : THIS TOOK OVER A MINUTE FOR ME

**nano \-** is a simple text editor that runs inside the terminal. The   
command opens a new empty file. 

**diff \-** compares two files line by line and prints out the only differences it is read like this 

42c42 (This means “Line 42 in the first file was changed and it’s line 42 in the second file”)  
\<old line contenthere  
– \- \-  
\>new line content here  
(Lines starting with \< come from the first filed you name and lines starting with \> come from the second file you name.

**.bashrc \-** this is a hidden file that contains commands that bash runs every time you start an interactive shell. When you SSH in normally, you get an interactive shell, so the logout command inside .bashrc runs immediately and you get kicked 

After some research after some concern about the editing of the .bashrc and security concerns. I found out that the bandit server has its own .bashrc and it did NOT edit the vms .bashrc

The only time you should be worried about .bashrc becoming a vulnerability on the vm is if you download a .bashrc from someone and apply it to your own VM.

**SSH NOTE \-** SSH can run a single command on the remote machine and print the result inside of opening the shell and then doing the command. 

**; \-** run the first, then run the second regardless of the result

**&& \-** run the second only if the first succeeded 

**setuid \-** This introduces the S so 

Owner : r w s

Where the x for execution would normally be is instead replaced by an s. Because of this is it mean that anyone who is allowed to run this file runs it as bandit20 (the owner) not as themselves.

**id \-** prints out which user you are

**euid \-** The euid (effective user ID) is who the system treats you as for permission checks. In 19 to 20 you are bandit19 but since the previous setuid had a s in it and bandit 19 is able to execute files it treats bandit19 as bandit20 when it executes the file.

**uid \-** real user ID, who you actually are and the account you are logged in as

**gid \-** your primary group id

\#Just so i have notes of this because this was kind of confusing

./bandit20-do   cat   /etc/bandit\_pass/bandit20

When you do this first line you are running the second half as the first users permissions even though you are bandit 19

THIS COULD BE DANGEROUS IN A REAL SCENARIO IF THE ACCOUNT HAD ACTUAL PRIVILEGES

**suconnect \-** is a client that connects to a port that you choose, in 20 \- 21 it checks whether that line is the bandit20 password and if it matches it sends back the bandit 21 password but something has to be listening on that port and that would be me. 

This is so complicated, in the assignment, I cat my password on a port that i choose using nc and then i use suconnect, which is a setuid with s which makes the permissions that i have be bandit21 then i choose the exact same port i used nc on so i am bandit20 communicating with myself as bandit21 on the same port.

**\* \* \* \* \*** \- Five \*\*\*\*\* means “every value” so this means that it runs every minute.

\#21 \- 22 

\* \* \* \* \*   bandit22   /usr/bin/cronjob\_bandit22.sh   &\> /dev/null  
(Schedule) (User)      (This is the command it runs)  (void output)

**cron \-** Cron is a scheduler, a background program (daemon), that starts when the system boots and never stops running. Every minute it reads its schedule files (that is what was in /etc/cron.d/) for system jobs and sees which jobs are due at that current time and then runs them as the user named. 

**myname=\$(whoami) \-** This stores the name of the user running the script whoami prints your username, and \$( ) captures a command’s output into a variable. So my name is equal to the name of the user running the script. whoami is literally who is running it. It is saying that take the result of whoami get that value and assign it to myname.

**mytarget=\$(echo I am user \$myname \| md5sum \| cut \-d ' ' \-f 1\) \-** this builds the file name into three parts. 

**echo i am user \$my name \-** prints the sentence (for this level) I am user bandit 23 when the script runs as bandit 23

**md5sum \-** turns the echo i am user my name into a 32-character hash. In general it just hashes stuff. You can do something like echo hello \| md5sum and it will convert hello into a hash and return it to the terminal. This is a one way function, meaning that you CANNOT reverse it.

This is a bit confusing, for the level you had to cut off the \- at the end. After doing some more digging apparently it is because \- is a place holder for a standard input. For example if you are doing md5sum file.txt it would output \= \<hash\> file.txt however when you are piping something and using it to hash it will out put the hash and a \- at the end to represent a standard input. Which is why we had to cut it off at the end for the level. Since we want to make sure that the file name matches when we look it up in the tmp. 

**md5 notes \-** md5 is obsolete for modern security. It is really fast and lightweight but besides that it really isn’t good for keeping things secure. It is good for non security related tasks. 

**cut \-** it takes a line of input and it keeps only the part you ask it to. 

**\-d ‘ ‘ \-** this sets up the delimiter. This defines what character is being cut at. In this case it is the space character. But it could be any value you want it to be

**\-f \-** picks which field to keep. Field meaning that at every space separates a field. Using our \-d ‘ ‘ for example, 1 2 3 would be 1(field1) 2(field2) 3(field3).

**cat /etc/bandit\_pass/$$myname>/tmp/$$mytarget \-** For this level, this means that it is copying the password tile for my name into the tmp of the target. Since the cron job is running as bandit23 the whoami gives bandit 23 the password.

**\$ \-** This is the “value” of. When you assign something to a variable you don’t use a \$ but when you want to use a variable's value you use a \$. This makes a lot more sense, originally when it showed myname=\$(whoami)it meant that it created a variable called myname and assigned the value from whatever returned from inside the ( ) then it assigned it to the value of myname.

**\$(...) \-** this is called a command substitution

**echo \-** it is used to display a line, text, or a variable on the terminal screen 

**\#BANDIT LEVEL 23 \- 24** 

**rm \-** remove something, it is used to permanently delete files and directories 

**\!WARNING FOR rm VERY IMPORTANT\!**  
IF USED INCORRECTLY rm CAN PERMANENTLY DELETE FILES AND DIRECTORIES. THERE IS NO UNDO BUTTON FOR rm SO PLEASE BE CAREFUL YOU COULD EASILY ACCIDENTALLY DELETE VERY SENSITIVE DATA.

**wildcards \-** wildcards are special symbols that allow you to match patterns of file and directory names. Instead of typing out the exact name you use wildcards to select multiple files at once.   
Wildcards are symbols such as:

**\* \-** When this wildcard is used such as: \<ls \*.txt\> It will print every file ending in .txt. It matches zero or more characters.

**? \-** This matches exactly one character. For example, if you did \<rm file?\> It would match something like file1, and filec but it wouldn’t match file10. 

**globbing \-** When a command is run with a wildcard the shell automatically expands that symbol into a matching list of file paths before the command is run.

**shopt \-** this sets shell options

**shopt \-s \-** This stands for set, meaning to turn this option on

**shopt \-u \-** This stands for unset, meaning to turn this option off

**shopt \<command\> \-** you can also run this command to see whether an option is turned on or off. For example, you can do shopt nullglob to see if it is turned on or off. 

**nullglob \-** changes how \* behaves. Normally if a wildcard matches nothing it will literally just return \*. This is bad, since it literally just returns the string “\*” so if you are doing something more complicated it can end up with bad results. With nullglob turned on, if the \* can’t find anything at all it won’t just return as \* it will return nothing at all. It is kind of like a small defensive setting. 

**spool folders \-** spool folders are used to temporarily store data that is waiting for future processing or delivery by a program, server, or background running application. It is located under /var/spool/. Specifically, in this case, it can hold user-specific cron table through /var/spool/cron

**\|\| \-** meaning or

**cd /var/spool/"\$myname"/foo \|\| exit \-** In the code I noticed this line, this code means that you move the value into the spool folder the or means that if you can’t do that then exit. This is a safe guard which I found interesting. This makes it to where you stop the script rather than continuing in the wrong directory. 

**\#\! \-** this tells the operating system that the file is a script that requires an interpreter rather than a compiled binary program

**/bin/bash \-** This is the absolute file path to the Bash executable. It directs the system to use Bash and to read and run all the commands that follow. 

**stat \-** this is a Linux utility that displays detailed metadata about a file or folder. For example, its size, permissions, timestamps, and ownership. 

**\--format “%U” \-** keep in mind, this is used with stat, with stat it will print out a long wall of text. This is basically formatting that wall of text to only get a certain thing. In this instance it is the username of the files owner. (After looking this up I also found that a lowercase u (%u) would output the numeric User ID instead.

**{} \-** For this task, the curly brackets are used to clearly define where the variable starts and where it ends. You can also use it for other purposes. For example, if you wanted to append something to the end of owner you could do “\${owner}\_bone” if you didn’t have the { } then the terminal would try to find a variable named owner\_bone

**timeout \-** this is a command in Linux that runs a specified command and then automatically terminates it if it is still running after a given time limit. This command exists to make sure that one script can’t hang forever and clog up the cron job for everyone. Kind of similar to context switching to make sure one process doesn’t hog CPU time. 

**\-s 9 \-** this is the signal to send IF it runs out of time. Signals are messages that the operating system can send to a running program to tell it to stop. Signal 9 is called SIGKILL

**SIGKILL \-** this is the most forceful method to get a program to stop running. It terminates the process immediately with no chance for it to clean up or ignore the sent request.

**SIGTERM \-** this is \-s 15, it is basically a polite way to ask the program to stop running. It allows the program to clean up after itself before exiting. SIGTERM is also the default signal that is sent when you run the kill command without specifying any options.

**./ \-** this is mentioned way back, but I feel like I should mention it since this is pretty much a safety guard just in case the file has a leading dash. Should get in the habit of using this before file/variable names if applicable. 

**rm \-rf \- \!THIS IS EXACTLY WHAT I WAS REFERRING TO WITH THE WARNING ABOVE\!** Bash lets you combine single-lettered flags after one dash. In this case, in the code below, \-r means recursively, it takes the input and keeps going down into the directories and their contents recursively. Then when it hits the bottom it starts deleting and moving back up the chain. This is bad enough, but with the added flag of \-f it gets even worse. \-f forcefully deletes files without prompting. Even if they are write-protected. This is exactly why you should have a disaster recovery plan and backups of your data stored somewhere. Since cron is running without human supervision this is especially dangerous. So \-rf is saying delete everything starting from the root. In this case the root is specified in the code before that being ”./\$i”

**fi \-** this is bash’s way of closing an if block. Since bash doesn’t use indentation or curly braces to mark where a block ends it instead spells the keyword backwards. 

**done \-** used to end a loop such as for, while, or until

**(Below is the code that is featured in level 23-24 with notes)**  
\#\!/bin/bash  
**\#This is telling the operating system to use bash to execute the commands that follow**

shopt \-s nullglob  
**\#This is setting nullglob to true which makes it to where wildcards won’t execute if there is nothing**

myname=\$(whoami)  
**\#Sets myname to be equal to wherever is running this. Since cron is running this as bandit24 myname becomes bandit24**

cd /var/spool/”\$myname”/foo \|\| exit  
**\#Moves moves it into the spool folder, if it cannot move into the spool folder then it will stop**  
echo “Executing and deleting all scripts in /var/spool/\$myname/foo:”  
**\#This is the equivalent to a print() in python.**  
for i in \* .\*;  
**\#i will loop through every file AND every hidden file in the directory.**   
	if \[“\$i” \!= “.”\] && \[ “\$i” \!= “..” \];  
**\#Skip the special two entries since all files are being shown, that being the current directory, (.) and the parent directory , (..).**   
	then   
		echo “Handling \$i”  
**\#Another print statement, since i is going through the files it will print out the current file that i is.**   
		owner=”\$stat \--format “%U” “./\$i”)”  
**\#This is taking the stat of whatever file i is currently and formatting it to where it retrieves whoever the file owner is of the current file that i is**  
		if \[“\${owner}” \= “bandit23” \] && \[ \-f “\$i” \]; then  
**\#This is a double boolean, if ONLY both are true then it can proceed. This checks if the owner variable that it got from checking the stat is \= to bandit23 AND it checks to make sure that i’s current file is a file, not a directory.**   
			timeout \-s 9 60 “./\$i”  
**\#This is saying to run this file for 60 seconds as bandit24 but if it is still going after 60 seconds forcefully kill it using SIGKILL**  
		fi   
		rm \-rf “./\$i”  
**\#This is saying to forcefully recursively remove every file from the root, that being whatever file “./\$i” is. Also keep in mind that since this is sitting between the outer and inner loop it will delete every file run through this regardless of if it passed the ownership test or not.**  
	fi  
	  
done

SINCE EVERYTHING IN THIS SPOOL FOLDER IS RUN AS BANDIT24 AND THEN DELETED AFTER I HAD TO WRITE SOME CODE TO MAKE IT READ ITS OWN PASSWORD AND THEN STORE IT LOCALLY

**mkdir \-** this is short for make directory.

**.sh \-** Linux is different from windows where it doesn’t need a specific file extension to tell the operating system how to run a file. Annotating your files with .sh means shell script. It is just used to name your files to keep it orderly

**chmod \+x \-** this adds executable permissions to a file or directory. This tells the operating system that a file is safe to run as a program or a script

**ls \-ld \-** means to check the directories permissions not the files inside 

My code that I wrote to insert into the spool folder was very simple  
**\#\!/bin/bash**  
**cat /etc/bandit\_pass/bandit24 \> /tmp/mycode/pass24.txt**  
**chmod 664 /tmp/mycode/pass24.txt**  
I had to change the directories privileges since I forgot that I am running this as bandit24 so when I created the directory “mycode” I forgot to set it to where bandit24 could actually access the directory and write to it.

**\#BANDIT LEVEL 24 \- 25**

**seq \-w \-** this is basically the (for \_ in range()) in python. The \-w pads the numbers with leading zeros.

**NOTE:** You can write code directly to the terminal and save the output as a file which I find really cool 

This level was a lot easier than I thought it would be. I created a for i in range loop from 0 to 9999 and echo’d the bandit24 password and \$i. Once the loop ran for 9999 times it got saved to a temporary text file which I used to feed into the port. It fed all those results into the port and then saved what the port spat back out at me into a result text file. I then filtered the result with grep to get the password.

**\#BANDIT LEVEL 25 \- 26 AND BANDIT LEVEL 26 \- 27**

**more \-** more is a command-line utility known as a pager. This is used to view contents of text files one screen at a time. This is unlike cat, which dumps an entire file into the terminal all at once. more instead pauses at the bottom of each screen so you can read long files or command outputs. more is interactive, while it is displaying a file you can press certain keys to control it. Pressing v while more is open opens the file in a text editor.

**export \-** this is a built-in shell command that turns a variable into an environment variable. It then passes that setting down to any programs or scripts that are launched from the current session

**TERM=linux** \- TERM is a standard environment variable that stores the name of your current terminal type. If the person who is connecting to the server has an unknown terminal type, setting this to Linux acts as a reliable fallback that almost every single Linux system recognizes. 

**exit 0 \-** there are status codes, just like in computer networking, that indicate if something was run as expected. (Such as a 200 meaning good). When exit 0 is placed at the end of a Bash script it explicitly tells the system that the script completed its job properly.

**LEVEL ISSUES NOTE:** For some reason when I was trying to resize my browser that way more wouldn’t kick me out completely since more was using my terminal size to split it up into pages. For some reason no matter how small I made it it wouldn’t work. It would just keep kicking me out. This was a massive headache but I got it to work. I managed to edit the stty rows and columns and that helped fix it.

**\#BANDIT LEVEL 27 \- 28, 28 \- 29, 30 \- 31, 31 \- 32**

**git log \-** this lists every commit, newest first and each entry has a long commit hash (which is a unique ID), as well as the author, the date, and a message. 

**git show \<commit hash\> \-** this will output what was commit at that commit

**\-- \-** these are what was removed in that commit 

\+ \- this is what was added in the commit

**git branches \-** this is a separate line of development inside the same repository. Teams can use this to work on changes without touching the main version. Each branch has its own commits and can hold different file contents.

**git branch \-a \-** \-a means all including branches that exist on the server but hasn’t been switched to yet. 

**git checkout \-** checkout switches branches.

**git tag \-** a tag is a permanent named label attached to a specific commit. Teams can use them to mark releases such a v1.0. Tags don’t move and they don’t collect new commits, and git branch and git log don’t show it either. This makes these tags easy to miss.

**git add \-** It moves new, modified, or deleted files from your working directory into a “staging area” so they can be included in your next commit

**git status \-** it is a command-line tool that displays the current state of a Git repository working directory and staging area. 

**git commit \-m \-** this permanently records staged project changes as a snapshot in your local git repository history. The \-m gives the commit messages in quotes.

**git push \-** this uploaded committed changes from your local git repository to a remote repository such as Github, Gitlab, or a private server. With the git push in the Bandit level it is just saying to take the commits on my local master branch and send them to the origins master branch.

**git origin \-** origin is a nickname for the remote repository. Git automatically saved that long URL under the name origin so that way you don’t have to retype it. 

**git remote \-v \-** this allows you to see where origin points to

**\#BANDIT 32 \- 33**

**Uppercase \-** in Linux, commands are case sensitive 

**\$0 \-** this is a special variable that holds the name of the currently running shell/script.

![][image1]

[image1]: <data:image/png;base64,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>