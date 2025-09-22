# Hello Hackers

## Intro to Commands 
IIn this challenge, you will invoke your first command! When you type a command and hit enter, the command will be invoked, as so:

```bash
hacker@dojo:~$ whoami
hacker
hacker@dojo:~$
```

Here, the user executed the whoami command, which simply prints the username (hacker) to the terminal. When the command terminates, the shell once again displays the prompt, ready for the next command.

In this level, invoke the hello command to get the flag! Keep in mind: commands in Linux are case sensitive: hello is different from HELLO.

### Solve
**Flag:** `pwn.college{scSO1IlJHjHSUNc-1Y2Qf3Mo_ek.QX3YjM1wSN1gjNzEzW}`
 for this Challenge, i just invoked the command hello to get the flag.

```bash 
hello
pwn.college{scSO1IlJHjHSUNc-1Y2Qf3Mo_ek.QX3YjM1wSN1gjNzEzW}
```

### New Learnings
I learned how to invoke commands in linux terminal

### References

## Intro to Arguments
 Let's try something more complicated: a command with arguments, which is what we call additional data passed to the command. When you type a line of text and hit enter, the shell actually parses your input into a command and its arguments. The first word is the command, and the subsequent words are arguments. Observe:

```bash
hacker@dojo:~$ echo Hello
Hello
hacker@dojo:~$
```

In this case, the command was echo, and the argument was Hello. echo is a simple command that "echoes" all of its arguments back out onto the terminal, like you see in the session above.

Let's look at echo with multiple arguments:

```bash
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
hacker@dojo:~$
```

In this case, the command was echo, and Hello and Hackers! were the two arguments to echo. Simple!

In this challenge, to get the flag, you must run the hello command (NOT the echo command) with a single argument of hackers. Try it now!

 ### Solve
 **Flag:** `pwn.college{I0TYz2p0WK2cP0ZBOiM0m3nZXxz.QX4YjM1wSN1gjNzEzW}`
 For this challenge , i invoked the command hello with an argument hackers

 ```bash
 hello hackers
 pwn.college{I0TYz2p0WK2cP0ZBOiM0m3nZXxz.QX4YjM1wSN1gjNzEzW}
 ```
### New Learnings
i learned what are arguments.
I learned how to run a command with arguments.

### References

## Command History
You're going to type a lot of commands, and typing everything from scratch can be annoying. Luckily, the shell saves a history of every command you invoke.

You can scroll through those saved commands with the up/down arrow keys, and we'll practice that in this challenge. This challenge will inject the flag into your history. Bring up a terminal, hit the up arrow, and grab it! In other challenges, the history will contain the log of the commands you've run, so if you need to run a similar command again, you can use the arrow keys to scroll through and find it!

### Solve
**Flag:** `pwn.college{w2AE9jiqZhDDwkDP3X7BVZmxkBH.0lNzEzNxwSN1gjNzEzW}`
For this challenge, i scrollled up using the arrow keys to get the flag.

```bash
pwn.college{w2AE9jiqZhDDwkDP3X7BVZmxkBH.0lNzEzNxwSN1gjNzEzW}
```
### New Learnings
I learned how the command history can be accessed.

### References
