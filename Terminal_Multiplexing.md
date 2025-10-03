# Terminal Multiplexing

## Launching Screen
Let's dive right in!

screen is a program that creates virtual terminals inside your terminal. It's somewhat like having multiple browser tabs, but for your command line!

Starting screen is super simple:

```bash
hacker@dojo:~$ screen
```
That's it! You're now inside a screen session. It looks exactly like a terminal, but there are new capabilities there, waiting to be discovered.

For this challenge, we've hooked things up so that just launching screen will get you the flag. Easy!

NOTE: When you're done with your command line, type exit or press Ctrl-D to leave the screen session. Then screen will terminate and return you to your original shell.

### Solve
**Flag:** `pwn.college{8X_HcHzYwoiD_stXyDjz2TisaV5.0VN4IDOxwSN1gjNzEzW}`
 for this Challenge,i ran screen command.In the new screen session i clicked enter key to get the flag.

```bash 
hacker@terminal-multiplexing~launching-screen:~$ screen
Congratulations! You're inside a screen session!
Here's your flag:
pwn.college{8X_HcHzYwoiD_stXyDjz2TisaV5.0VN4IDOxwSN1gjNzEzW}
```

### New Learnings
I learned how screen command to open a new virtual terminal.

### References

## Detaching and Attaching
Now we'll start digging in with the magic of detaching!

Imagine you're working on something important over a remote connection, and your connection drops. With a normal terminal (outside of this awesome dojo environment), everything's gone. With screen, your work keeps running, and you can reattach later!

You can also detach on purpose, which we'll do in this challenge. You detach by pressing Ctrl-A, followed by d (for detach). This leaves your session running in the background while you return to your normal terminal.

```bash
hacker@dojo:~$ screen
[doing some work...]
[Press Ctrl-A, then d]
[detached from 12345.pts-0.hostname]
hacker@dojo:~$ 
```
To reattach, you can use the -r argument to screen:

```bash
hacker@dojo:~$ screen -r
```
For this challenge, you'll need to:

  1.Launch screen
  2.Detach from it.
  3.Run /challenge/run (this will secretly send the flag to your detached session!)
  4.Reattach to see your prize
FUN FACT: Ctrl-A is screen's activation key for all of its shortcuts in its default configuration. All screen functionality is activated by some command combination starting with Ctrl-A.

HINT: Remember: Hold Ctrl and press A, then release both and press d.

HINT: If you see [detached from...], you did it right!

### Solve
**Flag:** `pwn.college{sIoh5YXaLFonZU5-N-belFlYnv3.0lN4IDOxwSN1gjNzEzW}`
 for this Challenge,i ran screen command.In the screen session i clicked enter key and then used Crtl+A and then pressed D key to detach the screen session.Then i ran /challenge/run and then again ran screen -r command to get the flag in the screen session .

```bash 
hacker@terminal-multiplexing~detaching-and-attaching:~$ screen
[detached from 163.pts-0.terminal-multiplexing~detaching-and-attaching]
hacker@terminal-multiplexing~detaching-and-attaching:~$ /challenge/run
Found detached screen session: 163.pts-0.terminal-multiplexing~detaching-and-attaching
Sending flag to your screen session...

Flag sent! Now reattach to your screen session with:

  screen -r

You'll find the flag waiting for you there!
hacker@terminal-multiplexing~detaching-and-attaching:~$ echo Yes! Flag is: pwn.college{sIoh5YXaLFonZU5-N-belFlYnv3.0lN4IDOxwSN1gjNzEzW}
Yes! Flag is: pwn.college{sIoh5YXaLFonZU5-N-belFlYnv3.0lN4IDOxwSN1gjNzEzW}
hacker@terminal-multiplexing~detaching-and-attaching:~$ screen -r
[screen is terminating]
```

### New Learnings
I learned how Ctrl+A and D key can be used to detach a screen session and -r option with screen command.

### References

## Finding Sessions
Time for some screen detective work!

If you become an avid screen user, you will inevitably end up with multiple sessions running. How do you find the right one to reattach to?

Well, we can list them:

hacker@dojo:~$ screen -ls
There are screens on:
        23847.mysession   (Detached)
        23851.goodwork    (Detached)
        23855.morework    (Detached)
3 Sockets in /run/screen/S-hacker.
The identifiers of the sessions are the PID of each respective screen process, a dot, and the name of the screen session. To attach to a specific one, you use its name or its PID by giving it as an argument to screen -r.

hacker@dojo:~$ screen -r goodwork
In this challenge, we've created three screen sessions for you. One of them contains the flag. The other two are decoys!

You'll need to check each one until you find it. Don't forget to detach (Ctrl-A d) before trying the next session!

### Solve
**Flag:** `pwn.college{8pxJT-lwgBV1mVHFPHuk8pvXQSO.01N4IDOxwSN1gjNzEzW}`
 for this Challenge,i ran screen -ls command.Then i ran screen -r command with each PID of screen and check for flag and then detach the screen session.

```bash 
hacker@terminal-multiplexing~finding-sessions:~$ screen -ls
There are screens on:
        173.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
        144.session_6b532e1ce48db217    (Detached)
        147.session_27f2637843346616    (Detached)
        150.session_32f63652f8b88776    (Detached)
4 Sockets in /home/hacker/.screen.
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 144
[detached from 144.session_6b532e1ce48db217]
hacker@terminal-multiplexing~finding-sessions:~$  echo 'Nothing here! Try another session.'
Nothing here! Try another session.
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 147
[detached from 147.session_27f2637843346616]
hacker@terminal-multiplexing~finding-sessions:~$  echo 'Congratulations! You found the right session!'
Congratulations! You found the right session!
hacker@terminal-multiplexing~finding-sessions:~$  echo pwn.college{8pxJT-lwgBV1mVHFPHuk8pvXQSO.01N4IDOxwSN1gjNzEzW}
pwn.college{8pxJT-lwgBV1mVHFPHuk8pvXQSO.01N4IDOxwSN1gjNzEzW}
```

### New Learnings
I learned how screen -ls can be used to list all screen sessions.

### References

