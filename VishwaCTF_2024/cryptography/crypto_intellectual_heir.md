# Intellectual Heir

> We had second blood

Another poorly designed guessy challenge. 

We are given a zip file containing an encryption script and three other files

After finding `pow(msg,e,f)` in the encrypter script and `RIADSH` in the challenge description, it is fairly obvious that it is RSA cryptosystem, with "RIADSH" being RIvest,ADleman,SHamir.

After guessing that the two files contain the two different primes encoded as cos and sin, it was straightforward to decode.

The encoder was converting a string to a concatenation of the ascii values of the constituent characters.

See the attached solve script.

```py
#! /bin/python3

with open("file.txt") as f: encrypted = int(f.read())

e = 0x10001

with open("file1.txt") as cos: res1 = cos.readlines()
with open("file2.txt") as sin: res2 = sin.readlines()

res1 = ['0' if i[0] == '1' else '1' for i in res1]
res2 = ['0' if i[0] == '0' else '1' for i in res2]

n1 = int("".join(res1),2)
n2 = int("".join(res2),2)

n = n1 * n2

phi = n - n1 - n2 + 1

d = pow(e,-1,phi)

c = pow(encrypted, d, n)


s = str(c) 

print(*[chr(int(s[i:i+2])) for i in range(0,len(s),2)],sep='')
# output: Y0U_@R3_T#3_W0RT#Y_OF_3
```
After wrapping the output in the flag format, we get

# Flag: `VishwaCTF{Y0U_@R3_T#3_W0RT#Y_OF_3}`
