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

**cronjobs \-** this is a scheduler that runs commands automatically at set times. 

**myname=\$(whoami) \-** This stores the name of the user running the script whoami prints your username, and \$( ) captures a command’s output into a variable. So my name is equal to the name of the user running the script. Who am i is literally who is running it. 

**mytarget=\$(echo I am user \$myname \| md5sum \| cut \-d ' ' \-f 1\) \-** this builds the file name into three parts. 

**echo i am user \$my name \-** prints the sentence (for this level) I am user bandit 23 when the script runs as bandit 23

**md5sum \-** turns the echo i am user my name into a 32-character hash

**cut \-d ‘ ‘ \- f 1 \-** this keeps only the first space-separated field, since md5sum also prints a trailing \-

**cat /etc/bandit\_pass/$$myname>/tmp/$$mytarget \-** For this level, this means that it is copying the password tile for my name into the tmp of the target. Since the cron job is running as bandit23 the whoami gives bandit 23 the password.