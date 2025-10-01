# Comprehending Commands
## cat: not the pet, but the command!
One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:
```
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files, like so:
```
cat will concatenate (hence the name) multiple files if provided multiple arguments. For example:
```
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
### solve
**Flag:** `pwn.college{sQfgJ8BZr7ORtLP9W3LUY_c4ayj.QXxcTN0wyN1gjNzEzW}`
```
hacker@commands~cat-not-the-pet-but-the-command:~$ ls
Desktop  Downloads  a  d  f  flag  l  o
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{sQfgJ8BZr7ORtLP9W3LUY_c4ayj.QXxcTN0wyN1gjNzEzW}
```

## catting absolute paths
In the last level, you did cat flag to read the flag out of your home directory! You can, of course, specify cat's arguments as absolute paths:
```
hacker@dojo:~$ cat /challenge/DESCRIPTION.md
In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
```
In this directory, I will not copy it to your home directory, but I will make it readable. You can read it with cat at its absolute path: /flag.

FUN FACT: /flag is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.
### solve
**Flag:** `pwn.college{Q1O-cQ_omFAaZtASAH-S9o1KGD1.QX5ETO0wyN1gjNzEzW}`
```
hacker@commands~catting-absolute-paths:~$ cd /
hacker@commands~catting-absolute-paths:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  opt   root  sbin  sys  usr
boot  dev        flag  lib   lib64  media   nix  proc  run   srv   tmp  var
hacker@commands~catting-absolute-paths:/$ cat /flag
pwn.college{Q1O-cQ_omFAaZtASAH-S9o1KGD1.QX5ETO0wyN1gjNzEzW}
```

## more catting practice
You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for you. You must retrieve the flag by absolute path, wherever it is.
### solve
**Flag:** `pwn.college{kQO9uHuBHCf9KCSQKuoDoWSfUmz.QXwITO0wyN1gjNzEzW}`
```
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /usr/share/php7.4-opcache/flag. Go cat it out **without** cding 
into that directory!
hacker@commands~more-catting-practice:~$ cat /usr/share/php7.4-opcache/flag
pwn.college{kQO9uHuBHCf9KCSQKuoDoWSfUmz.QXwITO0wyN1gjNzEzW}
```

## grepping for a needle in a haystack

Sometimes, the files that you might cat out are too big. Luckily, we have the grep command to search for the contents we need! We'll learn it in this challenge.

There are many ways to grep, and we'll learn one way here:
```
hacker@dojo:~$ grep SEARCH_STRING /path/to/file
```
Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

In this challenge, I've put a hundred thousand lines of text into the /challenge/data.txt file. grep it for the flag!

HINT: The flag always starts with the text pwn.college.
### solve
**Flag:** `pwn.college{YMopB_yqTfYbeHPvDSQjUh1TZqv.QX3EDO0wyN1gjNzEzW}`
```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ pwd
/home/hacker
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ cd /
hacker@commands~grepping-for-a-needle-in-a-haystack:/$ grep pwn.college /challenge/data.txt
pwn.college{YMopB_yqTfYbeHPvDSQjUh1TZqv.QX3EDO0wyN1gjNzEzW}
```

## comparing files
When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the diff command becomes invaluable.

diff compares two files line by line and shows you exactly what's different between them. For example:
```
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
```
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
### solve
**Flag:** `< pwn.college{ki_4AoETDp-4jGPeVMN72Hqx08O.01MwMDOxwyN1gjNzEzW}`
```
hacker@commands~comparing-files:~$ diff /challenge/decoy_only.txt /challenge/decoys_and_real.txt
diff: /challenge/decoy_only.txt: No such file or directory
hacker@commands~comparing-files:~$ cd /challenge
hacker@commands~comparing-files:/challenge$ ls
DESCRIPTION.md  decoys_and_real.txt  decoys_only.txt
hacker@commands~comparing-files:/challenge$ diff decoys_and_real.txt decoys_only.txt
80d79
< pwn.college{ki_4AoETDp-4jGPeVMN72Hqx08O.01MwMDOxwyN1gjNzEzW}
```

## listing files
So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the ls command!

ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:
```
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
### solve
**Flag:** `pwn.college{UaCDkFK1AStUEYqG-uosugMAavU.QX4IDO0wyN1gjNzEzW}`
```
hacker@commands~listing-files:~$ ls /challenge
89-renamed-run-23199  DESCRIPTION.md
hacker@commands~listing-files:~$ cd /challenge
hacker@commands~listing-files:/challenge$ ls
89-renamed-run-23199  DESCRIPTION.md
hacker@commands~listing-files:/challenge$ cat 89-renamed-run-23199
#!/opt/pwn.college/bash

echo "Yahaha, you found me! Here is your flag:"
cat /flag
hacker@commands~listing-files:/challenge$ ./89-renamed-run-23199
Yahaha, you found me! Here is your flag:
pwn.college{UaCDkFK1AStUEYqG-uosugMAavU.QX4IDO0wyN1gjNzEzW}
```

