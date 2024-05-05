# Topic:  Hackmeplease

# Subject:   CTF                                           


# Reported by : Shirinov Turan


Nmap enumeration result:
 
3 ports are open: 80 – 3306 – 33060

![nmap](https://github.com/ShTuran/CTFs/assets/111232034/2040fc84-205c-48b2-b780-eaaf8cc010c6)


After that, I enumerated subdomains with gobuster:

![gobusterthemain](https://github.com/ShTuran/CTFs/assets/111232034/4e84413a-3d58-4a33-8b3c-d0e1b030bc3c)
 

As a first look, I did not check any of them – which is my bad.


I tried to find any vulnerability with nikto:

 ![nikto](https://github.com/ShTuran/CTFs/assets/111232034/0406ea60-eb1e-4574-abff-4b3456be2c55)


Apache/2.4.41 outdated but I could not be able to gp from there.


When I finally visited the website -  and inspected the website I found that there is a /js/main.js path. 
 
I enumerated  192.168.221.129/js, in case I would find some interesting things as well, but I just confirmed.

![dirbuster(js-main js)](https://github.com/ShTuran/CTFs/assets/111232034/cb62aaa4-4cb7-4e09-b2ff-0cd909c43e99)

When I looked that directory:

![seeddms51x](https://github.com/ShTuran/CTFs/assets/111232034/c3a8e82a-c271-4b9a-afe2-9a270dc4f769)


Went  to the mentioned directory and also, tried to search any vulnerabilies regarding to it. 

![followedtheapath-seeddms](https://github.com/ShTuran/CTFs/assets/111232034/b1035e1c-4549-40c2-b577-d467e5f3b5e9)


Here, I found the login page – default creds do not work.
I could not be able to find anything else from there.

When I searched the vulnerability about seeddms – I have seen that there was a RCE but we have to login – so I need to find a way to login and add a some file there.
 
But when I searched the seeddms I found interesting github repo was saying that:

![conf-settingsxml](https://github.com/ShTuran/CTFs/assets/111232034/d173edff-7e71-4adf-ae21-ca6b11b424ca)


I checked it and, result:

 ![dbs-user-pass](https://github.com/ShTuran/CTFs/assets/111232034/d37ad0ab-3347-41f1-bef0-fced0fbb4e70)


We found the password of database. 

Time to check second port.

The username: seeddms and password: seeddms were working.

 ![dbsentered](https://github.com/ShTuran/CTFs/assets/111232034/ac568e5f-d545-48dd-b893-e34bcbbbede5)


After founding the database and tables – we found a user called – saket

![saketpassword](https://github.com/ShTuran/CTFs/assets/111232034/e1a8948a-a0a7-4c76-86f7-bfeca022236c)



Went to  the login page – but that password was not working.



After checking other tables I found the admin hash but cannot crack it!

![adminhash](https://github.com/ShTuran/CTFs/assets/111232034/a4fbf973-2841-4ed7-8720-3715fbce22c7)


That’s why I changed the admin password – to easy and crackable hash algorithm.

![changedadminpassword](https://github.com/ShTuran/CTFs/assets/111232034/e3223689-f24b-4499-9548-e2b046b2bc07)


Admin password now is – “salam12”

Okay, let’s check the login page:

![adminpagelogged](https://github.com/ShTuran/CTFs/assets/111232034/1adecd3e-28dd-436b-b4a3-081f4c91e2b9)


It worked!

------------------------------------------------------------------------------------
Time to exploit – remembered we have to login?!

Let’s follow the instructions in order to exploit it:

 ![instructions](https://github.com/ShTuran/CTFs/assets/111232034/6fcc0b66-024a-4e2b-ae59-8e4cff89816d)

I uploaded php-reverse-shell since there is RCE.  


I did not want to get the result from the browser, so I used the curl:

![following the instruction on exploit](https://github.com/ShTuran/CTFs/assets/111232034/b595cd65-443a-44c3-ba2c-d8e54edf72e1)


And started the listener.


Foothold:

![foothold](https://github.com/ShTuran/CTFs/assets/111232034/9bc466b7-0a8a-4179-9ec5-0273a104591c)

And time to escelate the privileges. I followed my checklist – which one of them, if possible, read /etc/passwd – and I see the ‘saket’ which we know this user password, let’s login with it:

And this user is what we want:

![saketROOT](https://github.com/ShTuran/CTFs/assets/111232034/cd372e82-eb28-40af-803f-a8da7c9a86fb)


