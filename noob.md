# Topic:  Noob

# Subject:   CTF                                           

# Reported by : Shirinov Turan

Nmap results:

 ![nmap](https://github.com/ShTuran/CTFs/assets/111232034/92ea78ee-a686-4fe0-9f2a-fe1bd7f9a4a3)

As we see 3 ports are open  - > 21, 80, 55077: ftp, http and ssh.


Gobuster results and Dirbuster:

 ![gobuster](https://github.com/ShTuran/CTFs/assets/111232034/daa9e16c-5855-4f63-91ce-116bf442e634)


![dirbuster](https://github.com/ShTuran/CTFs/assets/111232034/d4f3b402-1baf-4883-9b4d-dff99ee3e856)


 Which I do not get anything from there.


After that, I run the nikto:

 ![nikto](https://github.com/ShTuran/CTFs/assets/111232034/ea5d8166-35c8-4436-81eb-9e587e7c3920)

Apache seems outdated, but could not go from there. 


I went to website but I could not be able to get much information there neither, default credentials do not worked:

 ![login](https://github.com/ShTuran/CTFs/assets/111232034/ad9e94e5-fe8f-443e-aa72-256e972efaeb)


And went to ssh(55077):

![hydra](https://github.com/ShTuran/CTFs/assets/111232034/62fd2888-6379-4102-94f5-26c57fa3bb36)

And brute-forced but again – got nothing!

Okay, let’s go ftp:

![ftp](https://github.com/ShTuran/CTFs/assets/111232034/46164b05-a50e-4a8a-9858-33a005ec9819)

And “anonymous” login was successful!

There was cred.txt and welcome files which both of them contain the same thing – “Y2hhbXA6cGFzc3dvcmQ=”

It was base64 and when I decoded - champ:password. This might be website login or ssh login credentials.

Immediately, checked in the website and got the succesful  login: 

![website](https://github.com/ShTuran/CTFs/assets/111232034/61fd5bc9-dd38-47e9-bd2d-50c7cfc63614)

But when I clicked the “About Us” it downloaded the files – 2 picture and 1 text file – 

And “file” -> Did you notice the file name? Isn't is interesting?


I used `file` command and `exiftool` to see info about pictures.

And here, I discovered 2 tools for pictures to discover the information: `stegseek` and `steghide`.
 
![stegseek_funny png](https://github.com/ShTuran/CTFs/assets/111232034/a5ce8566-c913-498b-ad64-470b698f8add)

![steghide_funny png](https://github.com/ShTuran/CTFs/assets/111232034/ce0243fc-1b10-4c32-b664-b4b8e186ace1)

In one picture I have got info says that we need something to revolve

In the next. I get the “user.txt” and -> `wtf:this one is a simple one`; which this one looks like a username and password.


We have one place to check it: ssh and Volla! We are rooted successfully!

![root](https://github.com/ShTuran/CTFs/assets/111232034/56a27086-6e7a-41e3-9619-e4f9b34d8aea)

 

