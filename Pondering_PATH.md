# Pondering PATH

## The PATH Variable
It turns out that the answer to "How does the shell find ls?" is fairly simple. There is a special shell variable, called PATH, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands. If you blank out the variable, things go badly:

```bash
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```
Without a PATH, bash cannot find the ls command.

In this level, you will disrupt the operation of the /challenge/run program. This program will DELETE the flag file using the rm command. However, if it can't find the rm command, the flag will not be deleted, and the challenge will give it to you! Thus, you must make it so that /challenge/run also can't find the rm command!

Keep in mind: /challenge/run will be a child process of your shell, so you must apply the concepts you learned in Shell Variables to mess with its PATH variable! If you don't succeed, and the flag gets deleted, you will need to restart the challenge to try again!

### Solve
**Flag:** `pwn.college{YMc3zQ-aG9EGMO0kYam9l6s_V4w.QX2cDM1wSN1gjNzEzW`
 for this Challenge,i changed the directory to challenge and then set the PATH variable to blank.Then i ran ./run program to get the flag.

```bash 
hacker@path~the-path-variable:~$ cd /challenge
hacker@path~the-path-variable:/challenge$ PATH=""
hacker@path~the-path-variable:/challenge$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{YMc3zQ-aG9EGMO0kYam9l6s_V4w.QX2cDM1wSN1gjNzEzW}
```

### New Learnings
I learned how PATH variable of a directory works to store all paths of directories within that directory.

### References

## Setting PATHS
Okay, so things break when you blank out PATH. But what about doing something useful with PATH?

Let's explore how we would, for example, add a new directory of programs to our command repertoire. Recall that PATH stores a list of directories to find commands in and, for commands in nonstandard places, we must typically execute them via their path:

```bash
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ goodscript
bash: goodscript: command not found
hacker@dojo:~$ /home/hacker/scripts/goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

If you maintain useful scripts that you want to be able to launch by bare name, this is annoying. However, by adding directories to or replacing directories in this list, you can expose these programs to be launched using their bare name! For example:

```bash
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
Let's practice. This level's /challenge/run will run the win command via its bare name, but this command exists in the /challenge/more_commands/ directory, which is not initially in the PATH. The win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory. Good luck!

### Solve
**Flag:** `pwn.college{wxK2hpARv1BWEP7NS5jyw2I2cDH.QX1cjM1wSN1gjNzEzW}`
 for this Challenge,i set the PATH variable to /challenge/more_commands./ and then i ran /challenge/run program to get the flag.

```bash 
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{wxK2hpARv1BWEP7NS5jyw2I2cDH.QX1cjM1wSN1gjNzEzW}
```

### New Learnings
I learned how PATH variable can be used to set to any particular directory so that the command/programs in that directly be invoked using the file name without its path.

### References

## Finding Commands
When you type the name of a command, something inside one of the many directories listed in your $PATH variable is what actually gets executed (of course, unless the command is a builtin!). But which file, precisely? You can find out with the aptly-named which command:

```bash
hacker@dojo:~$ which cat
/bin/cat
hacker@dojo:~$ /bin/cat /flag
YEAH
hacker@dojo:~$
```
Mirroring what the shell does when searching for commands, which looks at each directory in $PATH in order and prints the first file it finds whose name matches the argument you passed.

In this challenge, we added a win command somewhere in your $PATH, but it won't give you the flag. Instead, it's in the same directory as a flag file that we made readable by you! You must find win (with the which command), and cat the flag out of that directory!

### Solve
**Flag:** `pwn.college{U7pP0o-3D3IEjrBMyj-0uF4DR_B.01NzEzNxwSN1gjNzEzW}`
 for this Challenge,i used which command with win as the PATH variable to /challenge/more_commands./ and then i ran /challenge/run program to get the flag.

```bash 
hacker@path~finding-commands:~$ which win
/challenge/paths/23368/win
hacker@path~finding-commands:~$ cd /challenge/paths/23368/
hacker@path~finding-commands:/challenge/paths/23368$ cat flag
pwn.college{U7pP0o-3D3IEjrBMyj-0uF4DR_B.01NzEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how which command can be used to find a command location.

### References

## Adding Commands
Recall our example from the previous level:

```bash
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```

What we see here, of course, is the hacker making the shell more useful for themselves by bringing their own commands to the party. Over time, you might amass your own elegant tools. Let's start with win!

Previously, the win command that /challenge/run executed was stored in /challenge/more_commands. This time, win does not exist! Recall the final level of Chaining Commands, and make a shell script called win, add its location to the PATH, and enable /challenge/run to find it!

Hint: /challenge/run runs as root and will call win. Thus, win can simply cat the flag file. Again, the win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory. But remember, if you do that, your win command won't be able to find cat.

You have three options to avoid that:

  1.Figure out where the cat program is on the filesystem. It must be in a directory that lives in the PATH variable, so you can print the variable out (refer to Shell Variables to remember how!), and go through the directories in it (recall that the different entries are separated by :), find which one has cat in it, and invoke cat by its absolute path.
  2.Set a PATH that has the old directories plus a new entry for wherever you create win.
  3.Use read (again, refer to Shell Variables) to read /flag. Since read is a builtin functionality of bash, it is unaffected by PATH shenanigans.
Now, go and win!

### Solve
**Flag:** `pwn.college{wYNHsNUGHAbSDyBU2q3OTWhhkEg.QX2cjM1wSN1gjNzEzW}`
 for this Challenge,i create a shell script file named win and added a shebang for bash and read the /flag file to the VAR and to echo it. Then i added the path of win to the PATH variable then used chmod to make the win file executable and ran the /challenge/run to get the flag.

```bash 
hacker@path~adding-commands:~$ nano win
#!/bin/bash
read VAR < /flag
echo $VAR
hacker@path~adding-commands:~$ PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/hacker
hacker@path~adding-commands:~$ chmod +x ./win
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{wYNHsNUGHAbSDyBU2q3OTWhhkEg.QX2cjM1wSN1gjNzEzW}
```

### New Learnings
I learned how a new command can be invoked from anywhere by adding its path to the PATH variable.

### References

## Hijacking Commands
Armed with your knowledge, you can now carry out some shenanigans. This challenge is almost the same as the first challenge in this module. Again, this challenge will delete the flag using the rm command. But unlike before, it will not print anything out for you.

How can you solve this? You know that rm is searched for in the directories listed in the PATH variable. You have experience creating the win command when the previous challenge needed it. What else can you create?

### Solve
**Flag:** `pwn.college{gR5I8hNHRarS-o8KpLTlhXCMjUB.QX3cjM1wSN1gjNzEzW}`
 for this Challenge,i create a shell script file named rm and wrote cat /flag. Then i changed its permission to be executed.I then used which -a rm to find all directories with the original rm command and found three then i removed two except the /run/dojo/bin as it had cat command also and then added the path of this rm script before the /run/dojo/bin  to the PATH variable. Finally i ran the /challenge/run to get the flag.

```bash 
hacker@path~hijacking-commands:~$ nano rm
hacker@path~hijacking-commands:~$ chmod +x rm
hacker@path~hijacking-commands:~$ PATH=/home/hacker:/run/dojo/bin:/run/challenge/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/sbin
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
pwn.college{gR5I8hNHRarS-o8KpLTlhXCMjUB.QX3cjM1wSN1gjNzEzW}
```

### New Learnings
I learned how the PATH variable works to find the required command by looking in the directories in order they are in the variable and returns the first matching command .

### References