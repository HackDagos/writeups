# **Writeup - VishwaCTF**

* Category **Steganography** <!-- challenge category -->
* Name **XOR** <!-- challenge name -->
* Difficulty **Medium**

## Description
My friend sent me a clip and I found it to be very interesting. I wanted to watch the full video but before I could rewatch the clip, he deleted it!! All I have right now is this image he sent me afterwards. Can you help me find the video link?

## **Solution**
The only file we had was an image, so the first thing to do was executing exiftool on the image in order to know more about the image with:
```sh
exiftool BossCat.jpg 
```
With the command we see there is a field name License that seems in the format of a base 64 or base 32. So by using:
```sh
echo "IFAUCLJXLIWUKQZTGIWUIMZS" | base32 -d
```
We obtain "AAA-7Z-EC32-D32" that maybe is a password for something. At this point we try to use steghide on image to see if there is something to extract, using the string obtained from the previous step as password. So executing:
```sh
steghide extract -sf BossCat.jpg
```
Extracted data are wrote into an archive secret.zip, and extracting files from it we obtain two images "n1.png" and "n2.png". So the last step to do, as the title of the challenge is XOR, is to xor the two images with the following python code:
```Python
from PIL import Image, ImageChops  
  
im1 = Image.open("n1.png").convert("1")  
im2 = Image.open("n2.png").convert("1")  
  
# applying logical_xor method  
im3 = ImageChops.logical_xor(im1, im2)  
im3.save('xored.png')
```
The obtained image contain a link which is the content of the flag, so the flag is: VishwaCTF{https://youtu.be/LlhKZaQk860}