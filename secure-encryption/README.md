# secure-encryption

Category: Cryptography

We connect to the server using netcat.

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/secure-encryption/first.png?raw=true"
</p>

You just have to figure it out that this is a base86 encryption. We will use pwn tools to solve this challenge.

The script that I used:

```
from pwn import *
import base64

r = remote("34.89.152.36", 30725)

def func():
	r.recvuntil(b"ENC= b'")
	enc=r.recvuntil(b"'", drop=True)
	dec = base64.b85decode(enc)
	print(dec)
	r.sendlineafter(b"Value: ", dec)

for i in range(0, 20):
	func()

r.interactive()
```

First time I used a while True loop and I saw that after the 20th iteration I have an error, that means that I reach a wrong value in my variable.
Then I updated my code with a for loop and added the `r.interactive()` function to get the final output.

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/secure-encryption/second.png?raw=true"
</p>
