# **Writeup - VishwaCTF**

* Category **Steganography**
* Name **CID**
* Difficulty **Medium**


## Description

Watch the image carefully !!

## **Solution**

I got an image with white text on black background, gotta look at the metadata,
```
$ exiv2 -p all print case69.jpg
Xmp.xmpRights.Certificate                    XmpText    42  This is for you PASS='daya darwaza tod do'
```

this $PASS looks like a password, let's keep it in mind

looking for other informations i could read the output of xxd,

```
$ xxd case69.jpg
...

bunch of other data
...
00107360: 8185 0014 00da 0428 a005 c500 18a0 04c5  .......(........
00107370: 0034 8a00 00a0 05c5 1701 2980 5001 401f  .4........).P.@.
00107380: ffd9 377a bcaf 271c 0004 7d50 d2d9 43c3  ..7z..'...}P..C.
00107390: 0000 0000 0000 2500 0000 0000 0000 69fb  ......%.......i.
001073a0: d03a ffef 6560 6f5d 007f b61b edf0 8440  .:..e`o].......@
...

bunch of other data
...
```

looks like the end of file marker (0xffd9) isn't actually at the end, trim the actual jpeg data, analyze what's left and

```
$ file remaining_data
remaining_data: 7-zip archive data, version 0.4
```

it's a 7-zip archive

after extracting it i'm left with a directory full of images, they all look the same, let's see if there's one that's special

```
$ sha256sum CID\ HQ/* | uniq --check-chars=16
4a3885cdc4b8753dfec6da67a5e98b86e4f45ae4d956915b7ab309c016ad7484  CID HQ/1000.jpg
f50dc3ac1b2fbe8e26a8f225d1d80a492e5901e7385feeccf2608df1694db139  CID HQ/369.jpg
4a3885cdc4b8753dfec6da67a5e98b86e4f45ae4d956915b7ab309c016ad7484  CID HQ/36.jpg
6d31ce13140fad62d9a626d50a730beb7e32085047b23b85e8f59598a17c547a  CID HQ/500_info_for_you.txt
4a3885cdc4b8753dfec6da67a5e98b86e4f45ae4d956915b7ab309c016ad7484  CID HQ/500.jpg
```

looks like 369 is the chosen one with an hash that's unlike any other,

maybe it hides something as well, also it feels like the right time to use the password, so i use steghide to try extracting it

```
$ steghide extract -sf 369.jpg
Enter passphrase: 
wrote extracted data to "flag.txt".
```

eureka! the flag is here

flag: vishwaCTF{my_GOD_D4ya_tumn3_t0_fl4g_dhund_liy4....}