# Topic:  Noob

# Subject:   CTF                                           

# Reported by : Shirinov Turan

Nmap results:

 

As we see 3 ports are open  - > 21, 80, 55077: ftp, http and ssh.




Gobuster results and Dirbuster:

  



 


Which I do not get anything from there.


After that, I run the nikto:

 


Apache seems outdated, but could not go from there. 






I went to website but I could not be able to get much information there neither, default credentials do not worked:

 



And went to ssh(55077):

 


And brute-forced but again – got nothing!


Okay, let’s go ftp:

 


And “anonymous” login was successful!

 

There was cred.txt and welcome files which both of them contain the same thing – “Y2hhbXA6cGFzc3dvcmQ=”

It was base64 and when I decoded - champ:password. This might be website login or ssh login credentials.

Immediately, checked in the website and got the succesful  login: 


But when I clicked the “About Us” it downloaded the files – 2 picture and 1 text file – 


          

And “file” -> Did you notice the file name? Isn't is interesting?


I used `file` command and `exiftool` to see info about pictures.

And here, I discovered 2 tools for pictures to discover the information: `stegseek` and `steghide`.
 

In one picture I have got info says that we need something to revolve


 

In the next. I get the “user.txt” and -> `wtf:this one is a simple one`; which this one looks like a username and password.



We have one place to check it: ssh and Volla! We are rooted successfully!


 

