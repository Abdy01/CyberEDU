# overflowie

Category: PWN

Running the exe file locally we will get this:

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/overflowie/first.png?raw=true"
</p>

Use Ghidra to reverse the file and to understand the source code.
We will find a `verySecureFunction` function:

<p align="left">
  <img src="https://github.com/Abdy01/CyberEDU/blob/main/overflowie/second.png?raw=true"
</p>

What we can see here is that the next variable after our input should be equal with `l33t`. We can overflow this by our input because
our variable has the length of 76.

We can say something like:

```
python3 -c 'print("A"*76 + "l33t")'
```
