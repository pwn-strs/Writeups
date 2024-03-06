# We are Valorant

> We just got lucky in this chall

We were provided 2 files - `we_are_valorant.jpg` and `Astra_!!.mp4`

The jpeg image file had a corrupted signature (hint was there in description as well). After fixing the file I got the following image

![fixed image](files/we_are_valorant_fixed.jpg)

`stegseek --seed we_are_valorant_fixed.jpg` showed that there was data hidden by steghide. However rockyou.txt wordlist did not work. That's when I put it on AperiSolve to see if there were any previously used passwords and the password `Tenz` worked. Using steghide got `not_a_secret.txt` file which had the flag.

# Flag: `VishwaCTF{you_are_invited_to_the_biggest_valorant_event}`
