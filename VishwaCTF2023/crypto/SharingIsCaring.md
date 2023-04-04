# **Writeup - VishwaCTF**

* Category **CRYPTO**
* Name **Sharing is Caring**
* Difficulty **MEDIUM**


## Description
In this challenge the flag was encoded using a custom encoding function.
The challenge provides two files:
* a text file containing the encoded flag;
* a python file containing the algorithm used.


## **Solution**
### The **algorithm**
```Python
from sympy import randprime
from random import randrange

k = 3
n = 5
def generate_shares(secret, k, n):
    prime = randprime(secret, 2*secret)
    coeffs = [secret] + [randrange(1, prime) for _ in range(k-1)]
    shares = []
    for i in range(1, n+1):
        x = i
        y = sum(c * x**j for j, c in enumerate(coeffs)) % prime
        shares.append((x, y))
    return shares, prime
```

where `secret` is the _ASCII code_ of the given char.

### Example of an encoded char of the **flag**

```
[(1, 76), (2, 31), (3, 58), (4, 50), (5, 7)], 107
```

### Some considerations
* We have that `k = 3` so

```Python
coeffs = [secret] + [randrange(1, prime) for _ in range(k-1)]
coeffs = [secret] + [randrange(1, prime) for _ in range(2)]
coeffs = [secret, randrange(1, prime), randrange(1, prime)]
```

* Examining the for loop we find that the first iteration where `x = 1` gives the following result

```Python
y = sum(c * x**j for j, c in enumerate(coeffs)) % prime
y = sum(c * 1**j for j, c in enumerate(coeffs)) % prime
y = sum(c * 1 for j, c in enumerate(coeffs)) % prime
y = sum(c for j, c in enumerate(coeffs)) % prime
y = sum(coeffs) % prime
```

* This small considerations seems to be enought to brute force the solution in a reasonable amount of time


```Python
from string import printable
import ast

def lets_try(prime, shares):
	chars = ""  # the possible chars that satisfy the conditions
	# we brute force through all printable chars
	for char in printable:
		bc = ord(char)  # ASCII code of the char
        # we brute force through all possible 
        # random numbers between 1 and the prime number
		for r1 in range(1, prime):
            # there is no need to brute force through the second
            # random number because, from the considerations we 
            # did, we know that 
            # sum([secret, r1, r2]) = shares[0]
			r2 = shares[0] - bc - r1
            # there is no need to check the sign of r2 because
            # we are working with modulo operations
			coeffs = [bc, r1, r2]
			if shares[1] == sum(c * 2**j for j, c in enumerate(coeffs)) % prime:
				if shares[2] == sum(c * 3**j for j, c in enumerate(coeffs)) % prime:
					if shares[3] == sum(c * 4**j for j, c in enumerate(coeffs)) % prime:
						if shares[4] == sum(c * 5**j for j, c in enumerate(coeffs)) % prime:
							chars += char
	# just in case there are more than one char that satisfy all conditions
	if len(chars) > 1:
		return f"[{chars}]"
	return chars

# here we just read the encoded flag
# and decrypt it 
def print_flag():
	flag = ""
	with open("output.txt", "r") as f:
		for line in f.readlines():
			content = line.strip()
			prime_index = content.rfind(",")
			prime = int(content[prime_index + 2:])
			shares = [el[1] for el in ast.literal_eval(content[:prime_index])]
			char = lets_try(prime, shares)
			flag += char
	print(flag)

print_flag()
```


After just a second the result appears to be 

```
VishwaCTF{l4gr4ng[3p]_f0r_th[3n]_w1n[kF!]}
```

We can make a pretty reasonable guess and try

```
VishwaCTF{l4gr4nge_f0r_the_w1n!}
```

And there it is! That was the flag.
