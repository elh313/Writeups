# Log Me In

### Category: Web
__________________________


I approached this as a simple sqli injection (and it was!). 
I sent a potentially valid (but incorrect) request by submitting `hello@gmail.com` as the email with a random password. I intercepted the request with burp and sent it to the repeater. Using burp allowed me to bypass the simple character requirements the form had in place. 

I wanted the query to access the ‘admin’ account and ignore the password completely. In the repeater, I changed the email payload to 
~~~
admin’ -- 
~~~

![Alt text](Images/Log%20Me%20In.png)

I included a  ‘ after admin because I knew that the query would likely put the user input in quotes. By ending the quotation early, the -- acted as a command and commented the rest of the search out. 

It worked!
![Alt text](Images/Log%20Me%20In%201.png)
