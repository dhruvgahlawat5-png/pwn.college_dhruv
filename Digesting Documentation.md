# Digesting Documentation
## Learning From Documentation

The typical need you'll have for documentation is just to figure out how to use all these dang programs, and a specific case of that is figuring out what arguments to specify on the command line. This module will mostly dig into that concept, as a proxy for figuring out how to use the programs in general. Through the rest of the module, you'll go through various ways of asking the environment for help for the programs, but first, we'll dig into the concept of reading documentation.

The correct usage of programs depends, in a large part, on the proper specification of arguments to them. Recall the -a of ls -a in the hidden files challenge of the Basic Commands module: that -a was an argument that told ls to list out hidden files as well as non-hidden files. Because we wanted to list out hidden files, invoking ls with the -a argument was the correct way to use it in our scenario.

The program for this challenge is /challenge/challenge, and you'll need to invoke it properly in order for it to give you the flag. Let's pretend that this is its documentation:

Welcome to the documentation for /challenge/challenge! To properly run this program, you will need to pass it the argument of --giveflag. Good luck!

Given that knowledge, go get the flag!
### solve
**Flag:** `pwn.college{c9QWCAnEFBe2Bj4tlKNugB-kvqo.QX0ITO0wyN1gjNzEzW}`
```
hacker@man~learning-from-documentation:~$ cd /challenge
hacker@man~learning-from-documentation:/challenge$ ls
DESCRIPTION.md  challenge
hacker@man~learning-from-documentation:/challenge$ ls -a
.  ..  .init  DESCRIPTION.md  challenge
hacker@man~learning-from-documentation:/challenge$ ./challenge
Incorrect usage! You must pass an argument to me (read the challenge 
description for details).
hacker@man~learning-from-documentation:/challenge$ cat challenge
cat: challenge: Permission denied
hacker@man~learning-from-documentation:/challenge$ cat .init
#!/usr/bin/env python

import os
os.chmod("/challenge/challenge", 0o4711)
hacker@man~learning-from-documentation:/challenge$ ./challenge --giveflag
Correct argument! Here is your flag:
pwn.college{c9QWCAnEFBe2Bj4tlKNugB-kvqo.QX0ITO0wyN1gjNzEzW}
```

## Learning Complex Usage

While using most commands is straightforward, the usage of some commands can get quite complex. For example, the arguments to commands like sed and awk, which we're definitely not getting into right now, are entire programs in an esoteric programming language! Somewhere on the spectrum between cd and awk are commands that take arguments to their arguments...

This sounds crazy, but you've already encountered this with the find level in Basic Commands. find has a -name argument, and the -name argument itself takes an argument specifying the name to search for. Many other commands are analogous.

Here is this level's documentation for /challenge/challenge:

Welcome to the documentation for /challenge/challenge! This program allows you to print arbitrary files to the terminal, when given the --printfile argument. The argument to the --printfile argument is the path of the flag to read. For example, /challenge/challenge --printfile /challenge/DESCRIPTION.md will print out the description of the level!

Given that documentation, go get the flag!
### solve
**Flag:** `pwn.college{IrG4J3DMMuhswtthbrqo-xWUuhA.QX1ITO0wyN1gjNzEzW}`
```
hacker@man~learning-complex-usage:~$ cd /challenge
hacker@man~learning-complex-usage:/challenge$ ls
DESCRIPTION.md  challenge
hacker@man~learning-complex-usage:/challenge$ ls -a
.  ..  .init  DESCRIPTION.md  challenge
hacker@man~learning-complex-usage:/challenge$ ./challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{IrG4J3DMMuhswtthbrqo-xWUuhA.QX1ITO0wyN1gjNzEzW}
```

## Reading Manuels

This level introduces the man command. man is short for manual, and will display (if available) the manual of the command you pass as an argument. For example, let's say we wanted to learn about the yes command (yes, this is a real command):
```
hacker@dojo:~$ man yes
```
This will display the manual page for yes, which will look something like this:
```
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
```
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
### solve
**Flag:** `pwn.college{4yS_W_jIntJ20JQQCo3snxTPRkE.QX0EDO0wyN1gjNzEzW}`
```
hacker@man~reading-manuals:~$ man challenge
CHALLENGE(1)                  Challenge Commands                  CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --yjntos NUM
              print the flag if NUM is 420

AUTHOR
       Written by Zardus.
Manual page challenge(1) line 1/32 68% (press h for help or q to quit)
hacker@man~reading-manuals:~$ cd /challenge
hacker@man~reading-manuals:/challenge$ ./challenge --yjntos 420
Correct usage! Your flag: pwn.college{4yS_W_jIntJ20JQQCo3snxTPRkE.QX0EDO0wyN1gjNzEzW}
```

## searching manuels

You can scroll man pages with the arrow keys (and PgUp/PgDn) and search with /. After searching, you can hit n to go to the next result and N to go to the previous result. Instead of /, you can use ? to search backwards!

Find the option that will give you the flag by reading the challenge man page.
### solve
**Flag:** `pwn.college{QmTex6-Hwl2_riIdV1p5dG1hb0L.QX1EDO0wyN1gjNzEzW}`
```
hacker@man~searching-manuals:~$ man challenge
 --iyuykqn
              This argument will give you the flag!
hacker@man~searching-manuals:~$ /challenge/challenge --iyuykqn
Initializing...
Correct usage! Your flag: pwn.college{QmTex6-Hwl2_riIdV1p5dG1hb0L.QX1EDO0wyN1gjNzEzW}
```

## searching for manuels
This level is tricky: it hides the manpage for the challenge by randomizing its name. Luckily, all of the manpages are gathered in a searchable database, so you'll be able to search the man page database to find the hidden challenge man page! To figure out how to search for the right manpage, read the man page manpage by doing: man man!

HINT 1: man man teaches you advanced usage of the man command itself, and you must use this knowledge to figure out how to search for the hidden manpage that will tell you how to use /challenge/challenge

HINT 2: though the manpage is randomly named, you still actually use /challenge/challenge to get the flag!
### solve
**Flag:** ``
```
man -k printf
           Search the short descriptions and manual page names for the keyword
           printf as regular expression.  Print out any  matches.   Equivalent
           to apropos printf.
```
