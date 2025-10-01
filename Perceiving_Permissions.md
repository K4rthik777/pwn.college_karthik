# Perceiving Permissions

## Changing File Ownership
First things first: file ownership. Every file in Linux is owned by a user on the system. Most often, in your day-to-day life, that user is the user you log in as every day.

On a shared system (such as in a computer lab), there might be many people with different user accounts, all with their own files in their own home directories. But even on a non-shared system (such as your personal PC), Linux still has many "service" user accounts for different tasks.

The two most important user accounts are:

Your user account! On pwn.college, this is the hacker user, regardless of what your username is.
root. This is the administrative account and, in most security situations, the ultimate prize. If you take over the root user, you've almost certainly achieved your hacking objective!
So what? Well, it turns out that the way that we prevent you from just doing cat /flag is by having /flag owned by the root user, configure its permissions so that no other user can read it (you will learn how to do that later), and configure the actual challenge to run as the root user (you will learn how to do this later as well). The result is that when you do cat /flag, you get:

```bash
hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```

Here, you can see that the flag is owned by the root user (the first root in that line) and the root group (the second root in that line). When we try to read it as the hacker user, we are denied. However, if we were root (a hacker's dream!), we would have no problem reading this file:

```bash
root@dojo:~# cat /flag
pwn.college{demo_flag}
root@dojo:~#
```

Interestingly, we can change the ownership of files! This is done via the chown (change owner) command:

chown [username] [file]
Typically, chown can only be invoked by the root user. Let's pretend that we're root again (that never gets old!), and watch a typical use of chown:

```bash
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chown hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 hacker root    0 May 22 13:42 college_file
drwxr-xr-x 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
```

college_file's owner has been changed to the hacker user, and now hacker can do with it whatever root had been able to do with it! If this was the /flag file, that means that the hacker user would be able to read it!

In this level, we will practice changing the owner of the /flag file to the hacker user, and then read the flag. For this challenge only, I made it so that you can use chown to your heart's content as the hacker user (again, typically, this requires you to be root). Use this power wisely and chown away!

### Solve
**Flag:** `pwn.college{MF6BxHBjX0zcLdO_k761iaq1Uuq.QXxEjN0wSN1gjNzEzW}`
 for this Challenge, i ran chown command with username that is to be given the ownership with the filename as arguments in the privileged terminal.Then catted the /flag as the user to get the flag.

```bash 
hacker@permissions~changing-file-ownership:~$ ls -l /flag
-r-------- 1 root root 60 Oct  1 11:01 /flag
hacker@permissions~changing-file-ownership:~$ chown hacker /flag
hacker@permissions~changing-file-ownership:~$ ls -l /flag
-r-------- 1 hacker root 60 Oct  1 11:01 /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{MF6BxHBjX0zcLdO_k761iaq1Uuq.QXxEjN0wSN1gjNzEzW}
```

### New Learnings
I learned how chown command works to change the ownership of any only-root accessable file to a particular user.

### References

## Groups and Files
Sharing is caring, and sharing is built into Linux's design. Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.

You can check what groups you are part of with the id command:

```bash
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$
```

Here, the hacker user is only in the hacker group. The most common use-case for groups is to control access to different system resources. For example, "Practice Mode" in pwn.college grants you root access to allow better debugging and so on. This is handled by giving you an extra group when you launch in practice mode:

```bash
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker),27(sudo)
hacker@dojo:~$
```
A typical main user of a typical Linux desktop has a lot of groups. For example, this is Zardus' desktop:

```bash
zardus@yourcomputer:~$ id
uid=1000(zardus) gid=1000(zardus) groups=1000(zardus),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),106(netdev),114(bluetooth),117(lpadmin),120(scanner),995(docker)
zardus@yourcomputer:~$
```
All these groups give Zardus the ability to read CDs and floppy disks (who does that anymore?), administer the system, play music, draw to the video monitor, use bluetooth, and so on. Often, this access control happens via group ownership on the filesystem! For example, graphical output can be done via the special /dev/fb0 file:

```bash
zardus@yourcomputer:~$ ls -l /dev/fb0
crw-rw---- 1 root video 29, 0 Jun 30 23:42 /dev/fb0
zardus@yourcomputer:~$
```

This file is a special device file (type c means it is a "character device"), and interacting with it results in changes to the display output (rather than changes to disk storage, as for a normal file!). Zardus' user account on his machine can interact with it because the file has a group ownership of video, and Zardus is a member of the video group.

No such luck for the /flag file in the dojo, though! Consider the following:

```bash
hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```

Here, the flag file is owned by the root user and the root group, and the hacker user is neither the root user nor a member of the root group, so the file cannot be accessed. Luckily, group ownership can be changed with the chgrp (change group) command! Unless you have write access to the file and membership in the new group, this typically requires root access, so let's check it out as root:

```bash
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chgrp hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 root root   4096 May 22 13:42 pwn_directory
root@dojo:~#
```

In this level, I have made the flag readable by whatever group owns it, but this group is currently root. Luckily, I have also made it possible for you to invoke chgrp as the hacker user! Change the group ownership of the flag file, and read the flag!

### Solve
**Flag:** `pwn.college{EhUwtHYhJQwrhreZ5KTRoJHGam7.QXxcjM1wSN1gjNzEzW}`
 for this Challenge, i ran ls -l command to check the info about files and directories.Then i ran chgrp command with group name that is to be given the ownership of group with the filename/group name as arguments in the unprivileged terminal.Then catted the /flag as the user to get the flag.

```bash 
hacker@permissions~groups-and-files:~$ ls -l
total 28
-rw-r--r-- 1 hacker hacker   4 Sep 25 15:36  COLLEGE
-rw-r--r-- 1 hacker hacker   8 Sep 26 14:17  PWN
-rw-r--r-- 1 hacker hacker 829 Sep 26 14:00  instructions
-rw-r--r-- 1 hacker hacker  95 Sep 26 14:00  myflag
lrwxrwxrwx 1 hacker hacker   5 Sep 23 15:02  not-the-flag -> /flag
-rw-r--r-- 1 root   hacker   0 Sep 27 16:03  output_pwn
-rw-r--r-- 1 root   hacker   0 Sep 27 15:55  pwn
-rw-r--r-- 1 root   hacker  77 Sep 27 16:10  pwn_output
-rw-r--r-- 1 hacker hacker   0 Sep 26 14:00  the-flag
-rw-r--r-- 1 root   hacker  60 Sep 21 09:01 '~'
hacker@permissions~groups-and-files:~$ chgrp hacker not-the-flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{EhUwtHYhJQwrhreZ5KTRoJHGam7.QXxcjM1wSN1gjNzEzW}
```

### New Learnings
I learned how chgrp command works to change the ownership of any group to a particular user.

### References

## Fun with Group Names
In the previous levels, you may have noticed that your hacker user is a member of the hacker group, and that zardus is a member of the zardus group. There is a convention in Linux that every user has their own group, but this does not have to be the case. For example, many computer labs will put all of their users into a single, shared users group.

The point is, you've used hacker for the group before, but in this level, that is not going to work. I'll still allow you to use chgrp, but I have randomized the name of the group that your user is in. You will need to use the id command to figure that name out, then chgrp to victory!

### Solve
**Flag:** `pwn.college{g_iRNC8ysy9ApTBdDDxLPpJOSVP.QXycjM1wSN1gjNzEzW}`
 for this Challenge, i ran ls -l command to check the info about files and directories.Then i used id command with hacker as argument.Then i ran chgrp command with group id with the not-the-flag as arguments in the unprivileged terminal.Then catted the /flag as the user to get the flag.

```bash 
hacker@permissions~fun-with-groups-names:~$ ls -l
total 28
-rw-r--r-- 1 hacker grp15908   4 Sep 25 15:36  COLLEGE
-rw-r--r-- 1 hacker grp15908   8 Sep 26 14:17  PWN
-rw-r--r-- 1 hacker grp15908 829 Sep 26 14:00  instructions
-rw-r--r-- 1 hacker grp15908  95 Sep 26 14:00  myflag
lrwxrwxrwx 1 hacker grp15908   5 Sep 23 15:02  not-the-flag -> /flag
-rw-r--r-- 1 root   grp15908   0 Sep 27 16:03  output_pwn
-rw-r--r-- 1 root   grp15908   0 Sep 27 15:55  pwn
-rw-r--r-- 1 root   grp15908  77 Sep 27 16:10  pwn_output
-rw-r--r-- 1 hacker grp15908   0 Sep 26 14:00  the-flag
-rw-r--r-- 1 root   grp15908  60 Sep 21 09:01 '~'
hacker@permissions~fun-with-groups-names:~$ id hacker
uid=1000(hacker) gid=1000(grp15908) groups=1000(grp15908)
hacker@permissions~fun-with-groups-names:~$ chgrp 1000 not-the-flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{g_iRNC8ysy9ApTBdDDxLPpJOSVP.QXycjM1wSN1gjNzEzW}
```

### New Learnings
I learned how chgrp command works to change the group of a file.

### References

