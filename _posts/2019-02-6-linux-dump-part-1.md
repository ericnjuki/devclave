---
layout: post
title: "All My Linux: Part 1"
date: 2019-02-06 18:00:00 +0300
tags: linux
---

<span class="dropcaps">T</span>here was an attempt (by me) to 'know linux'. All of my efforts, in all their unedited glory, are hereby chronicled:
### Contents
* [Coming Soon](#coming-soon)
* [Disable users list Ubuntu](#disabling-user-list-at-ubuntu-login-screen)
* [Printing](#printing), [printing gotchas](#gotchas), [printing errors](#errors-you-might-encounter-while-printing)
* [Specific commands](#commands)

#### Coming soon
basics, more specific commands, scripting, tips and tricks, ssh

#### Disabling user list at ubuntu login screen
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
Look [here](https://wiki.ubuntu.com/DebuggingPrintingProblems) (official ubuntu page on debugging printing problems)


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

_to be continued..._