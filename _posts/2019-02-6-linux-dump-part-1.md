---
layout: post
title: "All My Linux: Part 1"
date: 2019-02-06 18:00:00 +0300
tags: linux
---

<span class="dropcaps">T</span>here was an attempt (by me) to 'know linux'...

### Contents
* [Printing](#printing), [printing gotchas](#gotchas), [printing errors](#errors-you-might-encounter-while-printing)
* [Remote Access](#remote-access), [ssh Errors](#ssh-errors)
* [Desktop Environments](#desktop-environments), [DE, DM, WM?](#desktop-environments-display-mangers-window-managers)
* [Specific things](#little-things): [disabling users list on ubuntu login screen](#disabling-user-list-at-ubuntu-login-screen), [running apps from terminal in background](#running-gedit-in-the-background-from-terminal), [make ubuntu say stuff](#make-ubuntu-say-things), [check linux distro](#check-linux-distro), [get IP and hostname](#get-ip-address-and-hostname), [open notepad++ from cli](#open-a-file-in-notepad-using-cmd), [copy files to ftp server(windows)](#copy-files-to-ftp-server-in-windows), [VSCode Code Snippets](#VSCode code snippets)
* [Commands dump](#commands)
* [Trouble shooting](#troubleshooting), [OpenSUSE](#opensuse), [Booting to virtual terminal](booting-to-virtual-terminal)
* [References](#references)

<!-- region printing -->
### Printing

The recommended way to print in ubuntu is to use CUPS (Common Unix Printing System) as opposed to the (old) BSD printing system.
You can read more about printing systems [here](https://www.linuxjournal.com/article/6729)

First you need to install CUPS

{% highlight bash %}
sudo apt install cups
{% endhighlight %}

The (old) BSD system uses `lp` and `lpr` commands to print. Cups has its own mappings of these same commands and it is therefore favorable to use them. You need to install them first:

{% highlight bash %}
sudo apt install cups-bsd
{% endhighlight %}

You can now print stuff
{% highlight bash %}
# print file with default settings (default printer, queue etc)
lp file

# print to specific printer/queue
lp file -d <printer-name>/<queue>

# using lpr
lpr file

# specifics
lpr file -P <printer-name>/<queue>
{% endhighlight %}

<!-- TODO: difference between lp and lpr -->
#### Gotchas
* `lp` and `lpr` can only print PDF, ps (PostSript) and plain text files

* It is not possible to use `lp` or `lpr` to print to a printer directly using its IP

* Also, if you don't know what your printer name is, you can find this and more printing commands at the [commands section](#printing-commands) of this page.

* I don't know difference between `lp` and `lpr` for now...

* Here's also some stuff I ended up installing while trying to get printing to work:
{% highlight bash %}
sudo apt install cups-filters libstdc++5:i386
{% endhighlight %}

#### errors you might encounter while printing:
###### not printing
{% highlight bash %}
# clear /var/spool/cups
rm -rf /var/spool/cups/*
{% endhighlight %}

###### `lp` and `lpr` not working
{% highlight bash %}
# install cups-bsd "This package provides the BSD commands for interacting with CUPS: 
# /usr/bin/lpqa /usr/bin/lpr /usr/bin/lprm /usr/sbin/lpc"
sudo apt install cups-bsd
{% endhighlight %}

##### none of these have solved my problems
Check CUPS logs (if you have CUPS installed) which can be found here: 
`found in /var/log/cups/error_log`

Look [here](https://wiki.ubuntu.com/DebuggingPrintingProblems) (official ubuntu page on debugging printing problems)
<!-- endregion printing -->

<!-- region remote-access -->
### Remote Access

#### using ssh (passwordless ssh login)
{% highlight bash %}
# solution 1: one-liner
sshpass -p 'password' ssh user@host
{% endhighlight %}

{% highlight bash %}
# solution 2: safer
# 1 create ~/.ssh on target PC if it does not exist
ssh user@host mkdir -p .ssh # enter password

# 2 exit and generate private/public key pair on your pc
ssh-keygen -t rsa

# 3 copy your generated public key to the authorized_keys file in .ssh folder of host
cat .ssh/public_key.pub | ssh user@host 'cat >> .ssh/authorized_keys'

# 4 set permissions on host .ssh folder and authorized_keys file
# this is important, otherwise ssh will always require a password
# from SO: "~, ~/.ssh and ~/.ssh/authorized_keys must be writable only by you (700 - 755)
# "your ~/.ssh/authorized_keys must be readable (at least 400) but writeable (600)
# if you'll need to add more keys to it
ssh user@host "chmod 700 .ssh; chmod 640 .ssh/authorized_keys"

# 2.5 OR, after generating the key in step 2, just do this which will do step 3 and 4 for you
ssh-copy-id user@host # enter password

# 2.5 OR if your server uses custom port no:
ssh-copy-id "user@host -p 1234"
{% endhighlight %}
..aand you're done, you can now login to the remote without having to input password with:
ssh user@host

#### ssh errors
-Attempting to ssh into windows:

`"Unable to negotiate with <IP> port 22: no matching cipher found. Their offer: aes128-cbc,3des-cbc,aes192-cbc,aes256-cbc"`

-FIX:
check which ciphers your client supports: 

`ssh -Q cipher`

if any of the ciphers are also supported by the server (Their offer: ...), then you can force the use of those specific ciphers:

`ssh -c aes256-cbc usr@host`
<!-- endregion remote-access -->

<!-- region desktop-environments -->
### Desktop environments
Stumbled on these when trying to figure out how to speed up a slow machine.
Here's my general assessment of popular linux DEs based on a quick read:
##### KDE
- Robust and highly customizable
- Heavy and clunky
- OpenSUSE, Kubuntu

##### Gnome (3)
- Modern, Graphically heavy
- Mother of Cinammon, Unity
- Debian, Fedora, Ubuntu Gnome
- Gnome 2, though deprecated is much more lightweight

##### MATE
- Based on Gnome 2
- Built to be lightweight
- Kind on memory
- Highly customizable
- Ubuntu MATE

##### The rest
Cinammon (linux Mint), LXDE (Lubuntu, lightweight), Xfce (Xubuntu, Manjaro, lightweight), Pantheon (Elementary OS, beautiful)

##### lightdm/gdm
-LightDM is an x display manager that aims to be lightweight, fast, extensible and multi-desktop
-gdm (the GNOME Display Manager) is a display manager (a graphical login program) for the windowing systems X11 and Wayland.It is a highly configurable reimplementation of xdm, the X Display Manager

#### Desktop Environments, Display Mangers, Window Managers?
from [StackOverflow](https://unix.stackexchange.com/questions/20385/windows-managers-vs-login-managers-vs-display-managers-vs-desktop-environment?rq=1):

* Xorg, XFree86 and X11 are display servers. This creates the graphical environment.
[gkx]dm (and others) are display managers. A login manager is a synonym. This is the first X program run by the system if the system (not the user) is starting X and allows you to log on to the local system, or network systems.
* A window manager controls the placement and decoration of windows. That is, the window border and controls are the decoration. Some of these are stand alone (WindowMaker, sawfish, fvwm, etc). Some depend on an accompanying desktop environment.
* A desktop environment such as XFCE, KDE, GNOME, etc. are suites of applications designed to integrate well with each other to provide a consistent experience.

- In theory (and mostly so in practice) any of those components are interchangeable. You can run kmail using GNOME with WindowMaker on Xorg.


<!-- endregion desktop-environments -->

<!-- region little-things -->
### Little things
##### Disabling user list at ubuntu login screen
_one liner:_

{% highlight bash %}
sed -i 's@# \[org\/gnome\/login-screen\]@[org/gnome/login-screen]@' /etc/gdm3/greeter.dconf-defaults && sed -i 's@# disable-user-list=true@disable-user-list=true@' /etc/gdm3/greeter.dconf-defaults; init 6
{% endhighlight %}

_manually:_

edit ```/etc/gdm3/greeter.dconf-defaults``` and uncomment the following lines:

{% highlight bash %}
disable-user-list=true

[org/gnome/login-screen]
{% endhighlight %}
Then restart

##### Running gedit in the background from terminal
`gedit &`\\
OR\\
`setsid gedit # runs a program in a new session`

##### Make Ubuntu say things
`sudo apt install gnustep-gui-runtime`
`say "You can't handle the truth"`

##### Check linux distro
`python -mplatform | grep -iw KEYWORD # KEYWORD could be 'ubuntu' or 'opensuse' etc` 

##### Get IP address and hostname
{% highlight bash %}
  hostname # prints hostname

  hostname -I # prints IP address

  # if the above (for IP) doesn't work e.g. in OpenSUSE, try this:
  ifconfig -a | grep -iw inet | grep -v '127.0.0.1' | awk '{ print $2}' | cut -f2- -d:

  # let's deconstruct that...

  ifconfig -a # gives a whole bunch of info related to currently connected network devices

  # '|' pipes (sends) the output of ifconfig -a to the next command:
  grep -iw inet 
  # returns every line that has 'inet' in it. 
  # -i = case-insensitive match (openSUSE gives its result in all caps, ubuntu does not)
  # -w = exact word match (otherwise grep matches things like inet6 or inetBLA which lie outside our interest)

  # the resulting lines get piped to:
  grep -v '127.0.0.1' 
  # grep -v is a reverse match i.e "return all lines that DO NOT have this"
  # '127.0.0.1' is... I forgot what's special about it, but we don't want it (TODO)

  # i forgot what the awk does also... (TODO)
  # ok so after the awk command, the result looks something like this:

  addr: X.X.X.X

  # so we want to remove the 'addr: ' part which is why we pipe that result to cut:
  cut -f2- -d:
  # read about the cut in the commands section below, but this cut splits its input into 2 fields
  # using a colon ':' as the delimiter and returns the second field (the part after the colon, which is the actual IP):
  X.X.X.X
{% endhighlight %}

##### Open a file in notepad++ using cmd
`start notepad++ <filename>`

##### Copy files to ftp server in windows
-you can map a network location to a local drive in windows by going to THIS PC > Map network drive
-this would allow you to upload files to an ftp server if you map one. (why? because browsers have limited ftp support and can only download but not upload; other than browsers you'd need a 3rd party ftp client to upload to an ftp server)

##### VSCode code snippets:
{% highlight json %}
  {
    "For_Loop": {
      "prefix": "for",
      "body": [
        "for (const ${2:element} of ${1:array}) {",
        "\t$0",
        "}"
      ],
    "description": "For Loop"
  }
}
{% endhighlight %}
KEY:

-`${1-based_index_of_traversal:initial_default}` - placeholders (tab stops)

-`$0` - final tab stop

-`\t` - insert tab

-each element of "body" is a line

-You can also use this [snippet generator app](https://snippet-generator.app)

<!-- endregion little-things -->

<!-- region specific-cmds -->
## Commands
### Packages Commands
{% highlight bash %}
# remove packages (and uneeded dependencies):
sudo apt-get remove --auto-remove package-name

# list all packages manually (intentionally) installed:
(zcat $(ls -tr /var/log/apt/history.log*.gz); cat /var/log/apt/history.log) 2>/dev/null |
  egrep '^(Start-Date:|Commandline:)' |
  grep -v aptdaemon |
  egrep '^Commandline:'

# search package
apt-cache search keyword
# or
apt search keyword
# (TODO: difference?)
{% endhighlight %}


### Printing Commands
{% highlight bash %}
# print
lp file [-d <printer-alias>/<queue>]

# or
lpr file [-P <printer-alias>/<queue>]

# hasn't worked for me...
cat you_file.prn | netcat -w 1 printer_ip 9100

# checking info about printers
lpq (-P printer_alias) # check printing queue

lprm # remove jobs from queue (that haven't been processed)

lpstat -p -d # will list all the available printers.

lpinfo -v # find out if your printer is detected by cups
{% endhighlight %}


### File management
{% highlight bash %}
cd /path/to/go/to # change directory to path

ls # list files+folders in a directory

cp from/here to/here # copy

mv from/here to/here # move/rename file

# to move multiple files, you can use wildcards:
mv *IDENTIFIER* destination 
# will move myIDENTIFIER, IDENTIFIERofmine 
# i.e. zero or more characters, followed by IDENTIFIER, 
# followed by zero or more characters to destination

# OR you can use -t flag to set destination:
mv -t DESTINATION file1 file2 file3
{% endhighlight %}

### cat
short for conCATenate

can:
-display file contents:

{% highlight bash %}
cat file

cat -n file #print line numbers

cat -s file #omit repeated empty lines

cat -T file #display 'tab' character as ^I (to distinguish them from space)

cat -e file #display end of line as $
{% endhighlight %}

-copy file contents (you can use cp for this though)

{% highlight bash %}
cat file > file2 #if file2 exists it will be overwritten with file's contents
{% endhighlight %}

-concatenate (of course)
{% highlight bash %}
cat file file2 #concats contents of both files and prints result on console
{% endhighlight %}

-create files
{% highlight bash %}
cat > fileX
# will create a new fileX, and give you the opportunity to write the contents of fileX. Once you are done, CTRL+D will save the file
{% endhighlight %}

--you can use `>>` in place of `>` to append to a file rather than overwrite it\\
-- `>>` can also be used to create files


### ssh
-List files in remote without logging in:\\
`ssh user@host ls path/to/directory`

-Copy files to and from remote using ssh:
{% highlight bash %}
scp file remoteuser@remoteserver:path # from local to remote

scp remoteuser@remoteserver:path/to/file destination # from remote to local

scp [-r] * remoteuser@remoteserver:path # copy all (can copy directories)
{% endhighlight %}

-Create/Edit files in remote (using vim)

{% highlight bash %}
`vi scp://user@host:22//home/user/Documents/file1`
# there are two slashes after the port number, 22 (which you can exclude btw) because the second one
# stands for root directory
{% endhighlight %}

<!-- endregion specific-cmds -->

<!-- region troubleshooting -->
### Troubleshooting
#### OpenSUSE
##### Booting to virtual terminal
Possible issues:

###### 1\. Default target is not graphical:

{% highlight bash %}
  systemctl get-default # something other than graphical.target
  # FIX:
  systemctl set-default graphical.target
{% endhighlight %}

if default is `graphical.target` then maybe the virtual terminal was activated by accident. Force revert to gui by doing:

{% highlight bash %}
  CTRL+ALT+F7 # if doesn't work do CTRL+ALT+(F1-F12)

  # if that still doesn't work force booting to gui:
  init 5
{% endhighlight %}

###### 2\. Insufficient space on disk

Try running `startx` from the virtual terminal (after logging in to root)
if you get an error saying "No space left on device" or "not enough space?", it's possible there's a drive taking up too much space.

<br>Run `df` and scan for anything close to "100%" on the `use` column. For me everything in `dev/sda7` was full. This happended to be where `/var` was mounted.

<br>From [StackOverflow](https://superuser.com/questions/1127028/startx-doesnt-work-not-enough-space):

-Run `sudo du -smx * .[^.]* | sort -n`
-The `-s (--summarize)` option prints the total size for each file/directory.
-The `-m` option prints the disk space used by each file/directory in Megabytes.

-The `-x (--one-file-system)` option forces du to remain on the initial filesystem. This leaves out irrelevant (to this end!) info like all files in /run, /sys, /dev and/or /proc.

-The `[^.].*` includes hidden files while excluding the parent directory, ..).

-Finally, sorting the list numerically conveniently displays the directories taking up the most amount of space at the end of the list.

-You then change into the directory taking up the most space and repeat the process for its subdirectories. Eventually you should find the culprit.

<br>For me though, `/var/tmp` was taking up 28 out of the allocated 30 GB for its partition.
A simple `sudo rm -rf /var/tmp;init 6` fixed my issue
<!-- endregion troubleshooting -->

### References
[SO](https://unix.stackexchange.com/questions/131496/what-is-lightdm-and-gdm) (LightDM vs GDM)

[SO](https://unix.stackexchange.com/questions/20385/windows-managers-vs-login-managers-vs-display-managers-vs-desktop-environment?rq=1) (Desktop Environment vs Display Managers vs Window Manager)

...to be continued