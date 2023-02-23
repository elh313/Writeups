# Ping Me

### Category: Web
__________________________

This one was a lot of fun. I started by examining the index.php file used by the server. According to the code, when setting the ip, any spaces in the input will throw an error, single quotes will be replaced with \\’, and if debug is on the command being run will echo out along with the result of the command.

> Note, the two slashes would appear to be one on output because the first is used as an escape character.

To bypass the character restriction on spaces, I used ${IFS} wherever I would use a space. IFS is the internal field separator, and, by default, it is equal to a space. 

To bypass the character restriction against the single quote, I included a backslash before any single quote. Although this may seem counter-intuitive, the end command would have two back slashes. Like in the original code \\’ indicates that the first backslash is to be used as an escape character for the second, and the single quote will be treated as standard code. 

Additionally, I noted that ; can be used in the command line to indicate multiple commands and that my input would need to escape the single quotes to its left and right. With this information, I used burp to test my theory and sent the following GET request. 

My theory was correct. I ran an echo command though shell_exec! I replaced ‘echo’ with ‘cat’ (and turned off debug as I no longer needed it) and retrieved the flag.