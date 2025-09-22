#  Pondering Paths

## cat: not the pet, but the command!
One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:

```bash
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files, like so:
```

cat will concatenate (hence the name) multiple files if provided multiple arguments. For example:

```bash
hacker@dojo:~$ cat myfile
This is my file!
hacker@dojo:~$ cat yourfile
This is your file!
hacker@dojo:~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
```

Finally, if you give no arguments at all, cat will read from the terminal input and output it. We'll explore that in later challenges...

In this challenge, I will copy the flag to the flag file in your home directory (where your shell starts). Go read it with cat!

### Solve
**Flag:** `pwn.college{MwR30opTR7hMSPRf_6mvt1bssns.QXxcTN0wSN1gjNzEzW}`
 for this Challenge, i used cat command with argument as flag file to get the flag.

```bash 
cat flag
pwn.college{MwR30opTR7hMSPRf_6mvt1bssns.QXxcTN0wSN1gjNzEzW}
```

### New Learnings
I learned how to use cat command to read a file in linux terminal

### References

## catting absolute paths
In the last level, you did cat flag to read the flag out of your home directory! You can, of course, specify cat's arguments as absolute paths:

```bash
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
```

In this directory, I will not copy it to your home directory, but I will make it readable. You can read it with cat at its absolute path: /flag.

FUN FACT: /flag is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

### Solve
**Flag:** `pwn.college{MwR30opTR7hMSPRf_6mvt1bssns.QXxcTN0wSN1gjNzEzW}`
 for this Challenge, i used cat command with argument as flag file to get the flag.

```bash 
cat flag
pwn.college{MwR30opTR7hMSPRf_6mvt1bssns.QXxcTN0wSN1gjNzEzW}
```

### New Learnings
I learned how to use cat command to read a file in linux terminal

### References

## more catting practice
You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for you. You must retrieve the flag by absolute path, wherever it is.

### Solve
**Flag:** `pwn.college{YU-BHw-bmQePXl4wqgSbQ9HtRBr.QXwITO0wSN1gjNzEzW}`
 for this Challenge, i used cat command with argument as absolute path of flag file to get the flag.

```bash 
cat /usr/share/mime-info/flag
pwn.college{YU-BHw-bmQePXl4wqgSbQ9HtRBr.QXwITO0wSN1gjNzEzW}
```

### New Learnings
I learned how to use cat command to read a file with its absolute path  in linux terminal

### References

## grepping for a needle in a haystack
Sometimes, the files that you might cat out are too big. Luckily, we have the grep command to search for the contents we need! We'll learn it in this challenge.

There are many ways to grep, and we'll learn one way here:

```bash
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```

Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

In this challenge, I've put a hundred thousand lines of text into the /challenge/data.txt file. grep it for the flag!

HINT: The flag always starts with the text pwn.college.

### Solve
**Flag:** `pwn.college{YaDnignexKYO1DkrT71ggp4yZ4t.QX3EDO0wSN1gjNzEzW}`
 for this Challenge, the absolute path of data.txt file to get the flag. i used grep command with arguments - pwn.college as the search_string and

```bash 
grep pwn.college /challenge/data.txt
pwn.college{YaDnignexKYO1DkrT71ggp4yZ4t.QX3EDO0wSN1gjNzEzW}
```

### New Learnings
I learned how to use grep command to search for a specific lines in a large file with a search_string and the file's absolute path in linux terminal

### References

## comparing two files
When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the diff command becomes invaluable.

diff compares two files line by line and shows you exactly what's different between them. For example:
```bash
hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
```
The output tells us that line 2 changed (2c2), with world in the first file (<) being replaced by universe in the second file (>).

Sometimes, when new lines are added, you'll see something like:

```bash
hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
```

This tells us that after line 1 in the first file, the second file has an additional line (1a2 means "after line 1 of file1, add line 2 of file2").

Now for your challenge! There are two files in /challenge:

  /challenge/decoys_only.txt contains 100 fake flags
  /challenge/decoys_and_real.txt contains all 100 fake flags plus the one real flag
Use diff to find what's different between these files and get your flag!

### Solve
**Flag:** `pwn.college{oV19UG19pl1azyMC2xCN_sp-sFc.01MwMDOxwSN1gjNzEzW}`
 for this Challenge, the absolute path of data.txt file to get the flag. i used grep command with arguments - pwn.college as the search_string and

```bash 
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
13a14
> pwn.college{oV19UG19pl1azyMC2xCN_sp-sFc.01MwMDOxwSN1gjNzEzW}
```

### New Learnings
I learned how to use diff commmand to find the differentiating lines in two files 
### References

## listing files
You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for you. You must retrieve the flag by absolute path, wherever it is.So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the ls command!

ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:

