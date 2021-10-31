# baby-pwn

Category: PWN

Running the exe file locally you will get this:

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/baby-pwn/first.png?raw=true"
</p>

Use Ghidra to reverse the file and to understand the source code.
You will find a `vuln` function that looks like this:

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/baby-pwn/second.png?raw=true"
</p>

Your input is the first variable which has the maximum length of 48, then your input will pass the next variable.
The next variable is used in the `system(local_38);` where will be recognized like a shell command.

The solution is to input something over 48 characters and then to use commands to get the flag.

Hint: If you are stuck by commands, try to call a shell