# Vastness of Space

### Category: Forensics
### Point Value: 359
__________________________

![Alt text](Images/vastness%201.png)


The prompt for this challenge was a jpeg file called Empty_Space.jpg. Knowing that this was a forensics challenge, I figured I should begin my examination with the metadata! It’s an obvious place to start, but often the clues we need are right under our noses.
 
My hunch was correct! In the metadata I learned that I will need to eventually use “BBCTF” as a password.
![Alt text](Images/Vastness%202.png)

From there, I ran 
~~~
strings Empty_Space.jpg > new.txt
~~~
to see if any additional unencrypted data was hiding in plain sight.
![Alt text](Images/vastness%2022.png)

 Although the vast majority of the output was encrypted, something caught my attention: right before the output shifts into a small column, there are two nearly identical lines that don’t look random at all. Both begin with &’()*, several numbers, and :CDEFGHIJSTUVWXYZcdefghijstuvwxyz
 
A quick Google showed that often (although not always) these strings are indicative of steganographic tools at play, like steghide. I installed steghide and ran 
~~~
steghide extract -sf Empty_Space.jpg
~~~
![Alt text](Images/vastness%203.png)

A chance to use the password I found! As a result, I extracted a file called somedata.txt

Inside somedata.txt were thousands of rows of two numbers separated by a comma. It was 4 in the morning and I hit a wall. I knew I was close, but what could these numbers mean?
![Alt text](Images/vastness%204.png)
Luckily, my teammate Diana was awake and came to the rescue: coordinates! When plotted (like in python with matplotlib), the coordinates make a QR code!
 

A scan of the QR code gave us the flag! flag{qUiCk_R3sP0nse_c0d3}
 
![Alt text](Images/vastness%205.png)
 






