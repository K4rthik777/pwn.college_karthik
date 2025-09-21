#  Pondering Paths

## The Root 
You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path".

### Solve
**Flag:** `pwn.college{IjLW89nFt4iAnPqIj-f_HHajrKT.QX4cTO0wSN1gjNzEzW}`
 for this Challenge, i just invoked the program pwn by using its absolute path /pwn to get the flag.

```bash 
/pwn
pwn.college{IjLW89nFt4iAnPqIj-f_HHajrKT.QX4cTO0wSN1gjNzEzW}
```

### New Learnings
I learned how to invoke a program using its absolute path in linux terminal

### References

## Program and absolute paths 
Challenges in pwn.college are in the challenge directory and the challenge directory is, in turn, right in the root directory (/). The path to the challenge directory is, thus, /challenge. The name of the challenge program in this level is run, and it lives in the /challenge directory.This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the run file that is in the challenge directory that is, in turn, in the / directory.

### Solve
**Flag:** `pwn.college{444tdUIaI68_bP2Eh6WlXrM_bet.QX1QTN0wSN1gjNzEzW}`
 for this Challenge, i just invoked the program run by using its absolute path /challenge/run to get the flag.

```bash 
/challenge/run
pwn.college{444tdUIaI68_bP2Eh6WlXrM_bet.QX1QTN0wSN1gjNzEzW}
```

### New Learnings
I learned how to invoke a program with a more complicated location using its absolute path in linux terminal

### References

## Position thy self 
This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program.

### Solve
**Flag:** `pwn.college{oaNc3XR049R1iZiYQdvaWrnqCn8.QX2QTN0wSN1gjNzEzW}`
 for this Challenge, i changed the directory to specified one that i got after initially running the program and then again invoked the program run by using its absolute path /challenge/run to get the flag.

```bash 
/challenge/run
cd /proc/144/fd 
/challenge/run
pwn.college{oaNc3XR049R1iZiYQdvaWrnqCn8.QX2QTN0wSN1gjNzEzW}
```

### New Learnings
I learned how to change a directory in terminal and then from within it invoke a program with a more complicated location using its absolute path in linux terminal

### References

## Position yet elsewhere 
This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program.

### Solve
**Flag:** `pwn.college{YzDP-ce-7W55zW_iSablI0w38ik.QX4QTN0wSN1gjNzEzW}`
 for this Challenge, i changed the directory to specified one that i got after initially running the program and then again invoked the program run by using its absolute path /challenge/run to get the flag.

```bash 
/challenge/run
cd /var 
/challenge/run
pwn.college{YzDP-ce-7W55zW_iSablI0w38ik.QX4QTN0wSN1gjNzEzW}
```

### New Learnings
I learned how to change a directory in terminal and then from within it invoke a program with a more complicated location using its absolute path in linux terminal

### References

## Implicit relative paths, from / 
This challenge will require you to run /challenge/run using a relative path while having a current working directory of /.

### Solve
**Flag:** `pwn.college{wgFyKNopRWYbGvwZC2xtY0lkdwy.QX5QTN0wSN1gjNzEzW}`
 for this Challenge, i changed the directory to specified one that i got after initially running the program and then again invoked the program run by using its relative path challenge/run to get the flag.

```bash 
/challenge/run
cd /
challenge/run
pwn.college{wgFyKNopRWYbGvwZC2xtY0lkdwy.QX5QTN0wSN1gjNzEzW}
```

### New Learnings
I learned how to change a directory in terminal and then from within it invoke a program with a more complicated location using its implicit relative path in linux terminal

### References

## Explicit relative paths, from / 
This challenge will require you to invoke /challenge/run using . in the relative path i.e explicit relative path while having a current working directory of /

### Solve
**Flag:** `pwn.college{E65e30900SlOVYFwOhqBYmBNqKt.QXwUTN0wSN1gjNzEzW}`
 for this Challenge, i changed the directory to specified one that i got after initially running the program and then again invoked the program run by using its relative path ./challenge/run to get the flag.

```bash 
/challenge/run
cd /
./challenge/run
pwn.college{E65e30900SlOVYFwOhqBYmBNqKt.QXwUTN0wSN1gjNzEzW}
```

### New Learnings
I learned how to change a directory in terminal and then from within it invoke a program with a more complicated location using its explicit relative path in linux terminal

### References

## Implicit relative path
This challenge will require you to invoke /challenge/run using . in the relative path while having a current working directory of /challenge

### Solve
**Flag:** `pwn.college{UFYdf3j2KID6GAUa6WDdVrbN3Cn.QXxUTN0wSN1gjNzEzW}`
 for this Challenge, i changed the directory to specified one that i got after initially running the program and then again invoked the program run by using its relative path ./run to get the flag.

```bash 
/challenge/run
cd /challenge
./run
pwn.college{UFYdf3j2KID6GAUa6WDdVrbN3Cn.QXxUTN0wSN1gjNzEzW}
```

### New Learnings
I learned how to change a directory in terminal and then from within it invoke a program with a more complicated location using its relative path in linux terminal

### References

## Home sweet home
In this challenge, /challenge/run will write a copy of the flag to any file you specify as an argument on the commandline, with these constraints:

 >Your argument must be an absolute path.
 >The path must be inside your home directory.
 >Before expansion, your argument must be three characters or less.
Again, you must specify your path as an argument to /challenge/run

### Solve
**Flag:** `pwn.college{sT6WnSe-CI2XMQogPwOMIDm-pPy.QXzMDO0wSN1gjNzEzW}}`
 for this Challenge, i invoked the program /challenge/run with argument as ~/~ to get the flag.

```bash 
/challenge/run ~/~
pwn.college{sT6WnSe-CI2XMQogPwOMIDm-pPy.QXzMDO0wSN1gjNzEzW}
```

### New Learnings
I learned that expansion of ~ is the absolute path of /home/user and the expansion of ~/~ is only /home/user/~

### References