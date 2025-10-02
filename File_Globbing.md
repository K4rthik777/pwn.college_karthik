# File Globbing

## Matching with *
The first glob we'll learn is *. When it encounters a * character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. It's easier to show you than explain:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
```
Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
When zero files are matched, by default, the shell leaves the glob unchanged:
```
```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```
The * matches any part of the filename except for / or a leading . character. For example:

```bash
hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
```

Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{U0vVJ7w4qpJg7Xac2OdZKRC8t8w.QXxIDO0wSN1gjNzEzW}`
 for this Challenge, i changed directory with only /ch* as the argument and it changed the directory to /challenge and then i invoked run to get the flag.

```bash 
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ ./run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{U0vVJ7w4qpJg7Xac2OdZKRC8t8w.QXxIDO0wSN1gjNzEzW}
```

### New Learnings
I learned how * works to find the files that match its pattern.

### References

## Matching with ?
Next, let's learn about ?. When it encounters a ? character in any argument, the shell will treat it as a single-character wildcard. This works like *, but only matches one character. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
```

Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{wER1-yHA7ru7Kq7pg-tC2sMszfm.QXyIDO0wSN1gjNzEzW}`
for this Challenge, i changed directory with /?ha??enge as the argument and it changed the directory to /challenge and then i invoked run to get the flag.

```bash 
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ ./run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{wER1-yHA7ru7Kq7pg-tC2sMszfm.QXyIDO0wSN1gjNzEzW}
```

### New Learnings
I learned how ? works to match the argument to a single character in another filename with similar pattern.

### References

## Matching with []
Next, we will cover []. The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

Try it here! We've placed a bunch of files in /challenge/files. Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h!

### Solve
**Flag:** `pwn.college{Mh4wa0aF57_nUIfKySDnssUD9fy.QXzIDO0wSN1gjNzEzW}`
for this Challenge, i changed directory to /challenge/files then i invoked /challenge/run with argument files_[absh] to get the flag.

```bash 
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[absh]
You got it! Here is your flag!
pwn.college{Mh4wa0aF57_nUIfKySDnssUD9fy.QXzIDO0wSN1gjNzEzW}
```

### New Learnings
I learned how [] works to match multiple filenames with similar pattern with the characters within it .

### References

## Matching paths with []
Globbing happens on a path basis, so you can expand entire paths with your globbed arguments. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
```

Now it's your turn. Once more, we've placed a bunch of files in /challenge/files. Starting from your home directory, run /challenge/run with a single argument that bracket-globs into the absolute paths to the file_b, file_a, file_s, and file_h files!

### Solve
**Flag:** `pwn.college{UHPc99fToZYsXEJiB1ak0zxKV01.QX0IDO0wSN1gjNzEzW}`
for this Challenge, i ran /challenge/run  with argument /challenge/files/files_[absh] to get the flag

```bash 
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[absh]
You got it! Here is your flag!
pwn.college{UHPc99fToZYsXEJiB1ak0zxKV01.QX0IDO0wSN1gjNzEzW}
```

### New Learnings
I learned how [] works even with the absolute path of the files to match multiple filenames with similar pattern  with the characters within it .

### References

## Multiple globs
So far, you've specified one glob at a time, but you can do more! Bash supports the expansion of multiple globs in a single word. For example:

```bash
hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
```

What happens above is that the shell looks for all files in / that start with anything (including nothing), then have an f and an l, and end in anything (including ag, which makes flag).

Now you try it. We put a few happy, but diversely-named files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

### Solve
**Flag:** `pwn.college{UML_YMo_UZr4906qXMiQyqVTUb8.0lM3kjNxwSN1gjNzEzW}`
 for this Challenge, i changed directory to /challenge/files and invoked /challenge/run with a arguments using two golbs with letter p to get the flag.

```bash 
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{UML_YMo_UZr4906qXMiQyqVTUb8.0lM3kjNxwSN1gjNzEzW}
```

### New Learnings
I learned how two golbs can be used to search anything that has specified characters in their filename.

### References

## Mixing globs
Now, let's put the previous levels together! We put a few happy, but diversely-named files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match the files "challenging", "educational", and "pwning"!

### Solve
**Flag:** `pwn.college{QBHChdx0M7CJVBT8TxexBlclGwS.QX1IDO0wSN1gjNzEzW}`
 for this Challenge, i changed directory to /challenge/files and invoked /challenge/run with a arguments using [] and * golbs with letters c,e,p to get the flag.

