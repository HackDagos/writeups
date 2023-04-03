# **Writeup - VishwaCTF**

* Category **Web**
* Name **Eeezzy**
* Difficulty **Easy**

## Description
The challenge was about bypassing a login in php.
By viewing the source of the page, we can see that there is a `strcmp` between our get parameters (username, password) and something we don't know.
This check is inside a try catch block and if it catches a `throwable` it will print the flag.
(Can't be more specific or upload the code used by the server because we don't have access to the istance after the end of the CTF)

## Solution
Send the GET parameters as array so `strcmp` will throw an error.
`curl https://ch41763110254.ch.eng.run/?username[]=[]&password[]=[]&submit=Login`

`VishwaCTF{5t0p_c0mp4r1ng}`
