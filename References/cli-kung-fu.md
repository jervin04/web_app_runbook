# BashKungFu

list items in list format include size of all items, included hidden all files in human readable format and sort by newest time first

# ls


ls -lsaht

# mousepad


use the mouspad tool to open an edit a file... because everyone hates vim


sudo mousepad /etc/hosts


# cat


cat /etc/hosts



When using a brute forcing tool, selecting the right wordlist can directly impact our results. DIRB's default wordlist is often useful, but we may want to use different wordlists if we don't get many results. Kali Linux includes several wordlists at /usr/share/wordlists.


ls -alh /usr/share/wordlists


asking Linux to separate errors and 'good' results.


# find


find / -name "passwd" 1>results.txt 2>errors.txt

Search for files that start with .hid. The search should be case insensitive from the root of the file system. Errors should be sent to /dev/null. Remember -iname searches for file name matches on a case insensitive basis. You can do this as follows:


find / -iname ".hid*" 2>/dev/null



Let us hunt for a specific file in the system. We are going to search from the root of the file system for files that contain the filename passwd. We will suppress errors based on permissions using 2>/dev/null.


find / -name "passwd" 2>/dev/null



find all files with permissions high suid permissions, and send get rid of all the errors from the scan, since this scans entire file system


find / -perm /4000 2>/dev/null



find all files in the etc directory, and grep for the string password, and surpress the errors


find /etc -iname "*.ini" -exec grep -i "password" {} /dev/null \; 2>/dev/null



# grep


Within the grepfile1.txt there is a reference to someone's home. Let's search for 'home' and see if we can find it.


grep "home" grepfile1.txt


grep "pass" grepfile2.txt


Neat, that found quite a few matches - like password123. But note this is all lowercase because we are defaulting case sensitive. Let us try it without case sensitivity.


grep -i "pass" grepfile2.txt


That found a few more hits, the -i switch found matches like Password. Finally, let us try searching across a couple of files together. In fact, let's search every file in this directory!


grep -i "whole" *


The /etc/passwd file contains references to users on the system, and we know the root user always exists in it.


grep root /etc/passwd


Perhaps we want to find references to root in the /etc directory overall and suppress errors


grep -R "root" /etc/ 2>/dev/null



# Reverse Command Search


Instead of using the arrow keys to navigate through your command history, you can actually perform a search. I find this is something that not many people know about, but in most terminals pressing CTRL + R in the terminal will bring up a search prompt. 


# history


We are going to run the history command to see what it knows about commands we have run. Do this as follows:


history


Now we are going to print out the .bash_history file! Here we go:


cat .bash_history


# top


We are going to run the top command to see what this system is up to. It will 'lock us in'.


Hit the control key and 'Z' at the same time to suspend it. Here we go:

Ctrl-Z


Now the process is suspended, we want to 'bring it back'. We do this with the following command:

fg


top is back! OK let us make this more complex and get two of these running. Suspend top again, and then we will launch another command.

Ctrl-z
less /etc/passwd
Ctrl-z


OK now we have two processes suspended. We can use the jobs command to list them. Simply execute it:


jobs


Want to switch to one of them? Use the number next to it, for example:

fg 2


You should have got your second process back. Now you can switch between things as you need!


# which


The which command is useful to find out 'which' binary you will run and where. This is useful in resolving version or path confusion issues!


If you try to run which on a command which doesn't exist in your PATH, then you will get no results. This is a good indication that you need to either:


Move the program you installed into a folder in your PATH or Add the folder that the program was installed into to your PATH.



Find out where the following tools are located:

ls


adduser


cat


nano


grep


less


Notice how some are under /bin, /sbin, or /usr/bin? These are all in the path and the which command shows you which matches. Note sometimes there will be commands with the same name in the path, and Linux will run the first one it finds. This is when which is useful.



# apropos


The apropos Command


The apropos command is a quick way to search manuals on your system for matches, for example to find a command that performs a certain function where you do not know the exact name of the command.


You already know about the 'man' command. This is the command used to pull up a manual page on tools installed on your Linux system. Similar to 'man' is 'apropos'. The 'apropos' tool is used to search man pages for keywords, usually to find the 'appropriate' tool to use in a particular situation.

