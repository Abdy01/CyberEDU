# secure-terminal

Category: Misc

We connect to the server using netcat.

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/secure-terminal/first.png?raw=true"
</p>

We have some options here. The first one will give us information about the ticket system:

```
We do not execute commands before you ask us to.
Our system works based on 'tickets', which contain signed commands.
While the free version can only generate 'whoami' tickets, the pro version can create any ticket.
Each ticket is a JSON object containing two fields: the command that you want to execute and a signature.
The signature is calculated as follows: md5(SECRET + b'$' + base64.b64decode(command)), where SECRET is a 64-character random hex string only known by the server.
This means that the PRO version of the software can generate tickets offline.
The PRO version also comes with multiple-commands tickets (the FREE version only executes the last command of your ticket).
The PRO version also has a more advanced anti-multi-command-ticket detection system - the free version just uses ; as a delimiter!
What are you waiting for? The PRO version is just better.
```

The second one is a ticket example:

```
You can find your ticket below.
{"command": "d2hvYW1p", "signature": "f2c1fe816530a1c295cc927260ac8fba"}
```

And the third one is our ticket that need to be execute.

We can use just `whoami` command. If we try others, the program will not let us do it.
This command: `d2hvYW1p` is `whoami` in base64.
`md5(SECRET + b'$' + base64.b64decode(command))` from the formula of the ticket, we do not know the `SECRET`. What we can do is an Length Extension Attack.

From Wikipedia we can find that "A length extension attack is a type of attack where an attacker can use Hash(message1) and the length of message1 to calculate Hash(message1 || message2) for an attacker-controlled message2, without needing to know the content of message1".
We can do this with a tool named `hashpump`.

The command will be `hashpump -s f2c1fe816530a1c295cc927260ac8fba -d whoami -a ";cat flag.txt" -k 65`
Signature that we got; Data which is accepted `whoami`; Data to add is our next command; And the length 64 + `$` which is 65; 

We will get this:
```
8a50f5de19ae13faf9ba47b9595276e0
whoami\x80\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x008\x02\x00\x00\x00\x00\x00\x00;cat flag.txt
```
The first one is the new signature and the second one is our command that needs to be encrypted in base64.

We will encrypt using this command: echo -ne "whoami\x80\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x008\x02\x00\x00\x00\x00\x00\x00;cat flag.txt" | base64 -w 0

The output:
d2hvYW1pgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADgCAAAAAAAAO2NhdCBmbGFnLnR4dA==

Now we have to make the ticket and to send it.

The ticket:
`{"command":"d2hvYW1pgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADgCAAAAAAAAO2NhdCBmbGFnLnR4dA==", "signature": "8a50f5de19ae13faf9ba47b9595276e0"}`

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/secure-terminal/second.png?raw=true"
</p>

