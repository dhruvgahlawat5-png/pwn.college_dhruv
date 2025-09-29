 # Hello Hackers
  ## Intro To Commands
  In this challenge, you will invoke your first command! When you type a command and hit enter, the command will be invoked, as so:  
  ```
  hacker@dojo:~$ whoami  
hacker  
hacker@dojo:~$  
```
Here, the user executed the whoami command, which simply prints the username (hacker) to the terminal. When the command terminates, the shell once again displays the prompt, ready for the next command.  

In this level, invoke the hello command to get the flag! Keep in mind: commands in Linux are case sensitive: hello is different from HELLO.  
  ### Solve
  **Flag:** `pwn.college{Ist3RBatAmpSODLKgXuqtyGXeNf.QX3YjM1wyN1gjNzEzW}`  
```
hacker@hello~intro-to-commands:~$ hello  
Success! Here is your flag:  
pwn.college{Ist3RBatAmpSODLKgXuqtyGXeNf.QX3YjM1wyN1gjNzEzW}  
```


### New Learnings
I learnt how to properly connect to pwn.college using ssh and moreover how to get the flag and put it in pwn.college to get the key.  



  ## Intro To Arguments
  Let's try something more complicated: a command with arguments, which is what we call additional data passed to the command. When you type a line of text and hit enter, the shell actually parses your input into a command and its arguments. The first word is the command, and the subsequent words are arguments. Observe:
   
  ```
  hacker@dojo:~$ echo Hello
Hello
hacker@dojo:~$ 
```
In this case, the command was echo, and the argument was Hello. echo is a simple command that "echoes" all of its arguments back out onto the terminal, like you see in the session above.

Let's look at echo with multiple arguments:

```
hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
hacker@dojo:~$
```
In this case, the command was echo, and Hello and Hackers! were the two arguments to echo. Simple!

In this challenge, to get the flag, you must run the hello command (NOT the echo command) with a single argument of hackers. Try it now! 
 
  ### Solve
  **Flag:** `pwn.college{Qg5MrfhvaJuRnsRJjju6dPa5h0e.QX4YjM1wyN1gjNzEzW}`  
```
hacker@hello~intro-to-arguments:~$ hello hackers
Success! Here is your flag:
pwn.college{Qg5MrfhvaJuRnsRJjju6dPa5h0e.QX4YjM1wyN1gjNzEzW}
```


  ## Command History
  
You're going to type a lot of commands, and typing everything from scratch can be annoying. Luckily, the shell saves a history of every command you invoke.

You can scroll through those saved commands with the up/down arrow keys, and we'll practice that in this challenge. This challenge will inject the flag into your history. Bring up a terminal, hit the up arrow, and grab it! In other challenges, the history will contain the log of the commands you've run, so if you need to run a similar command again, you can use the arrow keys to scroll through and find it!
 
  ### Solve
  **Flag:** `pwn.college{U3tFB1peoYHuzVTUFyoMtuCbgZt.0lNzEzNxwyN1gjNzEzW}`  
```
hacker@hello~command-history:~$ history
    1  whoami
    2  hello
    3  pwn.college{Ist3RBatAmpSODLKgXuqtyGXeNf.QX3YjM1wyN1gjNzEzW}
    4  whoami
    5  hello
    6  hello hacker
    7  hello hacker
    8  hello hackers
    9  hello
   10  the flag is pwn.college{U3tFB1peoYHuzVTUFyoMtuCbgZt.0lNzEzNxwyN1gjNzEzW}
   11  whoami
   12  hello hackers
   13  pwn.college{Ist3RBatAmpSODLKgXuqtyGXeNf.QX3YjM1wyN1gjNzEzW}
   14  whoami
   15  echo hello hackers
   16  HELLO
   17  hello
   18  HELLO
   19  hello
   20  echo hello hackers
   21  the flag is pwn.college{U3tFB1peoYHuzVTUFyoMtuCbgZt.0lNzEzNxwyN1gjNzEzW}
   22  whoami
   23  hello
   24  date
   25  history
   26  the flag is pwn.college{U3tFB1peoYHuzVTUFyoMtuCbgZt.0lNzEzNxwyN1gjNzEzW}
   27  hello
   28  hello
   29  hello
   30  hello hackers
   31  the flag is pwn.college{U3tFB1peoYHuzVTUFyoMtuCbgZt.0lNzEzNxwyN1gjNzEzW}
   32  history
hacker@hello~command-history:~$ the flag is pwn.college{U3tFB1peoYHuzVTUFyoMtuCbgZt.0lNzEzNxwyN1gjNzEzW}
```


### New Learnings
Just using the arrow keys also gave the flag but I kind of confused so I searched about the third one online (well chatGPT ;) ) and I found another command 'history' which gave me all the commands I entered before and then I noticed 'the flag is' since I didn't enter it, so it must be the flag I'm looking for

