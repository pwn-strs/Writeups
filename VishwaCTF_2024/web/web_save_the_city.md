# Save The City

After deploying the challenge instance, we receive an server address and port. After nc, we see the following output:


```sh 
nc $IP $PORT

SSH-2.0-libssh_0.8.1
```

After searching online for vulnerability in the given library, we come across [CVE-2018-10993](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-10993), libssh authentication bypass.


Using the following PoC script, [cve_2018_10993.py](https://gist.github.com/mgeeky/a7271536b1d815acfb8060fd8b65bd5d) we bypass the ssh authentication and connect to the server .

After connecting, we find a file named `location.txt` on the server and on viewing its contents, we we find the location described in the description: `elrow-club-pune`

# Flag: `VishwaCTF{elrow-club-pune}`