## touching files
Of course, you can also create files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by touching it with the touch command:
```
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
```
It's that simple! In this level, please create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get your flag!
### solve
**Flag:** ``
```
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ ls
bin  hsperfdata_root  tmp.4mK6TfTSUV
hacker@commands~touching-files:/tmp$ pwd
/tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.4mK6TfTSUV
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{wAbh2qiY_iPvX_F6Ar3HiLfYY6k.QXwMDO0wyN1gjNzEzW}
```

## removing files
Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you remove files with the rm command, as so:
```
hacker@dojo:~$ touch PWN
hacker@dojo:~$ touch COLLEGE
hacker@dojo:~$ ls
COLLEGE     PWN
hacker@dojo:~$ rm PWN
hacker@dojo:~$ ls
COLLEGE
hacker@dojo:~$
```
Let's practice. This challenge will create a delete_me file in your home directory! Delete it, then run /challenge/check, which will make sure you've deleted it and then give you the flag!
### solve
**Flag:** `pwn.college{IRml-xQ1OZ6F9XplXwILzKExh1j.QX2kDM1wyN1gjNzEzW}`
```
hacker@commands~removing-files:~$ ls
Desktop  Downloads  a  d  f  flag  l  o
hacker@commands~removing-files:~$ touch delete_me
hacker@commands~removing-files:~$ ls
Desktop  Downloads  a  d  delete_me  f  flag  l  o
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ ls
Desktop  Downloads  a  d  f  flag  l  o
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{IRml-xQ1OZ6F9XplXwILzKExh1j.QX2kDM1wyN1gjNzEzW}
```

## moving files