```bash 
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{QBHChdx0M7CJVBT8TxexBlclGwS.QX1IDO0wSN1gjNzEzW}
```

### New Learnings
I learned how multiple types of golbs can be used together to search anything that has specified characters in their filename.

### References

## Exclusionary globbing
Sometimes, you want to filter out files in a glob! Luckily, [] helps you do just this. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed. For example:

```bash
hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
```

Armed with this knowledge, go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n!

NOTE: The ! character has a different special meaning in bash when it's not the first character of a [] glob, so keep that in mind if things stop making sense! ^ does not have this problem, but is also not compatible with older shells.

### Solve
**Flag:** `pwn.college{MYCAF44BeriHxG1hJiixxeFFa8W.QX2IDO0wSN1gjNzEzW}`
 for this Challenge, i changed directory to /challenge/files and invoked /challenge/run with a arguments using [] and * golbs with ! used before the letters p,w,n to get the flag.

```bash 
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{MYCAF44BeriHxG1hJiixxeFFa8W.QX2IDO0wSN1gjNzEzW}
```

### New Learnings
I learned how ! and ^ golbs can be used with [] glob to exlude anything that has specified characters in their filename.

### References

## Tab completion 
As tempting as it might be, using * to shorten what must be typed on the commandline can lead to mistakes. Your glob might expand to unintended files, and you might not spot it until the rm command is already running! No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it. Auto-completion is super useful, and this challenge will explore its use in specifying files.

This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it. Try it out!

```bash
hacker@dojo:~$ ls /challenge
DESCRIPTION.md  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
```

When you hit that tab key, the name will expand and you'll be able to read the file. Good luck!

### Solve
**Flag:** `pwn.college{UHN6POSPLMPhYT8cKz3nkhPOELe.0FN0EzNxwSN1gjNzEzW}`
 for this Challenge, i wrote cat command with pwn then used tab to auto complete the argument and executed the command to get the flag.

```bash 
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​
pwn.college{UHN6POSPLMPhYT8cKz3nkhPOELe.0FN0EzNxwSN1gjNzEzW}
```

### New Learnings
I learned how tab can be used to auto complete filenames .

### References

## Multiple options for tab completion
Consider the following situation:

```bash
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
```

There are multiple options! What happens?

What happens varies based on the specific shell and its options. By default bash will auto-expand until the first point when there are multiple options (in this case, fl). When you hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

This challenge has a /challenge/files directory with a bunch of files starting with pwncollege. Tab-complete from /challenge/files/p or so, and make your way to the flag!

### Solve
**Flag:** `pwn.college{oaluj_RlkQoB4rXNewIBarCJcfq.0lN0EzNxwSN1gjNzEzW}`
 for this Challenge, i wrote cat command with /challenge/files/p then clicked tab twice to get all options for the argument and did the same untile i found the correct file and upon catting that file i got the flag.

```bash 
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwn
pwn                    pwncollege-family      pwncollege-flyswatter
pwn-college            pwncollege-flag        pwncollege-hacking
pwn-the-planet         pwncollege-flamingo
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-f
pwncollege-family      pwncollege-flamingo
pwncollege-flag        pwncollege-flyswatter
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-
pwncollege-family      pwncollege-flamingo    pwncollege-hacking
pwncollege-flag        pwncollege-flyswatter
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-fl
pwncollege-flag        pwncollege-flamingo    pwncollege-flyswatter
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-fla
pwncollege-flag      pwncollege-flamingo
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{oaluj_RlkQoB4rXNewIBarCJcfq.0lN0EzNxwSN1gjNzEzW}
```

### New Learnings
I learned how double clicking tab can be used to show all options that can be used.

### References

## Tab completion on commands
Tab completion is for more than files! You can also tab-complete commands. This level has a command that starts with pwncollege, and it'll give you the flag. Type pwncollege and hit the tab key to auto-complete it!

NOTE: You can auto-complete any command, but be careful: callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands!

### Solve
**Flag:** `pwn.college{U79iPtCd3TsGJUEG_QFwYL2jV_7.0VN0EzNxwSN1gjNzEzW}`
 for this Challenge, i wrote pwncollege command and then used tab to auto complete the command and executed the command to get the flag.

```bash 
hacker@globbing~tab-completion-on-commands:~$ pwncollege-25290
Correct! Here is your flag:
pwn.college{U79iPtCd3TsGJUEG_QFwYL2jV_7.0VN0EzNxwSN1gjNzEzW}
```

### New Learnings
I learned how tab can also be used to auto complete commands.

### References

