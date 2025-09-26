# Practicing Piping

## Redirecting outputs
First, let's look at redirecting stdout to files. You can accomplish this with the > character, as so:

```bash
hacker@dojo:~$ echo hi > asdf
```

This will redirect the output of echo hi (which will be hi) to the file asdf. You can then use a program such as cat to output this file:

```bash
hacker@dojo:~$ cat asdf
hi
```

In this challenge, you must use this output redirection to write the word PWN (all uppercase) to the filename COLLEGE (all uppercase).
### Solve
**Flag:** `pwn.college{EdUe-y_gsRU1qqZgcEVyaAUnD7Y.QX0YTN0wSN1gjNzEzW}`
 for this Challenge, i ran echo command with PWN argument and then used > to COLLEGE file to get the flag.

```bash 
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
flag:pwn.college{EdUe-y_gsRU1qqZgcEVyaAUnD7Y.QX0YTN0wSN1gjNzEzW}
```

### New Learnings
I learned how > can be used to redirect stdout to another file.

### References

## Redirecting more output
Aside from redirecting the output of echo, you can, of course, redirect the output of any command. In this level, /challenge/run will once more give you a flag, but only if you redirect its output to the file myflag. Your flag will, of course, end up in the myflag file!

You'll notice that /challenge/run will still happily print to your terminal, despite you redirecting stdout. That's because it communicates its instructions and feedback over standard error, and only prints the flag over standard out!

### Solve
**Flag:** `pwn.college{kc2MTBiJwFM0n2rGYe-0G-_ZhCs.QX1YTN0wSN1gjNzEzW}`
 for this Challenge, i ran /challenge/run command with > myflag to redirect its output to myflag file and catted myflag file to get the flag.

```bash 
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{kc2MTBiJwFM0n2rGYe-0G-_ZhCs.QX1YTN0wSN1gjNzEzW}
```

### New Learnings
I learned how > can be used to redirect output of any command to another file.

### References

## Appending output
A common use-case of output redirection is to save off some command results for later analysis. Often times, you want to do this in aggregate: run a bunch of commands, save their output, and grep through it later. In this case, you might want all that output to keep appending to the same file, but > will create a new output file every time, deleting the old contents.

You can redirect input in append mode using >> instead of >, as so:

```bash
hacker@dojo:~$ echo pwn > outfile
hacker@dojo:~$ echo college >> outfile
hacker@dojo:~$ cat outfile
pwn
college
hacker@dojo:$
```

To practice, run /challenge/run with an append-mode redirect of the output to the file /home/hacker/the-flag. The practice will write the first half of the flag to the file, and the second half to stdout if stdout is redirected to the file. If you properly redirect in append-mode, the second half will be appended to the first, but if you redirect in truncation mode (>), the second half will overwrite the first and you won't get the flag!

Go for it now!

### Solve
**Flag:** `pwn.college{4GqQ7sFgMEUmsHHkL1XkWhvfZOk.QX3ATO0wSN1gjNzEzW}`
 for this Challenge, i used > to redirect the output of /challenge/run to ~/the-flag and then again used >> to append the stdout to the same file and then catted ~/the-flag file to get the flag.

```bash 
hacker@piping~appending-output:~$ /challenge/run > ./the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll get the whole flag!
hacker@piping~appending-output:~$ /challenge/run >> ./the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll get the whole flag!
hacker@piping~appending-output:~$ cat ./the-flag
 |
\|/ This is the first half:
 v
pwn.college{4GqQ7sFgMEUmsHHkL1XkWhvfZOk.QX3ATO0wSN1gjNzEzW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>)
rather than *append* mode (>>), and so the write of the second half to stdout overwrote the initial write of the first half directly to the file. Try append mode!
```

### New Learnings
I learned how >> can be used to append more outputs to the same files again and again.

### References

## Redirecting errors
Just like standard output, you can also redirect the error channel of commands. Here, we'll learn about File Descriptor numbers. A File Descriptor (FD) is a number that describes a communication channel in Linux. You've already been using them, even though you didn't realize it. We're already familiar with three:

  FD 0: Standard Input
  FD 1: Standard Output
  FD 2: Standard Error
When you redirect process communication, you do it by FD number, though some FD numbers are implicit. For example, a > without a number implies 1>, which redirects FD 1 (Standard Output). Thus, the following two commands are equivalent:

```bash
hacker@dojo:~$ echo hi > asdf
hacker@dojo:~$ echo hi 1> asdf
```

Redirecting errors is pretty easy from this point. If you have a command that might produce data via standard error (such as /challenge/run), you can do:

```bash
hacker@dojo:~$ /challenge/run 2> errors.log
That will redirect standard error (FD 2) to the errors.log file. 
```

Furthermore, you can redirect multiple file descriptors at the same time! For example:

```bash
hacker@dojo:~$ some_command > output.log 2> errors.log
```

That command will redirect output to output.log and errors to errors.log.

Let's put this into practice! In this challenge, you will need to redirect the output of /challenge/run, like before, to myflag, and the "errors" (in our case, the instructions) to instructions. You'll notice that nothing will be printed to the terminal, because you have redirected everything! You can find the instructions/feedback in instructions and the flag in myflag when you successfully pull this off!

### Solve
**Flag:** `pwn.college{8XLxysiExppBV0ogutmYTCA78XG.QX3YTN0wSN1gjNzEzW}`
 for this Challenge, i ran /challenge/run and redirected its output to ~/myflag and its errors to intructions file.Then i catted the instruction file to run a check on my process which it confirmed as correct. So i then catted the myflag file to get the flag.

