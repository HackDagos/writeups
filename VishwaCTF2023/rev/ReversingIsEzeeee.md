# **Writeup - VishwaCTF**

* Category **Reversing**
* Name **Reversing is Ezeeee**
* Difficulty **Medium**

## Description
We are given an exe file called `examine.exe` and nothing else.

## **Solution**
By looking at the strings in the file, we found that pygame was used (a python library).
In order to solve this challenge you have to convert the exe back to python with a tool like [pyinstxtractor](https://github.com/extremecoders-re/pyinstxtractor).
Once you have extracted the file you'll find a folder with many file. Look for strings inside the `examine.pyc` file and you'll find this hex bytes string: `5669736877614354467b31355f70797468306e5f7468335f623335745f6c346e67753467333f3f7d`.
By converting it in a printable string with the command:
```sh
echo "5669736877614354467b31355f70797468306e5f7468335f623335745f6c346e67753467333f3f7d" | xxd -r -p
```

you'llget the flag:
`VishwaCTF{15_pyth0n_th3_b35t_l4ngu4g3??}`

