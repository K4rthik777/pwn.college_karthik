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