```bash 
hacker@piping~redirecting-errors:~$ /challenge/run > /home/hacker/myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat instructions
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will check that error output is redirected to a specific file path : instructions
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!

[TEST] You should have redirected my stderr to instructions. Checking...

[PASS] The file at the other end of my stderr looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-errors:~$ cat ./myflag
[FLAG] Here is your flag:
[FLAG] pwn.college{8XLxysiExppBV0ogutmYTCA78XG.QX3YTN0wSN1gjNzEzW}
```

### New Learnings
I learned how file descriptor number can be used with > to redirect any of the communication channels.

### References

## Redirecting input
Just like you can redirect output from programs, you can redirect input to programs! This is done using <, as so:

```bash
hacker@dojo:~$ echo yo > message
hacker@dojo:~$ cat message
yo
hacker@dojo:~$ rev < message
oy
```
You can do interesting things with a lot of different programs using input redirection! In this level, we will practice using /challenge/run, which will require you to redirect the PWN file to it and have the PWN file contain the value COLLEGE! To write that value to the PWN file, recall the prior challenge on output redirection from echo!

### Solve
**Flag:** `pwn.college{oDMUPZGq9C71ZF71u5OlH4WKJ88.QXwcTN0wSN1gjNzEzW}`
 for this Challenge, i ran echo command with COLLEGE and redirected its output using > to PWN file and ran /challenge/run and redirected PWN file into its standard input using < to get the flag.

```bash 
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{oDMUPZGq9C71ZF71u5OlH4WKJ88.QXwcTN0wSN1gjNzEzW}
```

### New Learnings
I learned how < can be used to redirect a file as input for a program.

### References

## Grepping stored results
You know how to run commands, how to redirect their output (e.g., >), and how to search through the resulting file (e.g., grep). Let's put this together!

In preparation for more complex levels, we want you to:

  1.Redirect the output of /challenge/run to /tmp/data.txt.
  2.This will result in a hundred thousand lines of text, with one of    them being the flag, in /tmp/data.txt.
  3.grep that for the flag!

### Solve
**Flag:** `pwn.college{A62SPmu9j_MMCpFRiv95Vm_6XGI.QX4EDO0wSN1gjNzEzW}`
 for this Challenge, i ran /challenge/run and redirected /tmp/data.txt file and then used grep with search string as pwn.college to get the flag.

```bash 
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt
pwn.college{A62SPmu9j_MMCpFRiv95Vm_6XGI.QX4EDO0wSN1gjNzEzW}
```

### New Learnings
I learned how > and grep can be used to help us search through the redirected file.

### References

## Grepping live output
It turns out that you can "cut out the middleman" and avoid the need to store results to a file, like you did in the last level. You can do this by using the | (pipe) operator. Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe. For example:

```bash
hacker@dojo:~$ echo no-no | grep yes
hacker@dojo:~$ echo yes-yes | grep yes
yes-yes
hacker@dojo:~$ echo yes-yes | grep no
hacker@dojo:~$ echo no-no | grep no
no-no
```

Now try it for yourself! /challenge/run will output a hundred thousand lines of text, including the flag. grep for the flag!

### Solve
**Flag:** `pwn.college{kH-0HUmr4XPIF9cmqxwNF59KsAS.QX5EDO0wSN1gjNzEzW}`
 for this Challenge, i ran /challenge/run with (|) pipe operator and grep with search string as pwn.college to get the flag.

```bash 
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{kH-0HUmr4XPIF9cmqxwNF59KsAS.QX5EDO0wSN1gjNzEzW}
```

### New Learnings
I learned how pipe operator can be used to directly pipe output of one command as input for another command.

### References

## Grepping errors
You know how to redirect errors to a file, and you know how to pipe output to another program, such as grep. But what if you wanted to grep through errors directly?

The > operator redirects a given file descriptor to a file, and you've used 2> to redirect fd 2, which is standard error. The | operator redirects only standard output to another program, and there is no 2| form of the operator! It can only redirect standard output (file descriptor 1).

Luckily, where there's a shell, there's a way!

The shell has a >& operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|)!

Try it now! Like the last level, this level will overwhelm you with output, but this time on standard error. grep through it to find the flag!

### Solve
**Flag:** `pwn.college{ozuOCHJKXMoUDwRQHYavEHiYwT9.QX1ATO0wSN1gjNzEzW}`
 for this Challenge, i ran /challenge/run with 2>& 1 before (|) pipe operator and grep with search string as pwn.college to get the flag.

```bash 
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{ozuOCHJKXMoUDwRQHYavEHiYwT9.QX1ATO0wSN1gjNzEzW}
```

### New Learnings
I learned how pipe operator can be used to directly pipe output of one command as input for another command.

## Filtering with grep -v
The grep command has a very useful option: -v (invert match). While normal grep shows lines that MATCH a pattern, grep -v shows lines that do NOT match a pattern:

```bash
hacker@dojo:~$ cat data.txt
hello hackers!
hello world!
hacker@dojo:~$ cat data.txt | grep -v world
hello hackers!
hacker@dojo:~$
```

Sometimes, the only way to filter to just the data you want is to filter out the data you don't want. In this challenge, /challenge/run will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word DECOY somewhere in the flag) mixed in with the real flag. You'll need to filter out the decoys while keeping the real flag!

Use grep -v to filter out all the lines containing "DECOY" and reveal the real flag!

### Solve
**Flag:** `pwn.college{AsqTJL0Dtgrgk-yCpKd_XoQ38K6.0FOxEzNxwSN1gjNzEzW}`
 for this Challenge, i ran /challenge/run with (|) pipe operator and grep -v with search string as DECOY to get the flag.

```bash 
hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep -v DECOY
pwn.college{AsqTJL0Dtgrgk-yCpKd_XoQ38K6.0FOxEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how grep -v can be used to filter out and find out unmatched lines.

### References 

