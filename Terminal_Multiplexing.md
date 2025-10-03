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

## Switching Windows
Okay, so far, screen is just a weird sort of terminal-with-a-terminal. But it can be much more!

Inside a single screen session, you can have multiple windows, like your browser has multiple tabs. This can be super handy for organizing different tasks!

These windows are handled with different keyboard shortcuts, all starting with Ctrl-A:

  Ctrl-A c - Create a new window
  Ctrl-A n - Next window
  Ctrl-A p - Previous window
  Ctrl-A 0 through Ctrl-A 9 - Jump directly to window 0-9
  Ctrl-A " - bring up a selection menu of all of the windows
For this challenge, we've set up a screen session with two windows:

  Window 0 has... well, you'll have to switch there to find out!
  Window 1 has a welcome message
Attach to the session with screen -r, then use one of the key combinations above to switch to Window 1. Go get that flag!

### Solve
**Flag:** ``
 for this Challenge,i ran screen -ls command.Then i ran screen -r command with the PID of challenge session and then pressed Ctrl+A and 0 key to get the flag and then detach the screen session.

```bash 
hacker@terminal-multiplexing~switching-windows:~$ screen -ls
There are screens on:
        173.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
        144.session_6b532e1ce48db217    (Remote or dead)
        147.session_27f2637843346616    (Remote or dead)
        150.session_32f63652f8b88776    (Remote or dead)
        135.challenge_session   (Detached)
5 Sockets in /home/hacker/.screen.
hacker@terminal-multiplexing~switching-windows:~$ screen -r 135
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Welcome to the window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-A 0 to switch to window 0!
> MSG
Welcome to the window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-A 0 to switch to window 0!
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{cMegpghZ6SCcB8yY3ZPk_qmLQm7.0FO4IDOxwSN1gjNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{cMegpghZ6SCcB8yY3ZPk_qmLQm7.0FO4IDOxwSN1gjNzEzW}
hacker@terminal-multiplexing~switching-windows:~$ screen -r 135
[detached from 135.challenge_session]

```

### New Learnings
I learned how Ctrl+A and 0-9 key can be used to switch between windows 0-9.

### References

## Detaching and Attaching (tmux)
Let's try the same thing with tmux!

tmux (terminal multiplexer) is screen's younger, more modern cousin. It does all the same things but with some different key bindings. The biggest difference? Instead of Ctrl-A, tmux uses Ctrl-B as its command prefix.

So to detach from tmux, you press Ctrl-B followed by d.

```bash
hacker@dojo:~$ tmux
[doing some work...]
[Press Ctrl-B, then d]
[detached (from session 0)]
hacker@dojo:~$ 
```
The commands also differ:

  tmux ls - List sessions
  tmux attach or tmux a - Reattach to session
For this challenge:

  1.Launch tmux
  2.Detach from it.
  3.Run /challenge/run (this will send the flag to your detached session!)
  4.Reattach to see your prize


### Solve
**Flag:** `pwn.college{8j7z_vHGN0p6hHnU-IlsbopBOOM.0VO4IDOxwSN1gjNzEzW}`
 for this Challenge,i ran tmux command.Then i detach the session using Ctrl+B and then ran /challenge/run.Then i ran tmux -r command to get the flag and then detached the session using Ctrl+B.

```bash 
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux
[detached (from session 0)]
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ /challenge/run
Found detached tmux session: 0
Sending flag to your tmux session...

Flag sent! Now reattach to your tmux session with:
  tmux attach
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux a
You'll find the flag waiting for you there! 
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$  echo Congratulations, here is your flag: pwn.college{8j7z_vHGN0p6hHnU-IlsbopBOOM.0VO4IDOxwSN1gjNzEzW}
Congratulations, here is your flag: pwn.college{8j7z_vHGN0p6hHnU-IlsbopBOOM.0VO4IDOxwSN1gjNzEzW}
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ 11;rgb:0c0c/0c0c/0c0c
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux a
[detached (from session 0)]
```

### New Learnings
I learned how tmux command to open a terminal multiplexer and Ctrl+B can be used to detach it and tmux a command can be used to reattach the session.

### References

## Switching Windows (tmux)
Let's learn to navigate windows in tmux!

Just like screen, tmux has windows. The key combos are different, but the concept is the same:

  Ctrl-B c - Create a new window
  Ctrl-B n - Next window
  Ctrl-B p - Previous window
  Ctrl-B 0 through Ctrl-B 9 - Jump to window 0-9
  Ctrl-B w - See a nice window picker
Tmux shows your windows at the bottom in a status bar that looks like:

```bash
[0] 0:bash* 1:bash
```
The * shows your current window, and each entry also shows the process that the window was created to run.

We've created a tmux session with two windows:

  Window 0 has the flag!
  Window 1 has your warm welcome.
Go get that flag!

### Solve
**Flag:** `pwn.college{4QrfNLycKkoji-pNVnAHd5mCixX.0FM5IDOxwSN1gjNzEzW}`
 for this Challenge,i ran tmux command.Then i ran pressed Ctrl+B and W key to see the window picker and opened the window 1.Then i switched detach the session using Ctrl+B and then ran /challenge/run.Then i ran tmux -r command to get the flag and then detached the session using Ctrl+B.

```bash 
hacker@terminal-multiplexing~switching-windows-tmux:~$ tmux
> Excellent work! You found window 0!
> Here is your flag: pwn.college{4QrfNLycKkoji-pNVnAHd5mCixX.0FM5IDOxwSN1gjNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{4QrfNLycKkoji-pNVnAHd5mCixX.0FM5IDOxwSN1gjNzEzW}
hacker@terminal-multiplexing~switching-windows-tmux:~$ tmux
[detached (from session challenge_session)]
```

### New Learnings
I learned how Ctrl+B and W key pressed in a terminal multiplexer can be used to open the window picker and Ctrl+B and 0-9 keys can be used to open a particular window 0-9.

### References