# Mysterious Old Case

Provided with `final.mp3`

The music had an audio which seemed to be some one speaking in reverse, so after reversing the audio, I got a message with important facts:

```
1. The was flight log data
2. Something to do with fibonacci series
3. Password was the airline which DB Cooper hijacked - google search revealed Northwest Orient Airlines
```

On running exiftool on the original mp3, I got the [drive link](https://drive.google.com/file/d/1bkuZRLKOGWB7tLNBseWL34BoyI379QbF/view?usp=drive_lin) and the hint that password was in lowercase

I quickly extracted the zip file and saw many logs. Used grep to find the flight of the date DB Cooper hijacked the flight. It was in `Flight-305.log`. I immediately noticed letters V and i in 2nd and 3rd place and knew flag letters were in positions of numbers in fibonacci series. Wrote the following script to get the flag

```python
with open('flight_logs/Flight-305.log') as f:
    data = f.read()

arr = data.split("\n")

a = 2
b = 3

for i in range(len(arr)):
    if(i == a-1):
        print(arr[i], end = "")
        a = a + b
    elif(i == b-1):
        print(arr[i], end = "")
        b = a + b

print()
```

NOTE: Found a red herring image by doing binwalk on which I wasted quite some time

# Flag: `VishwaCTF{1_W!LL_3E_B@CK}`
