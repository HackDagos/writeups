# **Writeup - VishwaCTF**

* Category **web** 
* Name **Payload** 
* Difficulty **Medium**


## Description

No description.





## **Solution**

On the website you can see that there is a button "System details", when you press it something change in the **URL**

- Normal URL: https://ch42763117925.ch.eng.run/
- After: https://ch42763117925.ch.eng.run/?btn=

I put "robots.txt" in the URL and there's a source code when I open it.

As you can see in the code, you can run a command using the **cmd** parameter.

If you **cat** "index.php" and look at the source code you can see the flag.

flag: **VishwaCTF{y0u_f-o-u-n-d_M3}**