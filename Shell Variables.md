# Shell Variables
## printing variables

Let's start with printing variables out. The /challenge/run program will not, and cannot, give you the flag, but that's okay, because the flag has been put into the variable called "FLAG"! Just have your shell print it out!

You can accomplish this using a number of ways, but we'll start with echo. This command just prints stuff. For example:
```
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
```
You can also print out variables with echo, by prepending the variable name with a $. For example, there is a variable, PWD, that always holds the current working directory of the current shell. You print it out as so:
```
hacker@dojo:~$ echo $PWD
/home/hacker
```
Now it's your turn. Have your shell print out the FLAG variable and solve this challenge!
### solve
**Flag:** `pwn.college{4G3l9iF1tdUlNrO-5L8eXy_Q_hg.QX3UTN0wyN1gjNzEzW}`
```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{4G3l9iF1tdUlNrO-5L8eXy_Q_hg.QX3UTN0wyN1gjNzEzW}
```

## setting variables

Naturally, as well as reading values stored in variables, you can write values to variables. This is done, as with many other languages, using =. To set variable VAR to value 1337, you would use:
```
hacker@dojo:~$ VAR=1337
```
Note that there are no spaces around the =! If you put spaces (e.g., VAR = 1337), the shell won't recognize a variable assignment and will, instead, try to run the VAR command (which does not exist).

