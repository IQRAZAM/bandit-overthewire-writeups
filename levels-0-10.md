Bandit Levels 0–10 — Writeup & Learnings
This document contains my solutions, approaches, and learnings for Bandit Levels 0–10.
Passwords are not shown for security reasons (you should practice it by yourself for better understandings.)
Before starting we need to learn how to login and start finding the passwords for level for that purpose we have level 0.
Goal of this level
You need to log into the Bandit server using SSH.


Host: bandit.labs.overthewire.org


Port: 2220


Username: bandit0


Password: bandit0

**** hint ****
the passwords of levels normally look like thsi :
 "morVThKiC34YsxHJHOvyg66cXTRDjVuijcDTF" 
 
Once you log in, you’re inside a remote Linux machine as user bandit0.
The whole point of Level 0 is:
Learn how to use SSH to connect to a remote server.
Nothing more. No searching files, no commands — just connecting.
What does “non-standard port” mean?
Normally, SSH uses port 22.
But Bandit uses port 2220 to avoid conflicts.
So instead of:
ssh bandit0@bandit.labs.overthewire.org

You must connect using a different port:
ssh -p 2220 bandit0@bandit.labs.overthewire.org

What happens after logging in?
You’ll see:
bandit0@bandit:~$

This means:


You are inside the Bandit server


You are logged in as user bandit0


You can now work inside this remote Linux environment


You are ready for Level 1



Level 0 → 1
Objective
SSH into the remote machine and retrieve the password in the readme file.
Approach
Use the provided port (2220), connect via SSH, list files, and read the file.
Commands
ssh bandit0@bandit.labs.overthewire.org -p 2220
ls
cat readme

Learning


Basics of SSH


Listing files


Reading file content



Level 1 → 2
Objective
File named - must be read.
Approach
Use path notation ./- to avoid confusion with command options. This step is very helpful.
Commands
ls
cat ./-

Learning


How Linux handles filenames starting with - (very important)


Using relative paths. This helped me understand how we can access files and how files are being arranged and can be accessed.



Level 2 → 3
Objective
Find the file with spaces in its name.
Approach
Escape spaces using quotes or backslashes.
Commands
ls
cat "spaces in this filename"

Learning
Handling filenames with spaces, making it easier to understand different file names.

Level 3 → 4
Objective
Find a hidden file.
Approach
Use ls -a to list hidden files.
Commands
ls -a
cat .hidden

Learning
Hidden files start with . (very important).

Level 4 → 5
Objective
File containing human-readable text among many.
Approach
Use file command to identify file type.
Commands
ls
file ./*
cat <filename>

Learning
Using file to detect data types.

Level 5 → 6
Objective
Find a file with specific permissions and size.
Approach
Use find with conditions.
Commands
find . -type f -size 1033c -group bandit6 -user bandit6
cat <path>

Learning
Using find with filters.

Level 6 → 7
Objective
Find a readable file owned by user bandit7, group bandit6.
Approach
Search from root directory with permission suppression.
Commands
find / -type f -user bandit7 -group bandit6 2>/dev/null
cat <file>

Learning


Search entire system


Suppress permission errors



Level 7 → 8
Objective
Find password inside a file containing the word "millionth".
Approach
Use grep to search.
Commands
grep "millionth" data.txt

Learning
Using grep to search within files.

Level 8 → 9
Objective
Find unique line in a huge file.
Approach
Sort and use uniq.
Commands
sort data.txt | uniq -u

Learning
Sorting + filtering unique values.

Level 9 → 10
Objective
File contains binary data mixed with text.
Approach
Use strings to extract readable text and filter unusual pattern.
Commands
strings data.txt | grep "="

Learning
Using strings to analyze binary files.

Level 10 → 11
Objective
File is base64-encoded.
Approach
Decode the file.
Commands
cat data.txt | base64 --decode

Learning
Base64 decoding in Linux.

