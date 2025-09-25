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