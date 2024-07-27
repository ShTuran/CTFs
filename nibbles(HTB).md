# Nibbles

# Reported by : Shirinov Turan

The first step, in almost every pentest or CTF is information gathering (get as much information as possible):

Let's start our nmap scan (I have put only one ss - do nmap as much as needed):

![initial_nmap](https://github.com/user-attachments/assets/9bb9f87f-f5cf-4e76-b431-8d73f0249873)

After that we need to find any vulnerabilities regarding to open ports; 

Website looks so:

![website](https://github.com/user-attachments/assets/b1cfd3a7-21ef-44bc-8a42-a7c7936f51a9)

After looking the source-code:

![source-code-of-website](https://github.com/user-attachments/assets/2a0e04f8-38f2-4f65-96ab-4584a0953e63)

Let's enumerate the website:

![gobuster(ip0)](https://github.com/user-attachments/assets/58490e17-b937-48ab-9de2-472066999869)

And also /nibbleblog itself:

![gobuster(ip-nibbleblog)](https://github.com/user-attachments/assets/a9ad7c6b-e83d-4c43-be7e-a53013c931b4)

Quick search showed that nibbleblog has some vulnerability:

![file-upload-vuln-4 0 3](https://github.com/user-attachments/assets/28de7926-5020-465c-b237-cf83628608f8)

Let's confirm our nibbleblog version:

![confirmed-the-version(v4 0 3)](https://github.com/user-attachments/assets/043cd584-c94d-462f-869c-7d1b05316c6e)

They both match.

I have searched `searchsploit` as well..

And wanted to find a PoC:

![poc-of-nibbles](https://github.com/user-attachments/assets/97acf9f9-f427-451a-8bb7-b58468ad4d27)

Let's do the same.

Let's go to /admin page:

![admin php(file)](https://github.com/user-attachments/assets/57d0c8f5-85f9-4f1c-9da7-24cc7c85c94e)

I have brute forced the credentials, but failed even get blocked; default credentials and some easy password did not work - however,  'admin' 'nibbles' is the password.

And here we uploaded our exploit in plugin (as described in PoC)

and opened a listener:

After we are in, went to

![content-folder](https://github.com/user-attachments/assets/c81fbf4c-3836-4f93-b73e-cb845bb82ee8)

to hit the 'POINT' to get a shell

![getting-a-shell](https://github.com/user-attachments/assets/aebc265b-62a4-4846-a325-c0dd6b90bea4)

We just need to upgrade the shell:

![upgrade-the-shell](https://github.com/user-attachments/assets/b9f02de8-150a-482f-9716-b37de4939a4c)

And get our first (user) flag:

![user-txt](https://github.com/user-attachments/assets/6c6f3459-b588-4095-8371-c2434739ac5d)

All we need to escelate the privileges; for that we can use any known script; and download the script to machine; (open the python server on attacker machine and wget the necessary script):

![LinEnum](https://github.com/user-attachments/assets/8e18fb34-f673-417e-a393-baa6b111b5b6)

Here, we get the interesting information.

We just added one line code to the end of it and run as sudo (also, do not forget to open a listener, since it will give us root access.)

![root](https://github.com/user-attachments/assets/aed13925-d82d-44e6-8e15-c0468a89319e)

![root-txt](https://github.com/user-attachments/assets/7c70579a-0022-47c2-a817-6004e055276f)










































