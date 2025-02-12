## SSH2JOHN (looks for passphrase)

```
ssh2joh  id_rsa > give2john.txt

john give2john --wordlist=/usr/share/wordlists/rockyou.txt
```

![[Pasted image 20250120011210.png]]


ssh -i id_rsa username@ip

ssh -l username ip 