Levels 11 to 20

This report continues my learning journey with the OverTheWire Bandit wargame.
In these levels, the difficulty increased significantly and introduced new Linux concepts such as encoding, compression, SSH keys, networking, and setuid binaries.
Each level helped me understand how real systems hide information and how attackers or security professionals uncover it.

Level 11 → Level 12
Problem Description

The file contains text where letters are rotated by 13 positions (ROT13 cipher).

Approach & Solution

ROT13 is a simple substitution cipher. I used the tr command to rotate characters back to their original positions.

Key Command Used
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
Difficulty Faced

Understanding the character mapping for ROT13 was confusing initially.

What I Learned

Simple ciphers still matter in security challenges

Power of text manipulation commands

tr command usage

Level 12 → Level 13
Problem Description

The password is hidden inside a file that has been compressed multiple times using different formats.

Approach & Solution

I repeatedly checked the file type and decompressed it step by step until I reached a readable file.

Tools & Commands Used

file

gzip, bzip2, tar

xxd (for hex to binary)

Difficulty Faced

Remembering which decompression tool to use at each step.

What I Learned

How file compression layers work

Importance of checking file types

Patience and systematic problem-solving

Level 13 → Level 14
Problem Description

The password is stored in /etc/bandit_pass/bandit14, but login requires an SSH private key, not a password.

Approach & Solution

I used the provided private SSH key to log into the next level.

Key Command Used
ssh bandit14@localhost -i sshkey.private
Difficulty Faced

Understanding how SSH keys work instead of passwords.

What I Learned

SSH key-based authentication

Importance of file permissions

Real-world secure login methods

Level 14 → Level 15
Problem Description

The password must be retrieved by sending the current password to a local port (30000).

Approach & Solution

I used nc (netcat) to send the password and receive the next one.

Key Command Used
nc localhost 30000
Difficulty Faced

Networking concepts felt intimidating at first.

What I Learned

Basic client-server communication

How services listen on ports

Using netcat for testing services

Level 15 → Level 16
Problem Description

Similar to the previous level, but this time the service uses SSL encryption.

Approach & Solution

I used openssl to securely communicate with the service.

Key Command Used
openssl s_client -connect localhost:30001
Difficulty Faced

SSL output looked overwhelming and noisy.

What I Learned

Difference between encrypted and unencrypted communication

Basics of SSL/TLS

Using OpenSSL for secure connections

Level 16 → Level 17
Problem Description

Multiple ports are open, but only one provides the correct service.

Approach & Solution

I scanned ports using nmap, identified the SSL service, and retrieved the SSH private key.

Key Commands Used
nmap localhost
openssl s_client -connect localhost:<port>
Difficulty Faced

Filtering useful information from scan results.

What I Learned

Port scanning fundamentals

Service identification

How attackers enumerate services

Level 17 → Level 18
Problem Description

Passwords are stored in two files. The correct password is the difference between them.

Approach & Solution

I compared the files line by line to find the unique line.

Key Command Used
diff passwords.old passwords.new
Difficulty Faced

Understanding how diff output works.

What I Learned

File comparison techniques

Spotting changes in system files

Why logs and backups matter

Level 18 → Level 19
Problem Description

The shell immediately logs out after login.

Approach & Solution

I bypassed the shell by executing commands directly during SSH login.

Key Command Used
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
Difficulty Faced

I thought my login was broken at first.

What I Learned

SSH command execution without shell access

Restricted environments

Bypassing limitations creatively

Level 19 → Level 20
Problem Description

A setuid binary exists that runs commands as another user.

Approach & Solution

I used the binary to execute a command that reads the password file.

Key Command Used
./bandit20-do cat /etc/bandit_pass/bandit20
Difficulty Faced

Understanding what setuid really means.

What I Learned

Privilege escalation basics

How misconfigured binaries are dangerous

Real-world security risks

Overall Challenges Faced (Levels 10–20)

Understanding new Linux tools

Interpreting noisy command output

Staying patient during multi-step problems

Overall Learnings

Linux is extremely powerful when used correctly

Small tools can solve big problems

Cybersecurity is about thinking, not memorizing commands

Real systems fail due to misconfigurations, not magic hacks

Conclusion

Levels 10 to 20 pushed me beyond basic Linux commands and introduced real cybersecurity concepts like encryption, networking, and privilege escalation.
These levels strengthened my confidence and made me think like a security practitioner rather than just a user.