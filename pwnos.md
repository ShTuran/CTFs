Topic: PWNOS 2.0
Subject: CTF
Reported by : Shirinov Turan
Date: 26.04.2024
Started with `nmap` scan with the following syntax:
`nmap -vv -A -T4 -p- 10.10.10.100`
Open ports –
22 -> ssh OpenSSH 5.8p1 Debian 1ubuntu3 -> OpenSSH < 6.6 SFTP - Command
Execution
80-> http Apache httpd 2.2.17 (Ubuntu) -> Apache Struts 2.0.1 < 2.3.33 / 2.5 <
2.5.10 - Arbitrary Code Execution
Begin with http enum:
After that, I went to web page -> http://10.10.10.100
- Admin email -> admin@isints.com - Dan (from users table)
- Site is PHP based
As a second step, I run nikto to see any vulnerability regarding to
webpage:
I’ve got a lot of information I here.
As a third step I’ve run gobuster to enumerate the directories:
Some of them were obvious, but there are some directories we’ve never seen
before.
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
And adding –dump will gave us what we need, even though I do get the hash of
admin I could not be able to crack it. I also tried to get –os-shell but it was not
successful neither.
And via the sqlmap I read the /etc/passwd:
It means that, I can read the file. The question was can I write as well? Yes. I
uploaded php-reverse shell:
Command was used: sqlmap -u http://10.10.10.100/login.php --
data="email=test&pass=test&submit=Login&submitted=TRUE" --file-write
/home/kali/phprs --file-dest /var/www/rev.php. And visited the .rev.php I do
get reverse shell. At this point, I only need to escelate the priveleges.
And listened on port 1234; got foothold.
After some recon – I found 2 “mysqli_connect.php” which one of them in
the /var directory and one of them in /var/www directory. The one which in
/var directory was containing the root password.
Additional vulnerabilites:
- 10.10.10.100/blog has xss in the `search`.
- Simple PHP Blog 0.4.0 is vulnerable to file upload when I `search PHP
Blog 0.4.0` I got the meterpreter shell but I could not be able to escelate the
priveleges from there.
- This module combines three separate issues within The Simple PHP
Blog (<= 0.4.0) application to upload arbitrary data and thus execute a shell.
The first vulnerability exposes the hash file (password.txt) to
unauthenticated users. The second vulnerability lies within the image upload
system provided to logged-in users; there is no image validation function in
the blogger to prevent an authenticated user from uploading any file type.
The third vulnerability occurs within the blog comment functionality,
allowing arbitrary files to be deleted.
Reference of above text
https://www.rapid7.com/db/modules/exploit/unix/webapp/sphpblog_file_upl
oad/
