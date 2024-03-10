# MetaFile 

A memory analysis chall that required some observation

```bash
$ vol -f dump_4.raw windows.filescan | grep Desktop
...
0x8989a4549900	\Users\josh\Desktop\bWV0YXZlcnNlb2ZtYWRuZXNz.rar
...
```

```bash
$ vol -f dump_4.raw windows.filescan | grep josh
...
0x8989a454d2d0	\Users\josh\Music\song.txt
...
```

I ran John on the rar file for 4 hours with no result

song.txt
```
Never Gonna Give You Up


We're no strangers to love
You know the rules and so do I (do I)
A full commitment's what I'm thinking of
You wouldn't get this from any other guy
I just wanna tell you how I'm feeling
Gotta make you understand
Never gonna give you up
Never gonna let you down
Never gonna run around and desert you
Never gonna make you cry
Never gonna say goodbye
Never gonna tell a lie and hurt you
We've known each other for so long
The flag is an image present on
Your heart's been aching, but you're too shy to say it (say it)
Inside, we both know what's been going on (going on)
We know the game and we're gonna play it
And if you ask me how I'm feeling
Don't tell me you're too blind to see
Never gonna give you up
Never gonna let you down
Never gonna run around and desert you
Never gonna make you cry
Never gonna say goodbye
Never gonna tell a lie and hurt you
Never gonna give you up
Never gonna let you down
Never gonna run around and desert you
Never gonna make you cry
Never gonna say goodbye
Never gonna tell a lie and hurt you
We've known each other for so long
Your heart's been aching, but you're too shy to say it (to say it)
Inside, we both know what's been going on (going on)
desktop in front of your eyes
We know the game and we're gonna play it
I just wanna tell you how I'm feeling
Gotta make you understand
Never gonna give you up
Never gonna let you down
Never gonna run around and desert you
Never gonna make you cry
Never gonna say goodbye
Never gonna tell a lie and hurt you
Never gonna give you up
Never gonna let you down
Never gonna run around and desert you
Never gonna make you cry
But environment is not letting you see it...
Never gonna say goodbye
Never gonna tell a lie and hurt you
Never gonna give you up
Never gonna let you down
Never gonna run around and desert you
Never gonna make you cry
Never gonna say goodbye
Never gonna tell a lie and hurt you
```

Thought was just a rickroll, but the three dots in `But environment is not letting you see it...` caught my eye

This line is not part of the lyrics. I got the hint to look for environment variables

```bash
$ vol -f dump_4.raw windows.envars
...
2852	notepad.exe	0x1e2a0da1ba0	JOHN_MIGHT_NEED	i_gave_up
...
```

Used the password and on the rar and got an image

![image](files/bWV0YXZlcnNlb2ZtYWRuZXNz.jpg)

```bash
$ exiftool bWV0YXZlcnNlb2ZtYWRuZXNz.jpg
...
Comment                         : pearl{3v3ryb0dy_f0rgets_ab0ut_m3tadat4}
...
```

# FLAG: `pearl{3v3ryb0dy_f0rgets_ab0ut_m3tadat4}`