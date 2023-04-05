# **Writeup - VishwaCTF**

* Category **steganography** 
* Name **Just Files** 
* Difficulty **Medium**


## Description

They are not what you see. They are different. Believe me.


## **Solution**

First, use **binwalk** and get the Morse Code and the .wav inside the zip. 

*Morse Code*:
R E V E R S E T H E A U D I O A N D Y O U S H O U L D F I N D N A M E O F P R O T A G O N I S T . I T O L D Y O U T H A T S T O R Y I N P N G F I L E ." 

If you reverse the .wav you can listen at **Lucifer Morningstar** which says the name of Jimmy (Jimmy Barners). 

If you look at the header there's also "S01E03". 

flag: **VishwaCTF{Lucifer_S01E03}**
