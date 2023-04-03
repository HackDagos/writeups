# **Writeup - VishwaCTF**

* Category **Crypto**
* Name **The indecipherable cipher**
* Difficulty **Medium**

## Description
We are given this string `j3qrh4kgz3iptmyqxcw0zkm8i5xugs5lwl0lrwvirwktlqinexcw0zkmq5nqvpebpor5wqipqhw2ikzm4ipktzlr` and the description cites "Mr. Kasiski".

## Solution
Kasiski was an hint for the Vigenere cipher. We can decrypt the ciphertext with [dcode.fr](https://www.dcode.fr/vigenere-cipher) automatic decryption by extending the normal alphabet with numbers.

The plaintext is `friedrichwilhelmkasiskiwastheonewhodesignedtheaaakasiskiexaminationtodecodevignerecipher`.

`VishwaCTF{friedrichwilhelmkasiskiwastheonewhodesignedtheaaakasiskiexaminationtodecodevignerecipher}`
