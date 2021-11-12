# bork-sauls

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/bork-sauls/first.png?raw=true"
</p>

For this challenge you have the option to hit the dancer to descrease his life or to throw with a flask in him.
Maybe you think that life has to reach 0 to win, right? In the way the program was created, not really...

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/bork-sauls/second.png?raw=true"
</p>

Using Ghidra to reverse the code, you can see a vulnerability of buffer overflow in local_c variable.

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/bork-sauls/third.png?raw=true"
</p>

We can make a little script using pwn library that will increase the dancer's life until the maximum value.

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/bork-sauls/fourth.png?raw=true"
</p>