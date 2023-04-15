# **Writeup - HackPackCTF**

* Category **Misc** 
* Name **Cat Me if You Can** 
* Difficulty **Easy**


## Description

>There's a flag hiding in plain sight, Our cat has been trying to get it for a while now, but it keeps escaping him at the last moment. Can you help him out? Author: Chika
><span style="color:red">nc cha.hackpack.club 41708 </span>


## **Solution**

As soon as we connect to the service we can see that we are provided with a reverse shell:

![reverse shell](img/cat_me_if_you_can_cat.png)

Let's take a look at what's inside the start folder;

by running the command `ls -la` we check the files inside the folder and discover the presence of only one file called "flag.txt"

![ls -la](img/cat_me_if_you_can_ls.png)

If we use the command "cat" to read the file, we'll see that our reverse shell has limitations, and it will respond with "hisssss"

![cat](img/cat_me_if_you_can_cat.png)

>About this challenge I found two solutions (there would be millions of them)

### **First solution (command substitution)**

The goal is simple:
run `>flag.txt` in a subshell and pass the result to `echo`.

This allows us to bypass the filter and read the flag,
using `$()`..

A brief explanation of the command:

>The command contained in `$()` or between the backticks \`..\` is executed in a subshell and the output is then inserted into the original command.

`echo $(<flag.txt)`

![echo](img/cat_me_if_you_can_echo.png)

### **Second solution (pr command)**

The goal is simple:

print all the files in the folder 

A brief explanation of the command:

>pr - convert text files for printing

`pr *`

![pr](img/cat_me_if_you_can_pr.png)


flag: ***flag{(^._.^)_m3ow_me0w_(^._.^)}***
