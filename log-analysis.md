# Topic: Log analysis


# Brute-force
According to the file – generated simple script which will give us the IP address of successful and failed.
When we run the script we got result like this:

![image](https://github.com/ShTuran/CTFs/assets/111232034/7858017a-fd59-446e-83ba-1675200b24f8)

 
Let’s get number of different IP address:
 
![image](https://github.com/ShTuran/CTFs/assets/111232034/e2830a48-03ec-4891-a91d-f25d3e9baaba)

Number of POST request:

![image](https://github.com/ShTuran/CTFs/assets/111232034/c4018e78-1def-44a7-a239-1a17a31aad05)

Different User Agents:

![image](https://github.com/ShTuran/CTFs/assets/111232034/06502973-afc3-42ad-bfba-27605b59ab4a)

 
And finally, the most POST requested IP address:

![image](https://github.com/ShTuran/CTFs/assets/111232034/b6286c99-7b30-4ac7-b11f-5d52d349ea6e)

 Recommended action: To block `146.241.73.240`





# Open-redirection
Searching for status code – 301 and 302:

![image](https://github.com/ShTuran/CTFs/assets/111232034/eb3eccd7-6bec-4797-9da7-0400e99bad3a)


Requested URL, and filters out only the URLs containing "http" or "https":

![image](https://github.com/ShTuran/CTFs/assets/111232034/49c238c2-6b02-42b2-a346-8821b06b04a3)

User-Agent string from each log entry and counts the occurrences of each unique User-Agent value:

![image](https://github.com/ShTuran/CTFs/assets/111232034/fc89d026-8b76-4df0-b242-4433306a809b)

 
filters out only the URLs containing query parameters:

 ![image](https://github.com/ShTuran/CTFs/assets/111232034/0abfbf61-8e29-4b97-8696-0d655f242ba4)



# Xmlexternalentity
Let’s analysis the timestamp:

![image](https://github.com/ShTuran/CTFs/assets/111232034/eca2aa76-5bcf-40b8-af90-d74e40d19ca6)

 
Timestamps from the log file and counts the occurrences of each unique timestamp.

"DOCTYPE" and “XML  ” declarations, which are often associated with XXE attacks:

![image](https://github.com/ShTuran/CTFs/assets/111232034/dd14c32f-0c93-44ba-9cc8-c83e26fc76c9)

 Different IP addresses:

![image](https://github.com/ShTuran/CTFs/assets/111232034/5f53c913-7913-4dcc-8162-8a2f705d25ef)



This command extracts the Referer header from the log file and counts the occurrences of each unique Referer value:

![image](https://github.com/ShTuran/CTFs/assets/111232034/e050506a-2981-4eb9-9c6c-0dc8d3f3b0fa)

 
This command filters log entries to show only those with HTTP status codes of 400 or higher:

 ![image](https://github.com/ShTuran/CTFs/assets/111232034/ad103c1a-def1-4595-8c68-3468dc56cef6)




# Directory-traversal
To filter out response codes starting with "4" (client errors) or "5" (server errors) in the Apache access log.

 ![image](https://github.com/ShTuran/CTFs/assets/111232034/dd53911b-db7a-4371-9daf-45069ecb7843)


The most requested IP address:

![image](https://github.com/ShTuran/CTFs/assets/111232034/6c8105bc-6089-4d01-ab54-886015918170)


And most used Directory Traversal command:

![image](https://github.com/ShTuran/CTFs/assets/111232034/4cd9c3ba-cfc2-4b6a-ac38-73321e37daf0)

 

But got nothing😊
