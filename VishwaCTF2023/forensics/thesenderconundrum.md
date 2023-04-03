# **Writeup - VishwaCTF**

* Category **Forensics**
* Name **The Sender Conundrum**
* Difficulty **Easy**

## Description
We are given two files, an email SMTP transcript and a zip folder encrypted with a password called "unzipme.zip"

## Solution
The email contains a riddle whose solution is "name". Looking for names in the email we can see BrandonLee@anonymousemail.me.
Unzip the zip folder with password "BrandonLee" and you will get the flag.txt file.

`vishwaCTF{1d3n7i7y_7h3f7_is_n0t_4_j0k3}`
