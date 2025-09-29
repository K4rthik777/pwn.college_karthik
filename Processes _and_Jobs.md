# Processes and Jobs

## Listing Processes
First, we will learn to list running processes using the ps command. Depending on whom you ask, ps either stands for "process snapshot" or "process status", and it lists processes. By default, ps just lists the processes running in your terminal, which honestly isn't very useful:

```bash
hacker@dojo:~$ ps
    PID TTY          TIME CMD
    329 pts/0    00:00:00 bash
    349 pts/0    00:00:00 ps
hacker@dojo:~$
```

In the above example, we have the shell (bash) and the ps process itself, and that's all that's running on that specific terminal. We also see that each process has a numerical identifier (the Process ID, or PID), which is a number that uniquely identifies every running process in a Linux environment. We also see the terminal on which the commands are running (in this case, the designation pts/0), and the total amount of cpu time that the process has eaten up so far (since these processes are very undemanding, they have yet to eat up even 1 second!).

In the majority of cases, this is all that you'll see with a default ps. To make it useful, we need to pass a few arguments.

As ps is a very old utility, its usage is a bit of a mess. There are two ways to specify arguments.

"Standard" Syntax: in this syntax, you can use -e to list "every" process and -f for a "full format" output, including arguments. These can be combined into a single argument -ef.

"BSD" Syntax: in this syntax, you can use a to list processes for all users, x to list processes that aren't running in a terminal, and u for a "user-readable" output. These can be combined into a single argument aux.

These two methods, ps -ef and ps aux, result in slightly different, but cross-recognizable output.

Let's try it in the dojo:

```bash
hacker@dojo:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
hacker         1       0  0 05:34 ?        00:00:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7       1  0 05:34 ?        00:00:00 /bin/sleep 6h
hacker       102       1  1 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server --auth=none -
hacker       138     102 11 05:34 ?        00:00:07 /usr/lib/code-server/lib/node /usr/lib/code-server/out/node/entr
hacker       287     138  0 05:34 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       318     138  6 05:34 ?        00:00:03 /usr/lib/code-server/lib/node --dns-result-order=ipv4first /usr/
hacker       554     138  3 05:35 ?        00:00:00 /usr/lib/code-server/lib/node /usr/lib/code-server/lib/vscode/ou
hacker       571     554  0 05:35 pts/0    00:00:00 /usr/bin/bash --init-file /usr/lib/code-server/lib/vscode/out/vs
hacker       695     571  0 05:35 pts/0    00:00:00 ps -ef
hacker@dojo:~$
```

You can see here that there are processes running for the initialization of the challenge environment (docker-init), a timeout before the challenge is automatically terminated to preserve computing resources (sleep 6h to timeout after 6 hours), the VSCode environment (several code-server helper processes), the shell (bash), and my ps -ef command. It's basically the same thing with ps aux:

```bash
hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
```

There are many commonalities between ps -ef and ps aux: both display the user (USER column), the PID, the TTY, the start time of the process (STIME/START), the total utilized CPU time (TIME), and the command (CMD/COMMAND). ps -ef additionally outputs the Parent Process ID (PPID), which is the PID of the process that launched the one in question, while ps aux outputs the percentage of total system CPU and Memory that the process is utilizing. Plus, there's a bunch of other stuff we won't get into right now.

Anyways! Let's practice. In this level, I have once again renamed /challenge/run to a random filename, and this time made it so that you cannot ls the /challenge directory! But I also launched it, so you can find it in the running process list, figure out the filename, and relaunch it directly for the flag! Good luck!

