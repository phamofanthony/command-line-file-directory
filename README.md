# Command Line Challenges VM

## VM Setup
A linux-based virtual machine will be setup with the directory outlined in this Git repository. Each folder in this main directory corresponds to a different part or challenge in this series. Each folder will be encrypted with a password that's required to access the challenge contents. This password will be granted as each challenge is unlocked.

The users will be run as user [USERID] with group [GROUPID]. 

## VM Considerations
In the VM, the active user should be setup to have just enough privileges to complete the challenges. They shouldn't have excessive privileges to mitigate any "cheesing" of the challenges.

Additionally, use tools like gocryptfs to encrypt the folder.

Run these commands in VM start:
```
sudo adduser ctfplayer (give it a password)
sudo adduser special_ctfplayer
```

## Admin Credentials
Username: vboxuser
Password: VJUcc'321LRw

## Folder Encryption Process
sudo apt install gocryptfs
Mkdir part1_encrypted part1_decrypted
Gocryptfs -init part1_encrypted
Gocryptfs part1_encrypted part1_decrypted
Mv part1/* part1_decrypted/
Fusermount -u part1_decrypted

Unlock:
Gocryptfs part1_encrypted part1_decrypted

## Solutions
### Part 1 (Adel)

### Part 2 (Anthony)
The flag string is reversed in the jumbled text. 
The reversed flag is `}nwod_edispu_nworf_taht_nrut{galf`, leading to a solution flag of `flag{turn_that_frown_upside_down}`.

### Part 3 (Adel)

### Part 4 (Anthony)
1. Have a .txt file saying "You're out of your reach, kiddo. Go home.", and have the `not_bad.txt` file hidden to the specific `special_ctfplayer` user only
2. Navigate to the home directory, which contains a setuid binary
3. Use the setuid binary to run commands as the `special_ctfplayer` user
4. With the binary, run `ls -a` in the challenge folder to show the previously hidden and privileged file
5. With the binary, run `cat not_bad.txt` to examine the contents of the file which will then expose the flag `flag{i_love_me_some_cup_rawrmen}`

### Part 5 (Adel)

### Part 6 (Anthony)
Have a text file with a bunch of flags with varying repetition counts. This text file will include hundreds of flags, making a brute force attempt infeasible. Because of this, we need to figure out which one is the right one.

There is a hidden markdown file in the directory that outlines a math problem. Solving the math problem results in `x=92`. This integer will correlate to the correct flag in the original text file that is repeated `x` times.

To find the flag that is repeated `x` times, use the `sort` command to organize the text and `uniq` command with the count flag `-c` to count the number of repetitions, then analyzing that text to find only the one with the count of 92. Here is a sample solution:
```
sort secret_flag_in_here.txt | uniq -c | awk '$1 == 92 {print $2}'
```
This results in the flag `flag{yZ4RYmBvcy}`


