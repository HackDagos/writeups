# **Writeup - VishwaCTF**

* Category **forensics** <!-- challenge category -->
* Name **Fraudulent** <!-- challenge name -->
* Difficulty **Medium**


## Description

I got ditched by someone and I need your help !!! The bill amount that was charged to me was not correct. The image of the bill was corrupted. Sources said that some PIXELS of the image were FORRENSICAllY manipulated or edited, leading to changes in the total bill amount. You have to reach the image to see what happened. Remember to analyze every pixel of the image carefully.

P.S.: Round off the actual total amount to closest Integer.

Flag Format : VishwaCTF{actual_total_amount}

## **Solution**

superimposing the 2 frames of the gif you get a pattern of 1s and 0s that reminds of a qr code, so let's try restoring it, the 1s become black pixels and the 0s become white, but it won't scan.

It seems that some parts are missing, namely the position detection patterns, alignment pattern and timing pattern are all mangled, so, after editing again in gimp and restoring the lost pieces, the code is now readable and the content is `https://github.com/Amanjain4269/next-step.git`, that's where the second phase begins.

The link obtained previously refers to a github repository containing an image with the calculations for the bill amount our client said was false, getting a hint from the description we search the web for the word `forensically`, apparently there's a website at the address [https://29a.ch/photo-forensics/](https://29a.ch/photo-forensics/) that offers functions to analyze images for the purpouse of detecting tampering, just what's needed right now.

Using the error level analysis tool you can see that the first digits of both the `phone` and the `laptop` expenses are unlike the others, maybe they were added later? let's try calculating the total amount without these digits...
```
(23454+6574+456280)(1+(18/100))
573843
```

let's try submitting and.. the answer is right

flag: VishwaCTF{573843}