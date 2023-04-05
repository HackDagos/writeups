# **Writeup - VishwaCTF**

* Category **Cryptography** <!-- challenge category -->
* Name **Email incoming** <!-- challenge name -->
* Difficulty **Medium**

## Description
One fine day Johnny received an E-mail which had just this file. He wonders this might have been sent by one of his friend who was supposed to send a confidential message. But Johnny cannot figure out anything from this file. Can you help him retrieve the message????

## **Solution**
The first thing to do is to crack zip password finding that the password is "thunderbird", and extract files. We understand tht justanimage.png is interesting. Then we look at the image  with xdd command executing:
```sh
xxd justanimage.png
```
We see that image header is image created with pyAEScrypt, sot the next step, is trying to change the image's hex with pyAEScrypt. After doing this we obtain the flag.