```bash
hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
```

In this challenge, we've named /challenge/run with some random name! List the files in /challenge to find it.

### Solve
**Flag:** `pwn.college{YY_Ih4X0RwCtMsON3zeXacgl6dm.QX4IDO0wSN1gjNzEzW}`
 for this Challenge, i changed the directory first to the root and then listed the challlenge dirtectory to view the required file name and then invoked that file using its absolute path to get the flag.

```bash 
hacker@commands~listing-files:~$ cd /
hacker@commands~listing-files:/$ ls challenge
28202-renamed-run-3876  DESCRIPTION.md
hacker@commands~listing-files:/$ /challenge/28202-renamed-run-3876
Yahaha, you found me! Here is your flag:
pwn.college{YY_Ih4X0RwCtMsON3zeXacgl6dm.QX4IDO0wSN1gjNzEzW}
```

### New Learnings
I learned how to use ls command to list all files within a specific directory

### References

## touching files
Of course, you can also create files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by touching it with the touch command:

```bash
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
```

It's that simple! In this level, please create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get your flag!

### Solve
**Flag:** `pwn.college{w8blaFX9xchm1c48UPOAV0rqaim.QXwMDO0wSN1gjNzEzW}`
 for this Challenge, i used cat command with argument as absolute path of flag file to get the flag.

```bash 
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{w8blaFX9xchm1c48UPOAV0rqaim.QXwMDO0wSN1gjNzEzW}
```

### New Learnings
I learned how to use touch command to new files in linux terminal

### References

## removing files 
Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you remove files with the rm command, as so:

```bash
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```

Let's practice. This challenge will create a delete_me file in your home directory! Delete it, then run /challenge/check, which will make sure you've deleted it and then give you the flag

### Solve
**Flag:** `pwn.college{EzaF_D4QcdcssHtBEIFXwNFEJC6.QX2kDM1wSN1gjNzEzW}`
 for this Challenge, i used rm command with argument as the delete_me file and then invoked /challenge/check to get the flag.

```bash 
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{EzaF_D4QcdcssHtBEIFXwNFEJC6.QX2kDM1wSN1gjNzEzW}
```

### New Learnings
I learned how to use rm command to delete a file in linux terminal

### References

## moving files
You can also move files around with the mv command. The usage is simple:

```bash
hacker@dojo:~$ ls
my-file
hacker@dojo:~$ cat my-file
PWN!
hacker@dojo:~$ mv my-file your-file
hacker@dojo:~$ ls
your-file
hacker@dojo:~$ cat your-file
PWN!
hacker@dojo:~$
```

This challenge wants you to move the /flag file into /tmp/hack-the-planet (do it)! When you're done, run /challenge/check, which will check things out and give the flag to you.

### Solve
**Flag:** `pwn.college{oALeARBPQMIqcKcY0BdG1bvXpsD.0VOxEzNxwSN1gjNzEzW}`
 for this Challenge, i used mv command to move /flag to /tmp/hack-the planet and then invoked /challenge/check to get the flag.

