- Enum4linux is a tool for enumerating information from Windows and Samba systems.

`enum4linux -a 10.10.126.168 | tee enum4linux.log`

- I have used 'ssh2john script' which I have never used it before. ssh2john is a utility to convert the key-file into a txt-format that would be suitable for JtR to crack by comparing hashes

`./ssh2john 'file_path_of_privkey' >   'hash.txt'`  based on that I find the passphrase (`cd /usr/share/wordlists/john`)

- `steghide` and `stegseek` -> learn about them

-  migrate in meterpreter -> Moves your meterpreter shell to another running process. 
