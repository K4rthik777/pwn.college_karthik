# Data Manipulation

## Translating characters
One of the purposes of piping data is to modify it. Many Linux commands will help you modify data in really cool ways. One of these is tr, which translates characters it receives over standard input and prints them to standard output.

In its most basic usage, tr translates the character provided in its first argument to the character provided in its second argument:

```bash
hacker@dojo:~$ echo OWN | tr O P
PWN
hacker@dojo:~$
```

It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.

```bash
hacker@dojo:~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:~$
```

Now, you try it! In this level, /challenge/run will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). Can you undo it with tr and get the flag?


### Solve
**Flag:** `pwn.college{YBxxGNc8lbKS4OQ1tbPv6PIdb47.01MxEzNxwSN1gjNzEzW}`
 for this Challenge, i ran tr ---help to find useful info about the command options and found [:upper:] and [:lower:] can used together to swap case.Finally i ran /challenge/run with | with tr command with arguments [:upper:][:lower:] along with [:lower:][:upper:] to get the flag.

```bash 
hacker@data~translating-characters:~$ tr --help
Usage: tr [OPTION]... STRING1 [STRING2]
Translate, squeeze, and/or delete characters from standard input,
writing to standard output.  STRING1 and STRING2 specify arrays of
characters ARRAY1 and ARRAY2 that control the action.

  -c, -C, --complement    use the complement of ARRAY1
  -d, --delete            delete characters in ARRAY1, do not translate
  -s, --squeeze-repeats   replace each sequence of a repeated character
                            that is listed in the last specified ARRAY,
                            with a single occurrence of that character
  -t, --truncate-set1     first truncate ARRAY1 to length of ARRAY2
      --help        display this help and exit
      --version     output version information and exit

ARRAYs are specified as strings of characters.  Most represent themselves.
Interpreted sequences are:

  \NNN            character with octal value NNN (1 to 3 octal digits)
  \\              backslash
  \a              audible BEL
  \b              backspace
  \f              form feed
  \n              new line
  \r              return
  \t              horizontal tab
  \v              vertical tab
  CHAR1-CHAR2     all characters from CHAR1 to CHAR2 in ascending order
  [CHAR*]         in ARRAY2, copies of CHAR until length of ARRAY1
  [CHAR*REPEAT]   REPEAT copies of CHAR, REPEAT octal if starting with 0
  [:alnum:]       all letters and digits
  [:alpha:]       all letters
  [:blank:]       all horizontal whitespace
  [:cntrl:]       all control characters
  [:digit:]       all digits
  [:graph:]       all printable characters, not including space
  [:lower:]       all lower case letters
  [:print:]       all printable characters, including space
  [:punct:]       all punctuation characters
  [:space:]       all horizontal or vertical whitespace
  [:upper:]       all upper case letters
  [:xdigit:]      all hexadecimal digits
  [=CHAR=]        all characters which are equivalent to CHAR

Translation occurs if -d is not given and both STRING1 and STRING2 appear.
-t is only significant when translating.  ARRAY2 is extended to length of
ARRAY1 by repeating its last character as necessary.  Excess characters
of ARRAY2 are ignored.  Character classes expand in unspecified order;
while translating, [:lower:] and [:upper:] may be used in pairs to
specify case conversion.  Squeezing occurs after translation or deletion.

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Report any translation bugs to <https://translationproject.org/team/>
Full documentation <https://www.gnu.org/software/coreutils/tr>
or available locally via: info '(coreutils) tr invocation'
hacker@data~translating-characters:~$ /challenge/run | tr [:upper:][:lower:] [:lower:][:upper:]
yOUR CASE-SWAPPED FLAG:
pwn.college{YBxxGNc8lbKS4OQ1tbPv6PIdb47.01MxEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how tr command works to swap string array elements using different options.

### References

## Deleting characters
tr can also translate characters to nothing (i.e., delete them). This is done via a -d flag and an argument of what characters to delete:

```bash
hacker@dojo:~$ echo PAWN | tr -d A
PWN
hacker@dojo:~$
```

Pretty simple! Now you give it a try. I'll intersperse some decoy characters (specifically: ^ and %) among the flag characters. Use tr -d to remove them!

### Solve
**Flag:** ``
 for this Challenge, i ran  /challenge/run with | with tr command with -d option with argements ^% to get the flag.

```bash 
hacker@data~deleting-characters:~$ /challenge/run | tr -d ^%
Your character-stuffed flag:
pwn.college{4Ypc9Gw7WP2f6ay72DEhrsB_Zy2.0FNxEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how tr command with -d option works to delete the arguments in the specified string array.

### References

## Deleting newlines
A common class of characters to remove is a line separator. This happens when you have a stream of data that you want to turn into a single line for further processing. You can specify newlines almost like any other character, by escaping them:

```bash
hacker@dojo:~$ echo "hello_world!" | tr _ "\n"
hello
world!
hacker@dojo:~$
```

Here, the backslash (\) signifies that the character that follows it is a standin for a character that's hard to input into the shell normally. The newline, of course, is hard to input because when you typically hit Enter, you'll run the command itself. \n is a standin for this newline, and it must be in quotes to prevent the shell interpreter itself from trying to interpret it and pass it to tr instead.

Now, let's combine this with deletion. In this challenge, we'll inject a bunch of newlines into the flag. Delete them with tr's -d flag and the escaped newline specification!

Fun fact! Want to actually replace a backslash (\) character? Because \ is the escape character, you gotta escape it! \\ will be treated as a backslash by tr. This isn't relevant to this challenge, but is a fun fact nonetheless!

### Solve
**Flag:** `pwn.college{U_F6shJTv0VKr1RTYWOlMpWXVip.0VNxEzNxwSN1gjNzEzW}`
 for this Challenge, i ran  /challenge/run with | with tr command with -d option with arguments "\n" to get the flag.

```bash 
hacker@data~deleting-newlines:~$ /challenge/run | tr -d "\n"
Your line-split flag: pwn.college{U_F6shJTv0VKr1RTYWOlMpWXVip.0VNxEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how tr command with -d option works to delete the newlines "\n" in the specified string array.

### References

## Extracting the first lines with head
In your Linux journey, you'll experience situations where you need to grab just the early output of very verbose programs. For this, you'll reach for head! The head command is used to display the first few lines of its input:

```bash
hacker@dojo:~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:~$
```

By default, it shows the first 10 lines, but you can control this with the -n option:

```bash
hacker@dojo:~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:~$
```

This challenge's /challenge/pwn outputs a bunch of data, and you'll need to pipe it through head to grab just the first 7 lines and then pipe them onwards to /challenge/college, which will give you the flag if you do this right! Your solution will be a long composite command with two pipes connecting three commands. Good luck!

### Solve
**Flag:** `pwn.college{smpTgbYXhmVYiI0BDDGXa-CrWuI.0lNxEzNxwSN1gjNzEzW}`
 for this Challenge, i ran  /challenge/run with | with head command with -n option with 7 and /challenge/.codes with another | with /challenge/college to get the flag.

```bash 
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n
 7 /challenge/.codes | /challenge/college
Congratulations, you piped the right codes!
pwn.college{smpTgbYXhmVYiI0BDDGXa-CrWuI.0lNxEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how head command with -n option can be used to display specified number of lines of its input.

### References


## Extracting specific sections of text
Sometimes, you want to grab specific columns of data, such as the first column, the third column, or the 42nd column. For this, there's the cut command.

For example, imagine that you have the following data file:

```bash
hacker@dojo:~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
```
You could use cut to extract specific columns:

```bash
hacker@dojo:~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:~$
```

The -d argument specifies the column delimiter (how columns are separated). In this case, it's a space character. Of course, it has to be in quotes here so that the shell knows that the space is an argument rather than a space separating other arguments! The -f argument specifies the field number (which column to extract).

In this challenge, the /challenge/run program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns. Use cut to extract the flag characters, then pipe them to tr -d "\n" (like the previous level!) to join them together into a single line. Your solution will look something like /challenge/run | cut ??? | tr ???, with the ??? filled out.

### Solve
**Flag:** `pwn.college{smpTgbYXhmVYiI0BDDGXa-CrWuI.0lNxEzNxwSN1gjNzEzW}`
 for this Challenge, i ran  /challenge/run with | with cut command with -d option with " " with -f option with 2 (got this as the right number by trial abd error) with another | with tr -d "\n" to get the flag.

```bash 
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d " " -f 2| tr -d "\n"
pwn.college{ocA3Ygbv1lxzVtRm7PnJZEMQEk3.01NxEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how cut command with -d option and -f option have to be used to extract specified column of its input.

### References

## Sorting data
Files (or output lines of commands) aren't always in the order you need them! The sort command helps you organize data. It reads lines from input (or files) and outputs them in sorted order:

```bash
hacker@dojo:~$ cat names.txt
  hack
  the
  planet
  with
  pwn
  college
hacker@dojo:~$ sort names.txt
  college
  hack
  planet
  pwn
  the
  with
hacker@dojo:~$
```

By default, sort orders lines alphabetically. Arguments can change this:

-r: reverse order (Z to A)
-n: numeric sort (for numbers)
-u: unique lines only (remove duplicates)
-R: random order!
In this challenge, there's a file at /challenge/flags.txt containing 100 fake flags, with the real flag mixed among them. When sorted alphabetically, the real flag will be at the end (we made sure of this when generating fake flags). Go get it!

### Solve
**Flag:** `pwn.college{cUI2torve4oEgmqSQvft97lOMa8.0FM0MDOxwSN1gjNzEzW}`
 for this Challenge, i ran sort command with /challenge/flags.txt file as argument and the last flag was the correct one.

```bash 
hacker@data~sorting-data:~$ sort /challenge/flags.txt
ovn.cnkldgd{bTH1torud3oDgmpRQufs97lOMa8.0EL0LDOxwSN0fiNzEyW}
ovn.cokkdge{cUI1toque4oDgmqSPvft97lOMa8.0EL0MCOwwSN0fjMzEzW}
ovn.colldgd{cUI2torve4oEgmqSQvft97kOMa7.0FM0MDOxwSN1gjNzDzW}
owm.bolldge{bUI2tnrve4oEfmqSQufs97lOMa8.0FL0MCOxwSN0gjMzEzV}
owm.coklege{cUI2torve4oEgmqSPvfs97lOLa8.0FM0LDNxwRM1gjNzEyW}
owm.colkege{bUI2tnrue3oEglpRQvfs96lOMa8.0FM0LDOwwSN0fjNzEzW}
owm.colldge{cTI1snrve4oEgmqRQuft96lOMa8.0FM0MDOxwSN0fjNzEzW}
own.bnllege{cUH2toqve4oEgmqSQves87lNMa8.0EL0MDNxwRN1gjNzEyV}
own.boklegd{cUH2torud4nEglqRPvet86lNLa8.0FM0MDOxwSM1giNzEyW}
own.boklege{cUI2tnrvd3oEfmqSQvft87kNMa7.0FM0MCOxwRN1fiNyDyW}
own.bollegd{cTI2torue3nEgmqRQvet87kOLa8.0FM0LDNxwSN1gjNzDzV}
own.bollege{cUH2sorve4oEgmqSQvfs86lOMa8.0FM0MDOxwSM0gjNyEzV}
own.bollege{cUI2toqve4oEfmqSQvft97lOMa8.0FM0MCOwwSN1gjNzEzW}
own.cnlldge{cTI2toqve4oDglqSQvet97lNMa8.0FM0MDNwwSN1gjNzEzW}
own.cnllege{cTH1sorve3nEfmqSQvft97lOMa8.0FM0LCOwwSM1giNyEzW}
own.cnllege{cTI2toqvd4oEflqRQvft87lOMa7.0FM0LDNxwRN1gjNzEyW}
own.cokldfe{bTI2sorvd4oEflpSQves97lNLa8.0EL0MDOxwSN1giNzDzW}
own.coklegd{cUI2torud4nEfmqRPufs97lOLa8.0EM0MDOwwSN0gjMzEzV}
own.coklege{bUH2sorve3oEgmqSQvft97lNMa8.0EM0MDOxwSN1gjNyEzW}
own.coklege{cUI2torud4oEgmqSQvft87lNLa7.0FM0MDOxwSM1gjNzEzW}
own.colkege{cUI2tnrvd3oEgmqRQvft96lOMa7.0EM0MCOwwRN0giNzEyW}
own.colkege{cUI2toqve4oDgmpSQves97lNMa8.0EM0MDNxwSN1fjMyDzV}
own.colldge{bTI1torve4nDgmqSPvft86lNMa8.0FM0LDOxwSM1fiNzDyW}
own.college{cTH2sorvd4oEflqSQvfs87kNLa7.0FL0MDNxvSN1gjNzEzW}
own.college{cUI2torve3oEfmqSQvfs86lOMa8.0FM0MDNxwSN1gjNzEzW}
pvm.bokkdfe{bUI1torve4oEgmqSQvft86lOMa8.0FM0MDOxwRM1gjNzEzW}
pvm.boklegd{cUI1tnqve3oEfmpSQuft96lNMa8.0EM0LCNxwSM0gjNyEyW}
pvm.boklege{cTH2toqvd3nEgmqRQvfs96lOLa8.0FM0MDOxwSM1gjNzDzV}
pvm.bolkdge{cUH1sorud3oDglpRQuet97lNMa8.0FM0LDNxvSN1gjNzDzV}
pvm.bollefe{cUI2soqve4oEgmqSQvft97lOMa8.0FM0LDOxwSN1fjNyEzW}
pvm.coklege{cUI2soque4oEgmqSQvfs96lOMa8.0FL0LDNxvSN1gjNyEzW}
pvm.college{bUI2torve4nDgmqSQvft87kOLa8.0FM0MDOxvSN1giMyDzW}
pvn.bnkkege{cUI2soqvd4oEfmqSPvft97lNMa8.0FL0MCOxwSN0fjNzEzW}
pvn.bnllefe{bUI2torud4oDfmqRPvfs97lOMa7.0FM0MCOxwRM1fjNyEzW}
pvn.bokkefe{cUI1torve4oEgmqSPufs86kOMa8.0FM0MDNxvSN1gjNzEzV}
pvn.boklege{cUH2snque4oEfmqSPvft97lOLa8.0FM0MDOxwSN1gjNzEzW}
pvn.bolldge{bUI2tnrud4oEgmqRPuft87kOMa8.0FM0MDNxwRN0fiMzEyW}
pvn.cnllefd{cUI1sorve4oEgmpSQvet87kOMa8.0FM0LDOwvSM0giMyEzW}
pvn.coklegd{cUI1tnrve3oEglqSQvet87lOMa7.0FM0LDOxwSM1gjNzEzW}
pvn.colkege{cUI2snrve4oEfmqRPvft96lNLa8.0FM0MDOxwSN1gjMzEzW}
pvn.collefe{bUI2torue3oEflqSQuft97lNMa8.0EM0LDNxwRN1giNzEzW}
pvn.college{bTI2tnrve3nEgmqSQves97lNLa8.0FM0MDOxwSN1gjNzEzW}
pvn.college{cUI2torve4oEgmqSQvft97lOMa8.0FM0MDOxwSN1gjNzEzW}
pwm.bokkegd{cUI2tnrve4oDfmpRPvft86lOLa8.0EM0MDOwvSN1giNyDzW}
pwm.bolkege{cUH1sorue4nEgmpSPvft97kOMa8.0FM0LDOxwSN1fjNzDzV}
pwm.cnllefe{cUH2torvd4oEgmqRQuft97lNMa7.0FM0MCOxwSN1gjMzEzW}
pwm.colldge{cUI2torve4oEgmqSQuft97lOLa8.0FM0MDOxvSN0gjNzEzW}
pwm.collefe{cUI2tnrve4oEgmpSPvft97lOMa8.0FM0MDOxwSN1gjNzEzW}
pwm.college{cUI2torve4oEgmqSQvft97lOMa8.0FM0MDOxwRN1gjNzEyW}
pwn.bnlkege{cTH2tnqve4nEgmqSPufs97kNMa8.0EM0MCNwwSM1giMzEyW}
pwn.bnllege{cUI1torvd4oEgmpSQuet97lNLa8.0EL0MCNxwSN0fiNzDzW}
pwn.bokkefd{bUI2torvd4oEgmqSQvfs87kOMa8.0FM0MDNxwSN1fjNzEzW}
pwn.bokldge{cUI2torvd4oEglqRPvft96lNLa8.0EM0MDOxwSM0giNyEyV}
pwn.bolkege{cTI2torud4nEgmqSPuet97kOLa7.0FL0MDOxwSM1gjNzEyW}
pwn.bolkege{cUI2torve4oEgmpSQvft87lOMa8.0FL0MCNxvSN1gjNzEzV}
pwn.bolldge{cTH2sorve3oEgmpSQves97lOLa8.0EM0LDNwwSM1fjMzDzW}
pwn.bollefe{cUI1sorve4oEgmqSQvft97lOLa7.0FM0MDNxwSN1giNzDzW}
pwn.bollege{cUI1torue4nEglqSQvft97lOMa8.0FL0MDOxwSN1gjNzDzW}
pwn.bollege{cUI2torve4oEgmqSQvft96lOMa8.0FM0MDOwwSN1gjNzEzW}
pwn.cnklegd{cUI2sorud4oEfmpSPvft96lNLa8.0EM0MCOxvRN1giNzDyW}
pwn.cnlkdfe{cUI2sorvd4oEflqSPves86kNLa8.0EM0MDOwwSN0gjNyEyW}
pwn.cnlkege{cUI2tnrve4oEgmqSPvet86lOMa8.0FM0MDOxwSN1gjNzEzW}
pwn.cnlldgd{cUI2sorud3nEglpSQues96kNMa8.0FM0LCOxwSM1gjMzEzW}
pwn.cnllegd{cUI2torve4oEfmqSQues97lOMa7.0EM0MDOwvRN1gjNyEzV}
pwn.cokldge{cTI2snqve4oEgmqRQvft97kOMa8.0FM0MDOxwRM1gjNzEyW}
pwn.coklefd{cUI2torvd4oEgmqSQvft97lOMa7.0EM0LCOxvSM1fjNzDzV}
pwn.coklefe{cUI2torve4nDgmqSQvet87lOLa8.0FM0MDOxvSN1fjMzEzV}
pwn.coklegd{bUI1torve4oEgmqSPvft97lOMa8.0FM0MDNxwSN1giMzEyV}
pwn.coklege{cTI1sorve3oEgmpRPvet96lOMa7.0FM0MDNwwRN1giMyEzW}
pwn.coklege{cTI2snrve4oEfmqSQuft97lNMa8.0EM0LDNxwSM1gjNzDzV}
pwn.coklege{cTI2torve3oEglpRPvft86lOLa8.0EL0MCNxwRM1gjNyDzV}
pwn.colkdgd{bUI2torve4oDglqRQuet96lOLa7.0FM0MDNxvRM1giNyEzW}
pwn.colkegd{cUI2torve4oDgmpRPves96lOMa8.0FM0MCOwvSN1giNzEzV}
pwn.colkege{bUI1torue3oEgmpSPvet97kOMa8.0FL0MDOxwSN1gjMzEzV}
pwn.colkege{cUI2toqve3nEfmqSQvft97lOMa8.0FM0LDOxwSM1gjNyDzW}
pwn.colkege{cUI2torve4oEgmqSQvft87lOMa8.0FM0MDOxwSN1gjNzEzW}
pwn.colldfe{cUI2torve4oEgmqSQvft97lOMa8.0FM0MCOxwSN1giNzEyW}
pwn.colldge{cTI2torvd4oEfmqSQvft87lOMa7.0FM0MDOwwRM1giMyEzW}
pwn.colldge{cUH2soqvd4oEglqSPvft97lOMa8.0EM0LDOxwSN1gjNzEzW}
pwn.colldge{cUI2toqve3oEflqSQvft97kOMa8.0FM0MDOxvSN0gjNyEzV}
pwn.collegd{cTH2tnrvd4oEglpRPvfs97lNMa7.0FL0MDOxwSN1fiNzDzW}
pwn.collegd{cTI2torud3nEgmqRQuft96kOMa8.0FL0LDNwvSN1giMyEyW}
pwn.collegd{cUI2torud3oEfmqSPvft97lOMa8.0EM0MDOxwSN1gjNzEyW}
pwn.collegd{cUI2torve4nEglqSQves96lOMa7.0FM0MDOxwSM1gjNzEzW}
pwn.collegd{cUI2torve4oEflqSQvfs97lOMa8.0FM0MDOxwSN1giNzEzW}
pwn.collegd{cUI2torve4oEglqRQvft96lOMa8.0FM0MDOxwSN1gjNyEyW}
pwn.collegd{cUI2torve4oEgmqSQvft97lOMa8.0FM0MDOxwSN1giNzEzW}
pwn.college{bUI2torve4nDglqSQvft97lOMa8.0FM0MDNxwSN1gjNzEzV}
pwn.college{cUH2torve4oEgmpSPuft97lOLa7.0FM0MDOxwSN1fjNzEzW}
pwn.college{cUI1snrve4oDfmqSQvft87kNMa8.0FM0LDOxwRN1gjMzEzW}
pwn.college{cUI1torve3nEglqSQvft97lOMa8.0EM0MCOxwSN0gjNzDzW}
pwn.college{cUI2toqve4nEglqSQvft97lNMa8.0EM0MDOxwSM1gjNzEyW}
pwn.college{cUI2torud4oDgmqSPvft87kNMa8.0FL0MDNxwSN1fjNyEzW}
pwn.college{cUI2torue4nDgmqSQuft97lOMa8.0FM0MDOxwSM0fjNzEyV}
pwn.college{cUI2torue4oEgmqSQvft97lOMa8.0FM0MDNxwSN1gjNzEzW}
pwn.college{cUI2torve4oEfmqSQvft97lOMa8.0EM0MDOxwSN0fjNzDzW}
pwn.college{cUI2torve4oEgmqSQvet97lOMa8.0FM0MDOxwSN1gjNzEzW}
pwn.college{cUI2torve4oEgmqSQvft97lOLa8.0FM0MDOxwSN1gjNzEzV}
pwn.college{cUI2torve4oEgmqSQvft97lOMa8.0FM0MCOxwSN0gjNzEzW}
pwn.college{cUI2torve4oEgmqSQvft97lOMa8.0FM0MDOxwSN1giNzEzW}
pwn.college{cUI2torve4oEgmqSQvft97lOMa8.0FM0MDOxwSN1gjNzEzW}
```

### New Learnings
I learned how sort command can be used to arrange the data of a file or output of a command in required order using its different options.

### References