You can also move files around with the mv command. The usage is simple:
```
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
### solve
**Flag:** `pwn.college{ElNHLu_pl_jSOFc7OJOr89pV3o9.0VOxEzNxwyN1gjNzEzW}`
```
hacker@commands~moving-files:~$ ls
Desktop  Downloads  a  d  f  l  o
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{ElNHLu_pl_jSOFc7OJOr89pV3o9.0VOxEzNxwyN1gjNzEzW}
```

## hidden files

Interestingly, ls doesn't list all the files by default. Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts. To view them with ls, you need to invoke ls with the -a flag, as so:
```
hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
```
Now, it's your turn! Go find the flag, hidden as a dot-prepended file in /.
### solve
**Flag:** `pwn.college{Y5VxbspYO5BKrnjFDN5pbOGJZEc.QXwUDO0wyN1gjNzEzW}`
```
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls
bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv            bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-18693198310818  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat .flag-18693198310818
pwn.college{Y5VxbspYO5BKrnjFDN5pbOGJZEc.QXwUDO0wyN1gjNzEzW}
```

## An Epic File Systen Quest

With your knowledge of cd, ls, and cat, we're ready to play a little game!

We'll start it out in /. Normally:
```
hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  us
```
That's a lot of contents! One day, you will be quite familiar with them, but already, you might recognize the flag file and the challenge directory.

In this challenge, I have hidden the flag! Here, you will use ls and cat to follow my breadcrumbs and find it! Here's how it'll work:

Your first clue is in /. Head on over there.
Look around with ls. There'll be a file named HINT or CLUE or something along those lines!
cat that file to read the clue!
Depending on what the clue says, head on over to the next directory (or don't!).
Follow the clues to the flag!
Good luck!
### solve
**Flag:** `pwn.college{czRaxcdq80cbwEKdAW80RsSVsX0.QX5IDO0wyN1gjNzEzW}`
```
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
ALERT  challenge  flag  lib32   media  opt   run   sys  var
bin    dev        home  lib64   mnt    proc  sbin  tmp
boot   etc        lib   libx32  nix    root  srv   usr
hacker@commands~an-epic-filesystem-quest:/$ ls -a
.           ALERT  challenge  flag  lib32   media  opt   run   sys  var
..          bin    dev        home  lib64   mnt    proc  sbin  tmp
.dockerenv  boot   etc        lib   libx32  nix    root  srv   usr
hacker@commands~an-epic-filesystem-quest:/$ cat ALERT
Tubular find!
The next clue is in: /usr/lib/python3/dist-packages/traitlets/utils/tests

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/lib/python3/dist-packages/traitlets/utils/tests
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/traitlets/utils/tests$ ls -a
.  ..  .DOSSIER  __init__.py  __pycache__  test_bunch.py  test_importstring.py
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/traitlets/utils/tests$ cat .DOSSIER
Great sleuthing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/jupyter_console

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/traitlets/utils/tests$ ls /usr/local/lib/python3.8/dist-packages/jupyter_console
HINT-TRAPPED  __main__.py  _version.py  completer.py  tests     zmqhistory.py
__init__.py   __pycache__  app.py       ptshell.py    utils.py
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/traitlets/utils/tests$ cat /usr/local/lib/python3.8/dist-packages/jupyter_console
cat: /usr/local/lib/python3.8/dist-packages/jupyter_console: Is a directory
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/traitlets/utils/tests$ cat /usr/local/lib/python3.8/dist-packages/jupyter_console/HINT-TRAPPED
Great sleuthing!
The next clue is in: /usr/share/doc/libpari-gmp-tls6

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/traitlets/utils/tests$ cd /usr/share/doc/libpari-gmp-tls6
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libpari-gmp-tls6$ ls -a
.  ..  LEAD  changelog.Debian.gz  copyright
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libpari-gmp-tls6$ cat LEAD
Yahaha, you found me!
The next clue is in: /usr/lib/terminfo/s
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libpari-gmp-tls6$ cd /usr/lib/terminfo/s
hacker@commands~an-epic-filesystem-quest:/usr/lib/terminfo/s$ la -a
bash: la: command not found
hacker@commands~an-epic-filesystem-quest:/usr/lib/terminfo/s$ ls -a
.   REVELATION  screen-256color      screen-bce  screen-w               sun
..  screen      screen-256color-bce  screen-s    screen.xterm-256color
hacker@commands~an-epic-filesystem-quest:/usr/lib/terminfo/s$ cat REVELATION
Tubular find!
The next clue is in: /usr/share/xml/docutils

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/terminfo/s$ cd /usr/share/xml/docutils
hacker@commands~an-epic-filesystem-quest:/usr/share/xml/docutils$ la -a
bash: la: command not found
hacker@commands~an-epic-filesystem-quest:/usr/share/xml/docutils$ ls -a
.  ..  .SNIPPET  catalog  catalog.xml  docutils.dtd  soextblx.dtd
hacker@commands~an-epic-filesystem-quest:/usr/share/xml/docutils$ cat .SNIPPET
Lucky listing!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Neo-Euler/Size1/Regular

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/xml/docutils$ ls /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Neo-Euler/Size1/Regular
BLUEPRINT-TRAPPED  Main.js
hacker@commands~an-epic-filesystem-quest:/usr/share/xml/docutils$ cat /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Neo-Euler/Size1/Regular/BLUEPRINT-TRAPPED
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/drivers/video/fbdev/sis

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/xml/docutils$ ls /opt/linux/linux-5.4/drivers/video/fbdev/sis
300vtbl.h     init.c     initdef.h     sis.h        sis_main.h
310vtbl.h     init.h     initextlfb.c  sis_accel.c  vgatypes.h
MEMO-TRAPPED  init301.c  oem300.h      sis_accel.h  vstruct.h
Makefile      init301.h  oem310.h      sis_main.c
hacker@commands~an-epic-filesystem-quest:/usr/share/xml/docutils$ cat /opt/linux/linux-5.4/drivers/video/fbdev/sis/MEMO-TRAPPED
Congratulations, you found the clue!
The next clue is in: /usr/local/lib/python3.8/dist-packages/bs4
hacker@commands~an-epic-filesystem-quest:/usr/share/xml/docutils$ cd /usr/local/lib/python3.8/dist-packages/bs4
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/bs4$ ls -a
.     __init__.py      _typing.py    css.py       element.py     formatter.py
..    __pycache__      _warnings.py  dammit.py    exceptions.py  py.typed
GIST  _deprecation.py  builder       diagnose.py  filter.py
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/bs4$ cat GIST
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{czRaxcdq80cbwEKdAW80RsSVsX0.QX5IDO0wyN1gjNzEzW}
```
### experience
I started to wonder if I'm going in the right direction

## making directories
We can create files. How about directories? You make directories using the mkdir command. Then you can stick files in there!

Watch:
```
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ mkdir my_directory
hacker@dojo:/tmp$ ls
my_directory
hacker@dojo:/tmp$ cd my_directory
hacker@dojo:/tmp/my_directory$ touch my_file
hacker@dojo:/tmp/my_directory$ ls
my_file
hacker@dojo:/tmp/my_directory$ ls /tmp/my_directory/my_file
/tmp/my_directory/my_file
hacker@dojo:/tmp/my_directory$
```
Now, go forth and create a /tmp/pwn directory and make a college file in it! Then run /challenge/run, which will check your solution and give you the flag!
### Solve
**Flag:** `pwn.college{0QvgJK-7krF-DYXyGBOPp9NjI5H.QXxMDO0wyN1gjNzEzW}`
```
hacker@commands~making-directories:~$ cd /
hacker@commands~making-directories:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  opt   root  sbin  sys  usr
boot  dev        flag  lib   lib64  media   nix  proc  run   srv   tmp  var
hacker@commands~making-directories:/$ cd /tmp
hacker@commands~making-directories:/tmp$ ls
bin  hsperfdata_root  tmp.4mK6TfTSUV
hacker@commands~making-directories:/tmp$ mkdir pwn
hacker@commands~making-directories:/tmp$ ls
bin  hsperfdata_root  pwn  tmp.4mK6TfTSUV
hacker@commands~making-directories:/tmp$ cd pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ ls
college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{0QvgJK-7krF-DYXyGBOPp9NjI5H.QXxMDO0wyN1gjNzEzW}
```

## finding files

So now we know how to list, read, and create files. But how do we find them? We use the find command!

The find command takes optional arguments describing the search criteria and the search location. If you don't specify a search criteria, find matches every file. If you don't specify a search location, find uses the current working directory (.). For example:
```
hacker@dojo:~$ mkdir my_directory
hacker@dojo:~$ mkdir my_directory/my_subdirectory
hacker@dojo:~$ touch my_directory/my_file
hacker@dojo:~$ touch my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find
.
./my_directory
./my_directory/my_subdirectory
./my_directory/my_subdirectory/my_subfile
./my_directory/my_file
hacker@dojo:~$
```
And when specifying the search location:
```
hacker@dojo:~$ find my_directory/my_subdirectory
my_directory/my_subdirectory
my_directory/my_subdirectory/my_subfile
hacker@dojo:~
```
And, of course, we can specify the criteria! For example, here, we filter by name:
```
hacker@dojo:~$ find -name my_subfile
./my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find -name my_subdirectory
./my_directory/my_subdirectory
hacker@dojo:~$
```
You can search the whole filesystem if you want!
```
hacker@dojo:~$ find / -name hacker
/home/hacker
hacker@dojo:~$
```
Now it's your turn. I've hidden the flag in a random directory on the filesystem. It's still called flag. Go find it!

Several notes. First, there are other files named flag on the filesystem. Don't panic if the first one you try doesn't have the actual flag in it. Second, there're plenty of places in the filesystem that are not accessible to a normal user. These will cause find to generate errors, but you can ignore those; we won't hide the flag there! Finally, find can take a while; be patient!
### solve
**Flag:** `pwn.college{olQftJ4r0IN6RZU77_sPueKJYGx.QXyMDO0wyN1gjNzEzW}`
```
hacker@commands~finding-files:~$ find / -name flag
find: ‘/root’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
find: ‘/tmp/tmp.4mK6TfTSUV’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
  
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/8/task/8/fd’: Permission denied
find: ‘/proc/8/task/8/fdinfo’: Permission denied
find: ‘/proc/8/task/8/ns’: Permission denied
find: ‘/proc/8/fd’: Permission denied
find: ‘/proc/8/map_files’: Permission denied
find: ‘/proc/8/fdinfo’: Permission denied
find: ‘/proc/8/ns’: Permission denied
/opt/linux/linux-5.4/include/config/printk/safe/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/nix/store/7ns27apnvn4qj4q5c82x0z1lzixrz47p-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag


