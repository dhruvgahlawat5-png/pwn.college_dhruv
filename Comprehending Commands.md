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
