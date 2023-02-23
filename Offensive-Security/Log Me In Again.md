# Log Me In Again

### Category: Web
__________________________

![Alt text](Images/Log%20Me%20In%20Again%201.png)

By saying that attackers should "pull an Equifax" the prompt suggests I obtain information by enumerating the database. This will likely require a blind SQL injection. In theory, I could have created a program that automated this attack. I've written such a script before and it's fairly tedious. Instead, I used sqlmap to facilitate my attack and enumerate the system. In powershell I entered the following: 

~~~
sqlmap -u http://offsec-chalbroker.osiris.cyber.nyu.edu:1241/login.php? 
--cookie="CHALBROKER_USER_ID=elh313; PHPSESSID=mtsg9d8bnlrc96puj2ga4kuco2" --forms 
--dbs --dbms=mysql --dump --tamper=space2comment --random-agent
~~~

| Options      | Reasoning/Description |
| -----------  | ----------- |
| cookie       | The cookies my web browser used       |
| forms       | Find and probe the form on the page|
| dbs    | Enumerate the database        |
| dump    | Dump the database table entries        |
| dbms       | Save time in future scan attempts, mysql is in use and it is known   |
| tamper=space2comment    | Bypass fiters by altering input|
| random-agent   | Bypass WAFS        |


Finally, I found the flag in the secrets table of the logmein database.

>To build it by hand I’d use the sleep function of MySQL as an indicator of if a query was true. I would explore the structure of the database by checking one character of a word at a time. If the nth letter in a string equals the character presented, the search would sleep for a set amount of time before the response could be given. If the response was delayed I’d know that that letter is the character in use, otherwise I’d check the next character. If no characters matched, I’d move to the next string. To speed up the comparisons I could also use a binary search that starts by comparing the value of the nth character to the median value of all visable ascii characters.

![Alt text](Images/Log%20Me%20In%20Again.png)