/nix/store/h88mxp2mbgyj06vypwmqpy05idhwimnp-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag
/nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
hacker@commands~finding-files:~$ 
hacker@commands~finding-files:~$ 
hacker@commands~finding-files:~$ 
hacker@commands~finding-files:~$ cat /usr/local/lib/python3.8/dist-packages/pwnlib/flag
cat: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /opt/linux/linux-5.4/include/config/printk/safe/flag
pwn.college{olQftJ4r0IN6RZU77_sPueKJYGx.QXyMDO0wyN1gjNzEzW}
```

## linking files

If you use Linux (or computers) for any reasonable length of time to do any real work, you will eventually run into some variant of the following situation: you want two programs to access the same data, but the programs expect that data to be in two different locations. Luckily, Linux provides a solution to this quandary: links.

Links come in two flavors: hard and soft (also known as symbolic) links. We'll differentiate the two with an analogy:

A hard link is when you address your apartment using multiple addresses that all lead directly to the same place (e.g., Apt 2 vs Unit 2).
A soft link is when you move apartments and have the postal service automatically forward your mail from your old place to your new place.
In a filesystem, a file is, conceptually, an address at which the contents of that file live. A hard link is an alternate address that indexes that data --- accesses to the hard link and accesses to the original file are completely identical, in that they immediately yield the necessary data. A soft/symbolic link, instead, contains the original file name. When you access the symbolic link, Linux will realize that it is a symbolic link, read the original file name, and then (typically) automatically access that file. In most cases, both situations result in accessing the original data, but the mechanisms are different.

Hard links sound simpler to most people (case in point, I explained it in one sentence above, versus two for soft links), but they have various downsides and implementation gotchas that make soft/symbolic links, by far, the more popular alternative.

In this challenge, we will learn about symbolic links (also known as symlinks). Symbolic links are created with the ln command with the -s argument, like so:
```
hacker@dojo:~$ cat /tmp/myfile
This is my file!
hacker@dojo:~$ ln -s /tmp/myfile /home/hacker/ourfile
hacker@dojo:~$ cat ~/ourfile
This is my file!
hacker@dojo:~$
```
You can see that accessing the symlink results in getting the original file contents! Also, you can see the usage of ln -s. Note that the original file path comes before the link path in the command!

A symlink can be identified as such with a few methods. For example, the file command, which takes a filename and tells you what type of file it is, will recognize symlinks:
```
hacker@dojo:~$ file /tmp/myfile
/tmp/myfile: ASCII text
hacker@dojo:~$ file ~/ourfile
/home/hacker/ourfile: symbolic link to /tmp/myfile
hacker@dojo:~$
```
Okay, now you try it! In this level the flag is, as always, in /flag, but /challenge/catflag will instead read out /home/hacker/not-the-flag. Use the symlink, and fool it into giving you the flag!
### solve
**Flag:** ``
```

```
