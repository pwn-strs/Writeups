# Happy Valentine's Day 

We were given the following source files `source.txt`  and `enc.txt`

```py
# source.txt

from PIL import Image
from itertools import cycle

def xor(a, b):
    return [i^j for i, j in zip(a, cycle(b))]

f = open("original.png", "rb").read()
key = [f[0], f[1], f[2], f[3], f[4], f[5], f[6], f[7]]

enc = bytearray(xor(f,key))

open('enc.txt', 'wb').write(enc)
```

As we can see the `original.png` file was xored with its first 8 bytes.

To decode  it, we need to know its original first 8 bytes.
As it turns out, PNG file format's [magic bytes](https://en.wikipedia.org/wiki/File_format#Magic_number)  is of 8 bytes, in particular

`89 50 4e 47 0d 0a 1a 0a` in hex.

Simply xoring `enc.txt` with these 8 bytes recovers `original.png`.

Solve script
---

```py
# solve.py

from itertools import cycle

def xor(a, b): return [i^j for i, j in zip(a, cycle(b))]

f = open("enc.txt","rb").read()

key = bytes.fromhex('89504e470d0a1a0a')

decode = bytearray(xor(f,key))

open('original.png', 'wb').write(decode)

# Flag: VishwaCTF{h3ad3r5_f0r_w1nn3r5}
```


![Original.png ](files/crypto_original.png) 

## FLAG: VishwaCTF{h3ad3r5_f0r_w1nn3r5}
