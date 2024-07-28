# Knowledge check ***with metasploit***

Enumeration is the key, so nmap result:

![nmap](https://github.com/user-attachments/assets/bc1d0d68-1344-42ba-b2b6-3efd9e3e3af8)

Immediately, went to website; website build with GetSimple version 3.3.15 (which vulnerable) and tried to find directories with `gobuster`:

![gobuster](https://github.com/user-attachments/assets/8a0e2700-3e52-4049-b5b6-e77ba5b1476d)

Admin page was using default credentials (admin:admin)

![admin-login-page](https://github.com/user-attachments/assets/2edde83a-685d-4003-a7c6-c0e1fda76296)

(searched the vulnerable version of website in metasploit) I got a shell with meterpreter:

![meterpreter-shell](https://github.com/user-attachments/assets/55c276c3-f390-4e1c-a0b8-2a416bdb3d38)

And in /home folder there is what we need:

![user-txt](https://github.com/user-attachments/assets/9efe3bdb-bd08-47ab-9f32-d302934b476a)

If we type the `shell`  and `sudo -l`:

![sudo-l](https://github.com/user-attachments/assets/c493e240-7f69-41fd-99f6-c094bfa3b421)

After that, we need to escelate the priveleges (I have used GtfoBins)

![gtfo-bins](https://github.com/user-attachments/assets/b94f9cdf-643a-499d-ac7b-b72c6a8f0c95)

Again, typing `shell` and above commands give us root:

![root](https://github.com/user-attachments/assets/02d8873e-55b1-4a4f-98cf-12bad6df649d)

![root-txt](https://github.com/user-attachments/assets/260139f3-061d-4f7d-ae75-61f6bb06776d)







