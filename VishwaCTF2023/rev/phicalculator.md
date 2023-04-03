# **Writeup - VishwaCTF**

* Category: **Rev**
* Name: **Phi Calculator**
* Difficulty: **Easy**

## Description
We are given a python file of a program that is in a trial version.
The interesting parts of the program are:
* the `key_part_static1_trial` variable which contains the initial part of the flag
* the `check_key` function that checks if the provided key is correct

## Solution
We can retrieve the key by following the steps of the `check_key` function to obtain the dynamic part of the flag and then put them together.

```
import hashlib
bUsername_trial = b"vishwaCTF"
key_part_static1_trial = "VishwaCTF{m4ke_it_p0ssible_"
key_part_dynamic_trial = ""
key_part_static2_trial = "}"
hashed_key = hashlib.sha256(bUsername_trial).hexdigest()
arr = [4, 5, 3, 6, 2, 7, 1, 8] 
key_part_dynamic_trial = "".join([hashed_key[i] for i in arr])
key = key_part_static1_trial + key_part_dynamic_trial + key_part_static2_trial
print(key)
```

`VishwaCTF{m4ke_it_p0ssible_b7cdc517}`