For example, 'which tool could I use to display the manual for a tool?":


The 'apropos' command is used to find the 'appropriate' tool for a particular job. It's particularly useful when you don't have access to the internet for some reason, such as if you are working on a long flight.



# file


The 'file' command can tell us the filetype of a file. You may have noticed that Linux isn't keen on using file extensions, instead what matters is the contents of the file. Specifically, every filetype has its own file header which is something like a signature identifying it. The file header is universal, even files created on Windows use them, it's just that Linux uses them to tell the type of file, while Windows relies more on file extensions (which, let's face it, are basically just part of the file name).

The way the file command works is by reading the file header of the file and comparing it against a database of file headers to tell you what type of file something is. Take a look:

Linux terminal showing output of file azipfile and file /bin/ls. For each it shows the type of file, e.g. Zip archive data or ELF 64-bit respectively. Numerous verbose properties are listed too.

Here we ran 'file' on two files. The first file is a zip file, which we removed the file extension from. The 'file' command accurately tells us that it is a zip file.

The second time we ran it on the 'ls' command, which is a binary executable file, and 'file' tells us that it is an 'ELF' file (which is the Linux version of an EXE on Windows: an executable file).


OK, so that file is a configuration file using ASCII text. Let us try instead a binary. How about the ls command? We will use which to find it, and file to examine it.


which ls


file /usr/bin/ls


# wget


The 'wget' command stands for 'web get'. It allows us to download files from the internet from the command line. Take a look:

wget 127.0.0.1


# Command Line Chaining


cd /usr
ls; sleep 3; ps aux


We can also use pipes and redirects if we want to.

cat /etc/passwd | grep root; sleep 2; ps aux | grep root


the ability to pass information between commands and build up your desired capabilities is the real point.


Firstly we will use the ps aux command. We then layer this together with grep to filter for a specific set of processes that match the name smbd. This is done as follows:


ps aux | grep smbd


This produces a list of the corresponding processes, but unfortunately also matches the grep itself! We want to remove this from the list as a false match, which we can do with another grep and the negation option!


ps aux | grep smbd | grep -v grep


Now we want to filter for the PID field, which is the second field (defined by tabs between data by default). We can use awk to do this. Please note that awk has a remarkable set of capabilities - it is a whole language designed to filter and manipulate data. Adding awk we now have:


ps aux | grep smbd | grep -v grep | awk '{ print $2 }'


This gives us a list of PIDs that we can now process, using the xargs command. Xargs enables us to take items delimited by spaces, other characters or returns. The default handles new lines which is exactly the format of our data! It will pass the command as an argument to any command that we specify.


ps aux | grep smbd | grep -v grep | awk '{ print $2 }' | kill -9


The kill -9 which hard terminates a process will be executed for each of the lines, terminating the processes one by one. Running one of our earlier ps aux | grep smbd commands against will demonstrate these have been terminated.


The power of this system is that each command you learn, such as awk, python, tee, cat, grep (and many more), can be tied together to form new combinations. You can use each command as a part of the jigsaw puzzle you assemble to solve your specific issue. It takes practice, but this is extremely powerful and will supercharge the velocity with which you complete tasks in the future.



# ps


A process is just a running program of some kind. You previously saw one method of viewing running processes by using 'top', however top is not a complete list of all processes running on the system, just the ones that are using the most resources. To see a full list, we can use the 'ps' command:


Launch the top command, then background it as we learned before. Remember this requires you to use Ctrl-Z on the keyboard at the same time.

top and now Ctrl-Z

bg (execute this as a command).


Now that top is running in the background we can run ps to list processes. We will list all the ones on the system we can see:


ps aux


See the top command? It will have a PID next to it. Read the text in this module again if you aren't following. Now we want to terminate this process.

kill -9 <pid> (where pid is the number listed)

The equivalent in Linux syntax would be:

ps -ef -f


Another thing you might find useful is to get a full list of processes along with subprocesses and more detail on the parameters the processes were launched with. In BSD syntax:


$ ps auxf


