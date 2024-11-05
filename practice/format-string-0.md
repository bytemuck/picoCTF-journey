# format-string-0
picoCTF Link: [https://play.picoctf.org/practice/challenge/433](https://play.picoctf.org/practice/challenge/433)

## About

```
Description:
Can you use your knowledge of format strings to make the customers happy?

Hints:
1. This is an introduction of format string vulnerabilities. Look up "format specifiers" if you have never seen them before.
2. Just try out the different options
```

## Solution

This challenge is only to get familiar with the string formats.

The first question expect an answer where the length of the string chosen is two times longer than the size of the input buffer.
```c
int count = printf(choice1);
if (count > 2 * BUFSIZE) {
    serve_bob();
} else {
    printf("%s\n%s\n",
            "Patrick is still hungry!",
            "Try to serve him something of larger size!");
    fflush(stdout);
}
```

Since `%114d` in this case is used to pad nothing with 114 whitespaces, it adds 114 character for a total of 123 characters, which is way more than 2 * 32.

```
Welcome to our newly-opened burger place Pico 'n Patty! Can you help the picky customers find their favorite burger?
Here comes the first customer Patrick who wants a giant bite.
Please choose from the following burgers: Breakf@st_Burger, Gr%114d_Cheese, Bac0n_D3luxe
Enter your recommendation: Gr%114d_Cheese
```

Then, we want to read from the stack many times (until we print the flag), and the options that do that is the `Cla%sic_Che%s%steak` option.

```
Sponge Bob wants something outrageous that would break the shop (better be served quick before the shop owner kicks you out!)
Please choose from the following burgers: Pe%to_Portobello, $outhwest_Burger, Cla%sic_Che%s%steak
Enter your recommendation: Cla%sic_Che%s%steak
```

## Answer

```
Enter your recommendation: Gr%114d_Cheese
Enter your recommendation: Cla%sic_Che%s%steak
```