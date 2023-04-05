# **Writeup - VishwaCTF**

* Category **Steganography**
* Name **Can you see me?**
* Difficulty **Easy**


## Description

A magician made the seven wonders disappear. But people claim they can still feel their presence in the air.

## **Solution**

The challenge gave me an image of the seven wonders, let's see if there are interesting strings inside

```
$ strings havealook.jpg
...

**a bunch of garbage**

...
h       CA
q!|&
[YoBt
Z       hPy
*$# 
{!,B
{y}D
        HoEi//
A*Ve
,U~N
VZHV
hereissomething.wavPK
```

`hereissomething.wav`, interesting, it's an uncommon string to find in a jpeg, also the letters `PK` besides it remind of a zip archive. Let's try extracting whatever it is

```
$ unzip havealook.jpg
Archive:  havealook.jpg
warning [havealook.jpg]:  134855 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: hereissomething.wav
```

so it was really a zip archive after all.

Let's try listening to this something

```
$ ffplay hereissomething.wav
```

it certainly isn't pleasing to hear, but the spectrogram shows something interesting, it's the flag:
* vishwaCTF{n0w_y0u_533_m3}