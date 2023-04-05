# **Writeup - VishwaCTF**

* Category **rev** 
* Name **Reverse Hill** 
* Difficulty **Medium**


## Description

Buddy Backpacker a famous hiker had gone for a hike on the reverse_hill. I have decided to go on this hike but i do not know the best way up. So i approached Buddy Backpacker for help and he gave me this file. But there is some problem. I think its not giving me the proper way. Can you help me? And if you succeed you can have a flag in return.

Hint:When entering the flag use a underscore(_) after each word.


## **Solution**

This challenge is about reversing a Hill Cipher decryption function that uses a randomized matrix. 

Note that the Hill Cipher decryption function is "spread" across three functions named **function1**, **function2**, and **function3**. 

**function1**: This function takes a single argument *a* which represents the row number of the matrix we should decrypt. It also calls function2, but with just this function we won't do much.

**function2**: This function initializes the *c* matrix with the *a* matrix provided in the code. 

**function3**: generates a randomized matrix c by generating random values. This function then returns a pointer to the *c* matrix.

**SOLVE**: patch function3 to return a "fixed" matrix instead of a randomized one. We can patch it using a debugger.

**ANOTHER SOLUTION**: patch function2 to get the randomized c matrix and then use it to take the b matrix and the plaintext for a single row. 

flag: **VishwaCTF{matrix_the_way_around}**
