# **Writeup - VishwaCTF**

* Category **web** 
* Name **aLive** 
* Difficulty **Medium**


## Description

In my college level project I created this website that tells us if any domain/ip is active or not. But there is a catch.


## **Solution**

The proper method to solve this challenge was doing a **Blind Command Injection**.

Try to put ;id and see what happens. You have to use **netcat** and send the ;ls command. You'll see that there's a file called "flag.txt". 

To print the flag, we can use the **cat** command or we can access to the directory (add /flag.txt to the URL). 

flag: **VishwaCTF{b1inD_cmd-i}**
