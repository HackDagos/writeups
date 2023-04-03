# **Writeup - VishwaCTF**

* Category **Crypto**
* Name **Unfolded**
* Difficulty **Medium**

## Description
We are given a file called `Step_1.json`, which contained an encrypted json with a plaintext key.
In the description we get a hint about Giovan Battista Bellaso.

## Solution
1. Decrypt the json file with a vigenere cipher decrypt tool, using the key provided.
2. The decrypted file looks like this:
```
Original:
{
    "Dmwktihi": "xpdnsrwp0690",
    "Beaera": "Vrxgovg Gmznfgismix, Qtb Qhympxjextb,Jtyc sbxuki",
    "Nxmvgbdsh": "4ih sdlt",
    "Mwmlbzcoi": "Wwiawx Ksmcfz Gkvhyby",
    "Key": "justgiveupanddie"
}


Decrypted:
{
   "Username": "dadapool0690",
   "Skills": "Android Development, Web Development,Open source",
   "Education": "4th fail",
   "Institute": "Chintu Coding Academy"
}
```
3. Since under skills there are coding related skills, search `dadapool0690` on github.
4. Found a user with a corresponding username who have only one repo.
5. This repo contained a base64 encoded image called "FOLDME"
6. "Fold" the image. This can be done with gimp following these steps:
    * open the image in gimp
    * duplicate the layer and make both layer to 50% opacity
    * select the flip tool and flip one layer vertically
    * to better see the text duplicate the gray channel a few times and you should see an image:
![folded.png](folded.png)
7. Go to the drive folder and open the flag.txt file

`VishwaCTF{0r1g4m1_1s_4n_4rt_856462584532}`