NOTE: Both ps -ef and ps aux truncate the command listing to the width of your terminal (which is why the examples above line up so nicely on the right side of the screen. If you can't read the whole path to the process, you might need to enlarge your terminal (or redirect the output somewhere to avoid this truncating behavior)! Alternatively, you can pass the w option twice (e.g., ps -efww or ps auxww) to disable the truncation.

### Solve
**Flag:** `pwn.college{8sDxOHvt2ghPPTZbbYF9xn2L6V4.QX4MDO0wSN1gjNzEzW}`
 for this Challenge, i ran the ps command with argument -efww to get info regarding all running processes and found the /challenge/18039-run-20819. Finally i ran /challenge/18039-run-20819 to get the flag.

```bash 
hacker@processes~listing-processes:~$ ps -efww
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 12:51 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           8       1  0 12:51 ?        00:00:00 /run/dojo/bin/sleep 6h
root         133       1  0 12:51 ?        00:00:00 /challenge/18039-run-20819
root         136     133  0 12:51 ?        00:00:00 sleep 6h
hacker       138       0  0 12:51 pts/0    00:00:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/bin/bash /run/dojo/bin/ssh-entrypoint
hacker       151     138  0 12:51 pts/0    00:00:00 /run/dojo/bin/bash --login
hacker       162       1  0 12:51 ?        00:00:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/ttyd --port 7681 --interface 0.0.0.0 --writable -t disableLeaveAlert true /run/dojo/bin/bash --login
hacker       166     162  0 12:51 pts/1    00:00:00 /run/dojo/bin/bash --login
hacker       176     151  0 12:51 pts/0    00:00:00 ps -efww
hacker@processes~listing-processes:~$ /challenge/18039-run-20819
Yahaha, you found me! Here is your flag:
pwn.college{8sDxOHvt2ghPPTZbbYF9xn2L6V4.QX4MDO0wSN1gjNzEzW}
```

### New Learnings
I learned how ps command works to list all running processes in the linux environment using different options like -f,-e,-ef,aux.

### References

## Killing Processes
You've launched processes, you've viewed processes, now you will learn to terminate processes! In Linux, this is done using the aggressively-named kill command. With default options (which is all we'll cover in this level), kill will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist.

Let's say you had a pesky sleep process (sleep is a program that simply hangs out for the number of seconds specified on the commandline, in this case, 1337 seconds) that you launched in another terminal, like so:

hacker@dojo:~$ sleep 1337
How do we get rid of it? You use kill to terminate it by passing the process identifier (the PID from ps) as an argument, like so:

```bash
hacker@dojo:~$ ps -e | grep sleep
 342 pts/0    00:00:00 sleep
hacker@dojo:~$ kill 342
hacker@dojo:~$ ps -e | grep sleep
hacker@dojo:~$
```

Now, it's time to terminate your first process! In this challenge, /challenge/run will refuse to run while /challenge/dont_run is running! You must find the dont_run process and kill it. If you fail, pwn.college will disavow all knowledge of your mission. Good luck.

### Solve
**Flag:** `pwn.college{Iuv35NUVwLZyIQIPpVGWZ_sp7-1.QXyQDO0wSN1gjNzEzW}`
 for this Challenge, i ran ps command with aux argument to get all the running processes and found the PID of /challenge/dont_run.Then used the kill command with its PID.  Finally used the /challenge/run to get the flag.

```bash 
hacker@processes~killing-processes:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   1056   640 ?        Ss   14:43   0:00 /sbin/doc
root           7  0.0  0.0 231708  2560 ?        S    14:43   0:00 /run/dojo
root         135  0.0  0.0   5204  3200 ?        S    14:43   0:00 su -c /ch
hacker       136  0.0  0.0 231576  3520 ?        Ss   14:43   0:00 /challeng
hacker       137  0.0  0.0 231708  2560 ?        S    14:43   0:00 sleep 6h
hacker       139  0.0  0.0 231576  3520 pts/0    Ss   14:43   0:00 /nix/stor
hacker       145  0.0  0.0 231940  4160 pts/0    S+   14:43   0:00 /run/dojo
hacker       177  0.0  0.0 231576  3520 pts/2    Ss   14:43   0:00 /nix/stor
hacker       183  0.0  0.0 231940  4160 pts/2    S    14:43   0:00 /run/dojo
hacker       206  0.0  0.0 233600  3840 pts/2    R+   14:54   0:00 ps aux
hacker@processes~killing-processes:~$ kill 136
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{Iuv35NUVwLZyIQIPpVGWZ_sp7-1.QXyQDO0wSN1gjNzEzW}
```

### New Learnings
I learned how kill command can be used to terminate any process using its PID.

### References

## Interrupting Processes
You've learned how to kill other processes with the kill command, but sometimes you just want to get rid of the process that's clogging up your terminal! Luckily, terminals have a hotkey for this: Ctrl-C (e.g., holding down the Ctrl key and pressing C) sends an "interrupt" to whatever application is waiting on input from the terminal and, typically, this causes the application to cleanly exit.

Try it here! /challenge/run will refuse to give you the flag until you interrupt it. Good luck!

For the very interested, check out this article about terminals and "control codes" (such as Ctrl-C).

### Solve
**Flag:** `pwn.college{4X4BrsUdU36TWWuOGw79WQcuACd.QXzQDO0wSN1gjNzEzW}`
 for this Challenge, i ran /challenge/run then used Ctrl+C to interrupt its process to get the flag.

```bash 
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{4X4BrsUdU36TWWuOGw79WQcuACd.QXzQDO0wSN1gjNzEzW}
```

### New Learnings
I learned how Ctrl+C can be used to interrupt any process.

### References

## Killing Misbehaving Processes
Sometimes, misbehaving processes can interfere with your work. These processes might need to be killed...

In this challenge, there's a decoy process that's hogging a critical resource - a named pipe (FIFO) at /tmp/flag_fifo into which (like in the Practicing Piping FIFO challenge) /challenge/run wants to write your flag. You need to kill this process.

Your general workflow should be:

Check what processes are running.
Find /challenge/decoy in the list and figure out its process ID.
kill it.
Run /challenge/run to get the flag without being overwhelmed by decoys (you don't need to redirect its output; it'll write to the FIFO on its own).
Good luck!

NOTE: You might see a few decoy flags show up even after killing the decoy process. This happens because Linux pipes are buffered: conceptually, they have a sort of length through which data flows, and you might kill the decoy process while data is in the pipe. That data, having already entered the pipe, will proceed to the other end (your cat). If you wait a second, you'll see the decoys stop, and then you can /challenge/run and win!
### Solve
**Flag:** `pwn.college{85HcT-cHEN1hi1m_Yv9fFeQ6mA5.0FNzMDOxwSN1gjNzEzW}`
 for this Challenge, i ran ps command with -e and found the decoy process PID and then used kill command with that PID.Then ran /challenge/run with > with /tmp/flag_fifo. USing another terminal i catted the /tmp/flag_fifo to get the flag.

```bash 
hacker@processes~killing-misbehaving-processes:~$ ps -e
    PID TTY          TIME CMD
      1 ?        00:00:00 docker-init
      8 ?        00:00:00 /run/dojo/bin/s
    138 ?        00:00:00 .init
    139 ?        00:00:00 .init
    140 ?        00:00:00 su
    141 ?        00:00:00 sleep
    142 ?        00:00:00 sleep
    143 ?        00:00:00 decoy
    145 pts/0    00:00:00 ssh-entrypoint
    151 pts/0    00:00:00 bash
    169 ?        00:00:00 ttyd
    173 pts/1    00:00:00 bash
    183 pts/0    00:00:00 ps
hacker@processes~killing-misbehaving-processes:~$ kill 142
bash: kill: (142) - Operation not permitted
hacker@processes~killing-misbehaving-processes:~$ kill 143
hacker@processes~killing-misbehaving-processes:~$ /challenge/run > /tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo!
Bash will now try to open the FIFO for writing, to pass it as the stdout of
/challenge/run. Recall that operations on FIFOs will *block* until both the
read side and the write side is open, so /challenge/run will not actually be
launched until you start reading from the FIFO!
hacker@processes~killing-misbehaving-processes:~$ cat /tmp/flag_fifo
pwn.college{fVgUzeU3P7npE1L7SkZ4KLDYN13K8LqwK0BxpSf63c93MXR}
pwn.college{lcy4M5rmm39OXW2wEjyJSgUop6BsVbpehRDxEHioCssMJcJ}
pwn.college{a4xPcVnp-IWhedf1s.MAaUByTc3alnppUzzSdoe.kZXnwqs}
pwn.college{VTvzyMaYiDgRuqLQgeqyXG3KaEAbCWaoMIE1wF9oJx4It.B}
pwn.college{kv31PHEOlPGk9nd1uUGdZqJiRTnFqwY4qrG8-kgLRQ8FjZp}
pwn.college{OSfVK.31zCeV8wXi.ju-MeSJrzoRLo8ksxSYCzRXt3nhJi2}
pwn.college{G2hvOoISNPDiBJVEMWqOhz8KYkkbr2N7JUTi.6iqoKCAz68}
pwn.college{JOrXP0K5WafdLc92KTnWXf35eUgpz-7lSMbD7jjevg7qwuc}
pwn.college{j67zTjwFYEM7AlX2a78uC8KAU.OxV-Y5hhMO3l4UIwFf0uX}
pwn.college{gyQI44H3sNiE44bZ0mz7pCT.OvGB4NkVs3nbCPo2QomIBcP}
pwn.college{J-Oq6Dwe2W5wRC8.etuKlfE2W-Qyu-AzhoZDVfEigaECXi4}
pwn.college{fZbvyVvYiqCqBEDiyQVkYUYzog-4cMvIFaqigtSTMdf9U-U}
pwn.college{C22MXKgfR8wo402eoV0UUwtS9aUNYA38g-pd-8rtTNc7YNU}
pwn.college{1S8kRTOeTrqdR4UIV.26C-vSEJ7VJV-.6SUHUfBLMygJ-O9}
pwn.college{kmvAuLGRoUu6q5eErcOOL8A5YcsHAa6cxCmIad65ZSwDW51}
pwn.college{fxHMFtMmSYq4E5jfnBJnVtfRhUEjmr15ensyMY2RAhQ3Xfx}
pwn.college{Mu1eJB8mENTicotrHOXCqlZiFtDPiitIH5Bj-Rlq5nhMxLi}
pwn.college{E5cmF7yyZYMJCnW7BbBrLkdDh8cl8GRB7mr9jBRlWZ7bYj8}
pwn.college{0otnc4Vjqrwh.ZVdPl8MntYqOZ0NswZghqk9DY0beIHgCjh}
pwn.college{gQAVVVoRRBvaxIniWXRwDwcf1UkWrIWcItWhmIQ7FsfpVyA}
pwn.college{oZkxvr38X8YKmViKZ55TqytgTYcQ5M5m8CrH3HhxcFq-Bf7}
pwn.college{49zr3Fd5EJrNxjNy9poGYKZQO8TtHMF.6Q3CdvNq7nchNed}
pwn.college{qMmsyylrRaaXpkXE59GGgJcZ9lnSTsfe6KmiD-jSFkvmnoW}
pwn.college{WLthQPifZnaX4wcfUyNKJbqiugDcjPLpNWTCQvzTRQndsiz}
pwn.college{9fs0UtojmHvoWjwz1TPaeUEgM03PG.sLQUfmD1sYHjQmD6v}
pwn.college{bJSFyLotV6pHrFSaGEsTyHI5fFSbY.t.MVANJVEuD8PPDB9}
pwn.college{W55FwJlbU9X6pwaZ-vc.0qUHFMZVIKt5mfbOkRDTvvN93jr}
pwn.college{5nK9jQElUUOTW4-LSjev.ZKSgzG545qhKAQobVoeRkC-uHr}
pwn.college{NjLyP-bFpJo9c9pRXmqdGbaFEuIxWZ-GcN.WX3cWe7RqbHK}
pwn.college{Q1D374KGFgNrDG29Clk2x-fEPYj0S95qmoDz1cnKWnULl-o}
pwn.college{zf.SEsOYydK35JiZoYmlDhsIoVuEr8kUY9x3jsuzWIhR8Eq}
pwn.college{toQOQkjWfR9movSVzBP1.E5dUANYom8mAy-Sv9NVLT-CoF-}
pwn.college{njAHAYXV2BCsBe0zQfw3LZ8Wq02sIS.hJWWHhOxboePCUop}
pwn.college{oEVMBImC4mKLVWSxvrmZugZrtZq5CT232YvMRZrEsSdiCqF}
pwn.college{Y8G7INB3W9nJdFmN51Ji40C62iQ1Zra4-OioYjOQ7tgc5pZ}
pwn.college{uCuvCJ0oRz08izQ3s-KiRBdjJX04YoDH0kGmiF2h6M7jAGS}
pwn.college{SHach5cHneCjth9TFZNFknR5sJ1wmIaDDdKC3M0srvUDBAu}
pwn.college{C4q0kBe3cihXGiplVTwWrAAPlM04bJBkc9niwThN2Z6uGoc}
pwn.college{1heOK2wm8AGGvzHm.xcQuCU94mSaK3t02Q0gHUNQ7OHMm.G}
pwn.college{-CW37sURMZiRCG8kGjOiS9jPBX3jWRzak8UCkNDdifSsB5Q}
pwn.college{TwpOVD5NbL3BDYNM-O1fvVt8jawYHz7YEPJLvuOmi4UXfrQ}
pwn.college{iIpaOVOjdyqo3y8OX6TNsHCh-5wAghE5xJ2nL7yF2vSM9gd}
pwn.college{It-MEiGctOVvh-PTMR1qBE.k5-4KEJKp9idfUPP8G1ytZhp}
pwn.college{bAfg1ZPpwchbXmBj3j18p9RRMTK0lx4CLqQ5x2fcxEU0blP}
pwn.college{5W-UNYg-Zvkj1yA2lPThoNS3Mw1p1hrIdZn9ajprHbe8uyM}
pwn.college{Y-M9Pl2PaBFwORWstZyaofFGmHMmnOxaEura5lfMJTt69xF}
pwn.college{VZtiVhBWQqPFiKTJMCtjb7PonR67fLKaSKtda6O29l0mV3Z}
pwn.college{Xd4o9gAW7N6DI1aVD4UufnemoR2UIxsgo-Z0f5GP.hHMa9S}
pwn.college{EV-8eSWYh33R6VsfQkmTGZLt8vg9HwVN1ujS4FjeJfA0uaK}
pwn.college{V7GU4bRQBQxCCfL9vQix95skf8ooNfQafJnTTMEzU9RgevF}
pwn.college{iSwUbk-kDTtKqFGev2REHVgWoRbl2.DsuUa1MG2VXgRCctr}
pwn.college{S1jb70sKO.HEIKhd9oSLbXwkd-8hXp8Qd6QiplHRuCCo8zD}
pwn.college{h3XWYzro-7gQSPfc2HOPwPodJdes35psRv0xmSjPKCEsftB}
pwn.college{b4dyNJi5NEwQxIdy5ONkBt7ukQmWJGnnnJJImh7tb4og22J}
pwn.college{Qp5difeDMYpGtr1Ax1Re9Svvft-nCA1aAQe66jaToTlzguQ}
pwn.college{7DkKVtsPp9mZ0e4CDf-UKOYNJi.WipAV2T49GwWzSKJqiOd}
pwn.college{GXO5m6fUSsdbzZp7JmvDI9tWF79.K7zaxaNsl-snmDH31k9}
pwn.college{10WvcSf0MWNu4Rycl0fn9L4JyFWD6lZvjHi.389pciAc5Tr}
pwn.college{WuLZXqvZz5vRI4ThDp7vaUE.sSfTlHYyipc-rst-j007KCo}
pwn.college{F3qFmcL2-oiE2Hs-EXb165TGg6.71GZs8NQS8yWeHi30yF-}
pwn.college{-o4kzBGeThkc4J3vD8NrRUelJep4m9Vsf3kjgNYLyFZOg9r}
pwn.college{DuTPp0IdnYWhs-gV0TVp7amRrO-cf0qk2RpcyxHEIuIQNFW}
pwn.college{Q6X2pA067BRfo02.KgniaPb0w9zlyHQa-LEOnNTyS3eRS3e}
pwn.college{8-Vf3tjZYWda3CpJrZongxmrFb8KDZQQqY5wm.8qXJ8YJJa}
pwn.college{.LsBQ0WbCk-FFW5xEcfgjEVjQ1.SGknerGzdwNm2ZY22NTq}
pwn.college{SpnUx-aOIk601UgkItvKhyWB3sQfalqN4-AB3gm3wyc0ctj}
pwn.college{uFKjNHWIKX-tFN4jGQjeb1l0FJLhx2UpfF5bQ5VggmZsD7p}
pwn.college{NAyb3vmTuFkjR5mOKtSmKzHBu6xup-2rWu4t-i6MRrXygXl}
pwn.college{hS3bj7u1FNINVcbnOxBGpi9nTD2T5L2m7mad8S1t.zV6iG5}
pwn.college{LVpjslGN8Iq4E-MFYZT-pHO52sGGd8NowWd.hRInOnHtA9z}
pwn.college{nk2BIhZ1b185xSMj1v-0FOkYWt71vLQlAoldmb9nmk1r8kB}
pwn.college{oa57792Kqb7FIoXhD2Wf7JmRIoSj6tPDmil8.YXxtmfwmj9}
pwn.college{aOCDnJRPBo1aFSLQzm4b7b-64cmoqpdqKbUytsk9TYMx086}
pwn.college{S3O1xlvUCV7e-YFKANDv2Xd2rQTzlRl0O1riuTbkAacudPW}
pwn.college{AhMVnkkHxFy84CDID4giVcYaBytPBPF.1TxkM9kM6KCRG0.}
pwn.college{C-FC-CRP.viONX3sMTytIb6vuzVTiy3k00L6AID5yK0WfA2}
pwn.college{eJb3oietDkL4PsR-eKYXTGbY6uLVATI1y9Ki5l4NSKNHcOs}
pwn.college{Wws6uRZll3MFkONn7aTRZ.YuVC3e.czt5fIUv7dwIF0mHo1}
pwn.college{Tmce-bawKhbrFvKCyHNQTvQpMrVvurRH87uZMbHD6YN9Xrg}
pwn.college{p2fYyfR-JXZ5QX-M7DnZg8RLeCHOLrlw0y1LSrsbl4cLUhH}
pwn.college{V-1lyTnE7zMSwUn.7MpxX6kzB67pQltFLMDO9r9Ud-Acl.V}
pwn.college{UW6JgGdtqvBYBk-ZGic38GlMKEta-qxDv-QoCPvOwVnonqz}
pwn.college{0rgOXkZTPdrgQbQXy7xZSse.GQVxMfGPJupOwaOadgMHjky}
pwn.college{-AOXFqsfN.eDtRhPPDYSNE1o4Eb0BROQ3Rpb4fGqyy1Kxz9}
pwn.college{HKKvfnmBQq5ykGKVupNYLskIbhSJdRJ1FxeafPBBf2G4MFt}
pwn.college{mocRBWUAhw48RSBSn2SoJjyvyT08NCtqukUcVwHFfP--2cR}
pwn.college{ELqIOPVKOCmv-BWQRv45cnLaEY4poudDeZ3LAwJRalikivH}
pwn.college{rTIby9gzLOCYND5sgCXjegaEKBl5-g5ESePn2ud4k20-3jm}
pwn.college{aqT2I3p8WMT1IEfXqrBvCBdWsDEIf.QjtoK5o72gOvhXa-Y}
pwn.college{cWw3DevxwMnwwcNf8VSBB-K9Ej.J8cZctWSHjteec7o0AZl}
pwn.college{54F1ioAJ0iQuJq6hLgu-R.Fd7kxkT9ZGfC.ZYpokfOTdfLt}
pwn.college{A0Kq9qrXhCNFBKHepbmFFnj6SkdsKkBzQMZl78lMD.zJnyy}
pwn.college{mcxz3JIOcf0Yv3qNm3T4NFp0QPt51p9Jc8qw94TJ4ZyKP9P}
pwn.college{Ela9M.sG929tLVY.QeQE.voM0r3YxZKSBXBOQRWwDmR7mIG}
pwn.college{BcmNqBHLA9U6gvYxr6UTmKOXb-cPuSYzX0Bm1KMq3tZMO-k}
pwn.college{PzmRnksUTPfdSxeHHtEz5OzgJtn351CJkZ7FC68-24tSd1Q}
pwn.college{G..VTTuLk4x3c5PZw4axtOYjE-Yv7BwfFN6tJbTHwRwDI2f}
pwn.college{Fxq9V2sTqTqMKG5KER-GNOd8sHwcStcP8IVp.YcUmwTu2PO}
pwn.college{B2QW2FWp.SvabJIH10nHF8dyRYNBhogWAxhHORPgs7Xk.Uh}
pwn.college{0s5vkftD358Q8um8PR1ByulVyjBvrdsMa96YY5C5r12XknS}
pwn.college{.Lxi9IO0A8RUMnEgo9sx8-nXTgO8V5bhSdRAcOIg5v0B63Q}
pwn.college{UeZ53Kb3hRlaHEnjrgpRcMDHiuSLkGuM97lPDsgdUtr8vux}
pwn.college{jSfh-3wJi8sqNpGFkNNDxxockv.l0sGRQDfJLJlg.PNj8xM}
pwn.college{rSAtJJuQX73I3F9crd-vbKOAXXZHvN.ssXBSg04jgDxfuWx}
pwn.college{YhmZ3bv8qH6zucLi3w5QlSx8EldLVW-8fESBmJN3dSeh04x}
pwn.college{Ei29rVBAiyvUF4huXvcNSDhcU8p5qJzKYjoT6bYKi9f5Ph5}
pwn.college{KKrPBBzfSjR.awe-PKEnyV9fwk0PmNmEjgYSJ7tNCwCY19E}
pwn.college{lYvJp.QPG3d5lkb5M8UDA-cClD3x0U4Bo1h-gFF1l-36HTr}
pwn.college{xUiiCWiaLHVigW8I3eQXWNHvclKI6IHo2atGB-A9qYYYeD5}
pwn.college{WZSwSipw7SVjXWe99iyaxoN0bLMWgmDP7d5UL1EdN2I7cIl}
pwn.college{CyvWm1-0GESOqZMBZ74l7L-MAZ5UOZ4LsbMiy0HUjR9aAax}
pwn.college{vgeECLYw3XHY3eo4uOKhO9MkELIhqX6ZhcT2Wn4NPmsH3Zd}
pwn.college{HYnP5wm7pnxdGu4bk3a1fniCDQzGw3uXZ6LyH0Ydeqz2aK8}
pwn.college{gsLUGSCwx0GoWmtX2FarDFzDYLBB4CMNv3zuxYGbtsS6N8m}
pwn.college{0WttH57vBqD.6-KOLFp5CawgrxvRLDBWpes9k7PsAQgyFrJ}
pwn.college{pDpTWoGU.4kTgnO6v62jBCxsAmIv.cKBr.z8nHUKz-SD.a5}
pwn.college{xguDF8oocqd2zkLQ4nYKaF9iGVWQ8wQe10hA34kwr3iV99C}
pwn.college{khGVg0BpVTtIPmNAV1pZORVyq6wKAeFH3tj.qtZiagicnb1}
pwn.college{Ql8ow34qbxqrnPX1OhbgyKiNXpAoAwXsAmes6thzkN7U7hL}
pwn.college{ix.8i3wJkI-jNhUiiRe.Tt2CQgVbHWQ7ZX4lQSC.i4E7vzd}
pwn.college{pdRInC-fL43m77uNEefvfhEIfAT7tw.TOw5QDwW9ZntOMUV}
pwn.college{SftwBAA.gS.3jI-KN0QKPXAQ0t1hvBr9PXaATkfvZI-s3Wj}
pwn.college{.a5aFsPIiFgLngwGKu2x3YpQYC41MjnPbCrXsWNFT97nT6f}
pwn.college{S4yYDKo6GcEmzszEHOOEP0n19SlAvaPxQaObUOv0XjGlC5O}
pwn.college{M.G-qHD2XF97i0.N.5aszrZaYgeBaxQCvVJwBExS7BNHv1r}
pwn.college{Iv4mTl8ZVDH8R2dVkAl01yk-3XSW.rwFXwopj7G-linWpnN}
pwn.college{XMyt0ETGtumdJdSbRUjpIfX6Y-GeCTrrwbSxZjnWXW6lBdb}
pwn.college{EN0Chqec2-3cktaUllkNn6yICWqLQEXcoM7gGvY.y5fOB-Y}
pwn.college{kvw3dg8dC.6QR708J0LHobmkZ.Y24yL4MULmS5K2Vv4SABH}
pwn.college{QtnA0fYQNHGfJZ4m4uyUwzAPW7c00BHJVa0BzOMcHRvx37C}
pwn.college{PdC4.6kMilpTZP9n883aS1mDDDbYkobSAXrhyOZ4SvLBXGF}
pwn.college{sTXCSaZz0OP7bSDcQM22xKLG5vfU90mO66kOtmwgLBL6w.d}
pwn.college{pEt3-XYynh.0bworHPVD-wato5TG3CA-1hGjZiRKEnP-n6M}
pwn.college{bYBMAtazoE38jfM2OzSlCR9JjdT-XhfN.mj.fSodLyvfPPT}
Sending the flag to /tmp/flag_fifo!
pwn.college{85HcT-cHEN1hi1m_Yv9fFeQ6mA5.0FNzMDOxwSN1gjNzEzW}
```

### New Learnings
I learned how to kill any clogging process can be used to interrupt any process.

### References

