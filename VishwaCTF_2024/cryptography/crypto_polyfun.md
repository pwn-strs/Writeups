# Poly Fun

> We had second blood in this challenge

In this challenge we were provided with `challenge.py` , `flag.txt`, `key.txt`

where `flag.txt` contains base64 encoded data, `key.txt` contains some UTF-8 encoded data.
The challenge description mentions symmetric encryption and something weird about the key.

In the challenge, the `transform` function was the identity function due to some mathematical facts.

Atleast if the author would have coded it up correctly `¯\_(ツ)_/¯`.

For example:

```py
    number = random.randint(1, 100000)
    org = number
    number *= 2
    number += 15
    number *= 3
    number += 33
    number /= 6
    number -= org
```

After this, number will have the value $13$ irrespective of original value of `number`.
Then the following `if number==13 :` check succeeds and the else block is never executed.

But author didn't know that you needed to pad a number to 4 digits for [kaprekar's routine](https://en.wikipedia.org/wiki/Kaprekar%27s_routine) to converge, hence that `while` loop would have taken a while for inputs like `1000`. 

Anyways, that's besides the point.
After replacing `transform` with identity, we get

```py
import numpy as np
import random

polyc = [4,3,7]
poly = np.poly1d(polyc)



def encrypt(p,key):
    return ''.join(chr(p(i)) for i in key) # p(x) = 4*x*x + 3*x + 7


key = open('key.txt', 'rb').read()
enc = encrypt(poly,key)
print(enc)
```

So, the `encrypt` function just takes each character and encodes it as `chr(p(ord(c)))`, where c is the character and p is the given polynomial.

To reverse the encoding, we just need to take `chr(invp(ord(i)))`, where `i` is the encoded character and $\text{invp}(x) = \frac{\sqrt{16x - 103} - 3}{8}$ by the quadratic formula.

On inspecting the content of the provided `key.txt`, it consisted of `utf-8` encoded bytes with `ord` values greater than 9000. On trying to decode the content of `key.txt` after reading the hint in the challenge description, we recover the actual key used to encrypt the flag, namely `12345678910111213141516171819202`

Since the challenge mentioned __symmetric key encryption__ we try to decrypt `flag.txt` using the discovered key and `AES ECB mode`.

Combining all of it, here's the attached solve script.

```py
from base64 import b64decode
from math import isqrt
import numpy as np

with open("key.txt","rb") as f: key = f.read()
with open("flag.txt","r") as f: flag = f.read()

flag = b64decode(flag)

key  =  "".join(chr(((isqrt(16*ord(i)-103) - 3)//8)) for i in key.decode("utf-8")).encode() # recover the real key used for encoding

def encrypt(p,key): return ''.join(chr(p(i)) for i in key) # p(x) = 4*x*x + 3*x + 7 # transform was just identity

np.poly1d([4,3,7])
poly = np.poly1d([4,3,7])
assert encrypt(poly, key) == open("key.txt","rb").read().decode("utf-8")

from Crypto.Cipher import AES
cipher = AES.new(key, AES.MODE_ECB)
print(cipher.decrypt(flag))

# output: b'VishwaCTF{s33_1_t0ld_y0u_1t_w45_345y}\x0b\x0b\x0b\x0b\x0b\x0b\x0b\x0b\x0b\x0b\x0b'
```

# Flag: `VishwaCTF{s33_1_t0ld_y0u_1t_w45_345y}`