```bash 
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{oALeARBPQMIqcKcY0BdG1bvXpsD.0VOxEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how to use mv command to move one file to another file in linux terminal

### References

## hidden files
Interestingly, ls doesn't list all the files by default. Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts. To view them with ls, you need to invoke ls with the -a flag, as so:

```bash
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```

Now, it's your turn! Go find the flag, hidden as a dot-prepended file in /.


### Solve
**Flag:** `pwn.college{ISBuzzf09Eifg7dEyL3W6xghaUr.QXwUDO0wSN1gjNzEzW}`
 for this Challenge,first i change the cwd to root and then used ls command with -a flag and then used cat command to read the hidden file to get the flag.

```bash 
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv           bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-2500319804567  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat /.flag-2500319804567
pwn.college{ISBuzzf09Eifg7dEyL3W6xghaUr.QXwUDO0wSN1gjNzEzW}
```

### New Learnings
I learned how to use ls command with -a flag to list hidden files( dot-prepended files) within a particular directory in linux terminal.

### References

## An Epic Filesystem Quest
With your knowledge of cd, ls, and cat, we're ready to play a little game!

We'll start it out in /. Normally:

```bash
hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
```

That's a lot of contents! One day, you will be quite familiar with them, but already, you might recognize the flag file and the challenge directory.

In this challenge, I have hidden the flag! Here, you will use ls and cat to follow my breadcrumbs and find it! Here's how it'll work:

Your first clue is in /. Head on over there.
Look around with ls. There'll be a file named HINT or CLUE or something along those lines!
cat that file to read the clue!
Depending on what the clue says, head on over to the next directory (or don't!).
Follow the clues to the flag!

### Solve
**Flag:** `c`
 for this Challenge, first i changed the directory to root and then list all the file in it to find the EVIDENCE file and then catted that file to get the next clue. The next clue was to use ls -a to find hidden files in the specified directory (/usr/share/perl/5.30.0/unicore/lib/CWU). i then changed the directory to  (/usr/share/perl/5.30.0/unicore/lib/CWU) and listed files in it using ls -a and found .LEAD file and then catted it to find the next clue.The next clue was to change directory to (/usr/share/racket/pkgs/realm/chapter2/compiled) and list all files in it to find the next clue. Upon changing to get the flag.

```bash 
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls -a
.   .dockerenv  bin   challenge  etc   home  lib32  libx32  mnt  opt   root  sbin  sys  usr
..  EVIDENCE    boot  dev        flag  lib   lib64  media   nix  proc  run   srv   tmp  var
hacker@commands~an-epic-filesystem-quest:/$ cat EVIDENCE
Yahaha, you found me!
The next clue is in: /usr/share/perl/5.30.0/unicore/lib/CWU
The next clue is hidden  its filename starts with a '.' character. You'll need to look for it using special options to 'ls'
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/share/perl/5.30.0/unicore/lib/CWU
hacker@commands~an-epic-filesystem-quest:/usr/share/perl/5.30.0/unicore/lib/CWU$ ls -a
.  ..  .LEAD  Y.pl
hacker@commands~an-epic-filesystem-quest:/usr/share/perl/5.30.0/unicore/lib/CWU$ cat .LEAD
Yahaha, you found me!
The next clue is in: /usr/share/racket/pkgs/realm/chapter2/compiled

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/share/perl/5.30.0/unicore/lib/CWU$ cd /usr/share/racket/pkgs/realm/chapter2/compiled
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/realm/chapter2/compiled$ ls -a
.  ..  TIP  source_rkt.dep  source_rkt.zo
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/realm/chapter2/compiled$ cat TIP
Great sleuthing!
The next clue is in: /usr/share/racket/pkgs/scribble-lib/scribble/base/lang

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/realm/chapter2/compiled$ ls /usr/share/racket/pkgs/scribble-lib/scribble/base/lang
SECRET-TRAPPED  compiled  reader.rkt
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/realm/chapter2/compiled$ cd
hacker@commands~an-epic-filesystem-quest:~$ cat /usr/share/racket/pkgs/scribble-lib/scribble/base/lang/SECRET-TRAPPED
Lucky listing!
The next clue is in: /usr/share/racket/pkgs/net-cookies

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:~$ ls -a /usr/share/racket/pkgs/net-cookies
.  ..  .BLUEPRINT  LICENSE.txt  info.rkt
hacker@commands~an-epic-filesystem-quest:~$ cat /usr/share/racket/pkgs/net-cookies/.BLUEPRINT
Tubular find!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX-Web/SansSerif

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:~$ cd /usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX-Web/SansSerif
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX-Web/SansSerif$ ls
Bold  BoldItalic  Italic  Regular  SPOILER
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX-Web/SansSerif$ cat SPOILER
Tubular find!
The next clue is in: /opt/linux/linux-5.4/arch/mips/alchemy
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/STIX-Web/SansSerif$ cd
hacker@commands~an-epic-filesystem-quest:~$ ls -a /opt/linux/linux-5.4/arch/mips/alchemy
.   Kconfig   POINTER   board-gpr.c   board-xxs1500.c  devboards
..  Makefile  Platform  board-mtx1.c  common
hacker@commands~an-epic-filesystem-quest:~$ cat /opt/linux/linux-5.4/arch/mips/alchemy/POINTER
Congratulations, you found the clue!
The next clue is in: /usr/share/docutils/scripts
hacker@commands~an-epic-filesystem-quest:~$ ls -a /usr/share/docutils/scripts
.  ..  CLUE  python3
hacker@commands~an-epic-filesystem-quest:~$ cat /usr/share/docutils/scripts/CLUE
Congratulations, you found the clue!
The next clue is in: /usr/lib/python3/dist-packages/ipython_genutils/tests

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:~$ cd /usr/lib/python3/dist-packages/ipython_genutils/tests
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/ipython_genutils/tests$ ls
SNIPPET  __init__.py  __pycache__  test_importstring.py  test_path.py  test_tempdir.py  test_text.py
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/ipython_genutils/tests$ cat SNIPPET
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{kqNs6MB92DEw3B4S5Syl41o9Oeo.QX5IDO0wSN1gjNzEzW}

```

### New Learnings
I learned how to use cat command to read a file with its absolute path  in linux terminal

### References