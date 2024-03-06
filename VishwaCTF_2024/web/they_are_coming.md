# They Are Coming

The repeated use of word robot, lead me straight to /robots.txt

`/robots.txt`
```
# https://www.robotstxt.org/robotstxt.html
User-agent: *
Disallow: /admin
L3NlY3JldC1sb2NhdGlvbg==
Decryption key: th1s_1s_n0t_t5e_f1a9
```

`L3NlY3JldC1sb2NhdGlvbg==` when decoded as base64 gives `/secret-location`

`/secret-location` has a value in local storage
```
Flag: Gkul0oJKhNZ1E8nxwnMY8Ljn1KNEW9G9l+w243EQt0M4si+fhPQdxoaKkHVTGjmA
```
The website had many hints that encryption is AES-128, however key was 20 bytes long. Just taking first 16 bytes of the key worked and gave the flag

# Flag: `VishwaCTF{g0_Su88m1t_1t_Qu14kl7}`