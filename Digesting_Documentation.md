# Digesting Documentation

## Learning from Documentation
The typical need you'll have for documentation is just to figure out how to use all these dang programs, and a specific case of that is figuring out what arguments to specify on the command line. This module will mostly dig into that concept, as a proxy for figuring out how to use the programs in general. Through the rest of the module, you'll go through various ways of asking the environment for help for the programs, but first, we'll dig into the concept of reading documentation.

The correct usage of programs depends, in a large part, on the proper specification of arguments to them. Recall the -a of ls -a in the hidden files challenge of the Basic Commands module: that -a was an argument that told ls to list out hidden files as well as non-hidden files. Because we wanted to list out hidden files, invoking ls with the -a argument was the correct way to use it in our scenario.

The program for this challenge is /challenge/challenge, and you'll need to invoke it properly in order for it to give you the flag. Let's pretend that this is its documentation:

```bash
Welcome to the documentation for /challenge/challenge! To properly run this program, you will need to pass it the argument of --giveflag. Good luck!
```

Given that knowledge, go get the flag!

### Solve
**Flag:** `pwn.college{oBU-kIm6mvXTLJ8G3Dt8GtZ3WYJ.QX0ITO0wSN1gjNzEzW}`
 for this Challenge, i ran the program /challenge/challenge with argument as --giveflag as per its documentation to get the flag.

```bash 
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{oBU-kIm6mvXTLJ8G3Dt8GtZ3WYJ.QX0ITO0wSN1gjNzEzW}
```

### New Learnings
I learned the correct usage of programs is through refering its documentation.

### References

## Learning Complex Usage
While using most commands is straightforward, the usage of some commands can get quite complex. For example, the arguments to commands like sed and awk, which we're definitely not getting into right now, are entire programs in an esoteric programming language! Somewhere on the spectrum between cd and awk are commands that take arguments to their arguments...

This sounds crazy, but you've already encountered this with the find level in Basic Commands. find has a -name argument, and the -name argument itself takes an argument specifying the name to search for. Many other commands are analogous.

Here is this level's documentation for /challenge/challenge:

```bash
Welcome to the documentation for /challenge/challenge! This program allows you to print arbitrary files to the terminal, when given the --printfile argument. The argument to the --printfile argument is the path of the flag to read. For example, /challenge/challenge --printfile /challenge/DESCRIPTION.md will print out the description of the level!
```

Given that documentation, go get the flag!

### Solve
**Flag:** `pwn.college{0m-fO7-xZKx0IQbtlkS_Byj8Bz8.QX1ITO0wSN1gjNzEzW}`
 for this Challenge, i ran the program /challenge/challenge with argument as --printfile and another argument to that --printfile as /flag file to get the flag.

```bash 
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{0m-fO7-xZKx0IQbtlkS_Byj8Bz8.QX1ITO0wSN1gjNzEzW}
```

### New Learnings
I learned about the complex programs that take arguments for arguments and how to use them correctly.
### References

## Reading Manuals
This level introduces the man command. man is short for manual, and will display (if available) the manual of the command you pass as an argument. For example, let's say we wanted to learn about the yes command (yes, this is a real command):

```bash
hacker@dojo:~$ man yes
```
This will display the manual page for yes, which will look something like this:

```bash
YES(1)                           User Commands                          YES(1)

NAME
       yes - output a string repeatedly until killed

SYNOPSIS
       yes [STRING]...
       yes OPTION

DESCRIPTION
       Repeatedly output a line with all specified STRING(s), or 'y'.

       --help display this help and exit

       --version
              output version information and exit

AUTHOR
       Written by David MacKenzie.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report any translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright  ©  2020  Free Software Foundation, Inc.  License GPLv3+: GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       Full documentation <https://www.gnu.org/software/coreutils/yes>
       or available locally via: info '(coreutils) yes invocation'

GNU coreutils 8.32               February 2022                          YES(1)
```

The important sections are:

```bash
NAME(1)                           CATEGORY                          NAME(1)

NAME
	This gives the name (and short description) of the command or
	concept discussed by the page.

SYNOPSIS
	This gives a short usage synopsis. These synopses have a standard
	format. Typically, each line is a different valid invocation of the
	command, and the lines can be read as:

	COMMAND [OPTIONAL_ARGUMENT] SINGLE_MANDATORY_ARGUMENT
	COMMAND [OPTIONAL_ARGUMENT] MULTIPLE_ARGUMENTS...

DESCRIPTION
	Details of the command or concept, with detailed descriptions
	of the various options.

SEE ALSO
	Other man pages or online resources that might be useful.

COLLECTION                        DATE                          NAME(1)
```

You can scroll around the manpage with your arrow keys and PgUp/PgDn. When you're done reading the manpage, you can hit q to quit.

Manpages are stored in a centralized database. If you're curious, this database lives in the /usr/share/man directory, but you never need to interact with it directly: you just query it using the man command. The arguments to the man command aren't file paths, but just the names of the entries themselves (e.g., you run man yes to look up the yes manpage, rather than man /usr/bin/yes, which would be the actual path to the yes program but would result in man displaying garbage).

The challenge in this level has a secret option that, when you use it, will cause the challenge to print the flag. You must learn this option through the man page for challenge!

### Solve
**Flag:** `pwn.college{oPefkBHbLxM-TqJ4mDbZL6irbEg.QX0EDO0wSN1gjNzEzW}`
 for this Challenge, i used man command with argument as challenge to open its manual and found the option that is needed to be used to get the flag. then i ran the challenge command with that option and got the flag

```bash 
hacker@man~reading-manuals:~$ man challenge
hacker@man~reading-manuals:~$ /challenge/challenge --oefkbx 460
Correct usage! Your flag: pwn.college{oPefkBHbLxM-TqJ4mDbZL6irbEg.QX0EDO0wSN1gjNzEzW}
```

### New Learnings
I learned how to use man command to get the manual for a particular command which helps to know the different options there for that particular command.

### References

## Searching Manuals
You can scroll man pages with the arrow keys (and PgUp/PgDn) and search with /. After searching, you can hit n to go to the next result and N to go to the previous result. Instead of /, you can use ? to search backwards!

Find the option that will give you the flag by reading the challenge man page.

### Solve
**Flag:** `pwn.college{8gzd--8WTMIhlM-B7bk-PUC3ZnG.QX1EDO0wSN1gjNzEzW}`
for this Challenge, i used man command with argument as challenge to open its manual and navigated through the different options and found the option that is needed to be used to get the flag. then i ran the challenge command with that option and got the flag

```bash 
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ /challenge/challenge --whfixy
Initializing...
Correct usage! Your flag: pwn.college{8gzd--8WTMIhlM-B7bk-PUC3ZnG.QX1EDO0wSN1gjNzEzW}
```

### New Learnings
I learned to navigate through the many diffferent options and search for a particular option in the manual of a command.

### References
