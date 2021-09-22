# why-xor

Category: Cryptography

```python
xored = ['\x00', '\x00', '\x00', '\x18', 'C', '_', '\x05', 'E', 'V', 'T', 'F', 'U', 'R', 'B', '_', 'U', 'G', '_', 'V', 
'\x17', 'V', 'S', '@', '\x03', '[', 'C', '\x02', '\x07', 'C', 'Q', 'S', 'M', '\x02', 'P', 'M', '_', 'S', 
'\x12', 'V', '\x07', 'B', 'V', 'Q', '\x15', 'S', 'T', '\x11', '_', '\x05', 'A', 'P', '\x02', '\x17', 'R', 'Q', 'L', '\x04', 
'P', 'E', 'W', 'P', 'L', '\x04', '\x07', '\x15', 'T', 'V', 'L', '\x1b']
s1 = ""
s2 = ""
# ['\x00', '\x00', '\x00'] at start of xored is the best hint you get
a_list = [chr(ord(a) ^ ord(b)) for a,b in zip(s1, s2)]
print(a_list)
print("".join(a_list))
```

It looks like we have a `xored` string which could contain the flag.
If we check what is happening in `a_list`:
- ord(a) - returns the decimal value of `a` in ASCII table
- chr(65) - returns the symbol you can find at `65` decimal value
- ^ - xor operation
- zip(s1, s2) - will pair the first letter from s1 with the first one from s2

From xor's properties we know that a^b=c and a^c=b. The first hint tells us about the start of the string.
We have \x00 \x00 \x00 at the beginning and we know that the flag must start with ctf.
If we xor the fourth character, `\x18`, with `c` you will get `{`. 

So, the solution is to xor the entire `xored` string using the same formula from `a_list`, with `ctf * (len(xored)/3)`