Also note that this uses VAR and not $VAR: the $ is only prepended to access variables. In shell terms, this prepending of $ triggers what is called variable expansion, and is, surprisingly, the source of many potential vulnerabilities (if you're interested in that, check out the Art of the Shell dojo when you get comfortable with the command line!).

After setting variables, you can access them using the techniques you've learned previously, such as:
```
hacker@dojo:~$ echo $VAR
1337
```
To solve this level, you must set the PWN variable to the value COLLEGE. Be careful: both the names and values of variables are case-sensitive! PWN is not the same as pwn and COLLEGE is not the same as College.
### solve
**Flag:** `pwn.college{wQhQtsuElcNpnF8PUkJJCRos1-M.QX5UTN0wyN1gjNzEzW}`
```
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{wQhQtsuElcNpnF8PUkJJCRos1-M.QX5UTN0wyN1gjNzEzW}
```

## multi-word variables
In this level, you will learn about quoting. Spaces have special significance in the shell, and there are places where you can't use them spuriously. Recall our variable setting:
```
hacker@dojo:~$ VAR=1337
```
That sets the VAR variable to 1337, but what if you wanted to set it to 1337 SAUCE? You might try the following:
```
hacker@dojo:~$ VAR=1337 SAUCE
```
This looks reasonable, but it does not work, for similar reasons to needing to have no spaces around the =. When the shell sees a space, it ends the variable assignment and interprets the next word (SAUCE in this case) as a command. To set VAR to 1337 SAUCE, you need to quote it:
```
hacker@dojo:~$ VAR="1337 SAUCE"
```
Here, the shell reads 1337 SAUCE as a single token, and happily sets that value to VAR. In this level, you'll need to set the variable PWN to COLLEGE YEAH. Good luck!
### solve
**Flag:** `pwn.college{g7Vh9YgOOVDv3ZLoBkkJVKFEyT9.QXwYTN0wyN1gjNzEzW}`
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{g7Vh9YgOOVDv3ZLoBkkJVKFEyT9.QXwYTN0wyN1gjNzEzW}
```

## exporting variables

By default, variables that you set in a shell session are local to that shell process. That is, other commands you run won't inherit them. You can experiment with this by simply invoking another shell process in your own shell, like so:
```
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is:
```
In the output above, the $ prompt is the prompt of sh, a minimal shell implementation that is invoked as a child of the main shell process. And it does not receive the VAR variable!

This makes sense, of course. Your shell variables might have sensitive or weird data, and you don't want it leaking to other programs you run unless it explicitly should. How do you mark that it should? You export your variables. When you export your variables, they are passed into the environment variables of child processes. You'll encounter the concept of environment variables in other challenges, but you'll observe their effects here. Here is an example:
```
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```
Here, the child shell received the value of VAR and was able to print it out! You can also combine those first two lines.
```
hacker@dojo:~$ export VAR=1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```
In this challenge, you must invoke /challenge/run with the PWN variable exported and set to the value COLLEGE, and the COLLEGE variable set to the value PWN but not exported (e.g., not inherited by /challenge/run). Good luck!
### solve
**Flag:** `pwn.college{8rrY8R64IUsT7eKPbnmkCXJfWJS.QXyYTN0wyN1gjNzEzW}`
```
hacker@variables~exporting-variables:~$ export PWN=COLLEGE; COLLEGE=PWN; /challenge/run
Incorrect...
You have not set the COLLEGE variable to the correct value (it should be 
'PWN'). Do that before running this script! Even though it is not exported, in 
this challenge, we have ways to check...
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ export PWN=COLLEGE; COLLEGE=PWN; /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{8rrY8R64IUsT7eKPbnmkCXJfWJS.QXyYTN0wyN1gjNzEzW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```

## printing exported variables

There are multiple ways to access variables in bash. echo was just one of them, and we'll now learn at least one more in this challenge.

Try the env command: it'll print out every exported variable set in your shell, and you can look through that output to find the FLAG variable!
## solve
**Flag:** `pwn.college{s8RWVpyeQ_b-H3oR0TiMT5zEghJ.QX4UTN0wyN1gjNzEzW}`
```
hacker@variables~printing-exported-variables:~$ env | grep FLAG
FLAG=pwn.college{s8RWVpyeQ_b-H3oR0TiMT5zEghJ.QX4UTN0wyN1gjNzEzW}
```

## storing command output

In the course of working with the shell, you will often want to store the output of some command into a variable. Luckily, the shell makes this quite easy using something called Command Substitution! Observe:
```
hacker@dojo:~$ FLAG=$(cat /flag)
hacker@dojo:~$ echo "$FLAG"
pwn.college{blahblahblah}
hacker@dojo:~$
```
Neat! Now, you practice. Read the output of the /challenge/run command directly into a variable called PWN, and it will contain the flag!

Trivia: You can also use backticks instead of $(): FLAG=`cat /flag` instead of FLAG=$(cat /flag) in the example above. This is an older format, and has some disadvantages (for example, imagine if you wanted to nest command substitutions. How would you do $(cat $(find / -name flag)) with backticks? The official stance of pwn.college is that you should use $(blah) instead of `blah`.
## solve
**Flag:** `pwn.college{8ngv6mRHOGFR8WB3OEeFhD7bL7y.QX1cDN1wyN1gjNzEzW}`
```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo $PWN
pwn.college{8ngv6mRHOGFR8WB3OEeFhD7bL7y.QX1cDN1wyN1gjNzEzW}
```

## reading input

We'll start with reading input from the user (you). That's done using the aptly named read builtin, which reads input into a variable!

Here is an example using the -p argument, which lets you specify a prompt (otherwise, it would be hard for you, reading this now, to separate input from output in the example below):
```
hacker@dojo:~$ read -p "INPUT: " MY_VARIABLE
INPUT: Hello!
hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
You entered: Hello!
```
Keep in mind, read reads data from your standard input! The first Hello!, above, was inputted rather than outputted. Let's try to be more explicit with that. Here, we annotated the beginning of each line with whether the line represents INPUT from the user or OUTPUT to the user:
```
 INPUT: hacker@dojo:~$ echo $MY_VARIABLE
OUTPUT:
 INPUT: hacker@dojo:~$ read MY_VARIABLE
 INPUT: Hello!
 INPUT: hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
OUTPUT: You entered: Hello!
```
In this challenge, your job is to use read to set the PWN variable to the value COLLEGE. Good luck!
## solve
**Flag:** `pwn.college{EsmDfutJf1dUEz8BLGQ7f-16ELp.QX4cTN0wyN1gjNzEzW}`
```
hacker@variables~reading-input:~$ read PWN
COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{EsmDfutJf1dUEz8BLGQ7f-16ELp.QX4cTN0wyN1gjNzEzW}
```

## reading files
Often, when shell users want to read a file into an environment variable, they do something like:
```
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ VAR=$(cat some_file)
hacker@dojo:~$ echo $VAR
test
```
This works, but it represents what grouchy hackers call a "Useless Use of Cat". That is, running a whole other program just to read the file is a waste. It turns out that you can just use the powers of the shell!

Previously, you read user input into a variable. You've also previously redirected files into command input! Put them together, and you can read files with the shell.
```
hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ read VAR < some_file
hacker@dojo:~$ echo $VAR
test
```
What happened there? The example redirects some_file into the standard input of read, and so when read reads into VAR, it reads from the file! Now, use that to read /challenge/read_me into the PWN environment variable, and we'll give you the flag! The /challenge/read_me will keep changing, so you'll need to read it right into the PWN variable with one command!
### solve
**Flag:** `pwn.college{MZOncl-MTMF39u3X1P651QjJqBN.QXwIDO0wyN1gjNzEzW}`
```
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{MZOncl-MTMF39u3X1P651QjJqBN.QXwIDO0wyN1gjNzEzW}
```
