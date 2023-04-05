# **Writeup - VishwaCTF**

* Category **steganography** 
* Name **Quick Heal** 
* Difficulty **Medium**


## Description

Security Simplified!!

(Everything is there)

## **Solution**

To extract all the frames from the .mkv video, use a media player (VLC) that allows you to save individual frames as image files. 

1. Open VLC and go to Media
2. Select "Convert"
3. Click Add and insert ur file
4. Put the destination

Now that you have the audio file, you can use Audacity to extract the other part of the flag. Open Audacity and import the audio file you just extracted.

flag: **VishwaCTF{S3cur1ty_S1mpl1f13d_5NJ0Y_C0UP0NS}**


