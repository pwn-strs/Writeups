# Wifi Broken

Simple chall, just run a bruteforce using aircrack-ng

`aircrack-ng -z findme.cap -w ~/wordlists/rockyou.txt`

```
                           KEY FOUND! [ shenoydx ]


      Master Key     : 65 BB E2 8B 45 5B B1 BE 5D 96 78 82 14 CC 4B A1
                       1A 15 BC 85 B0 BA 31 A7 9C 83 9E 9D 47 D2 3E 32

      Transient Key  : FE 71 C4 60 DD E1 B6 2D 3C E2 04 12 78 18 95 6F
                       62 B2 04 9D D4 35 8B A2 DC 7D 85 AB DF 04 77 F8
                       B9 7B 8F FE 44 CC 98 6C 9C 83 98 80 D5 EC 72 98
                       A7 FC D7 23 9B 87 C8 CD BF CF 62 5A 97 41 DB 4B

      EAPOL HMAC     : 00 65 7D DC 8B 14 31 78 37 A8 10 86 BC 5B 70 08
```

# FLAG: `pearl{shenoydx}`
