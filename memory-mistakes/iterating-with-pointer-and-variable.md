# Iterating with pointers and variables at the same time

Source: [Problem with a function similar to strcat()](https://stackoverflow.com/q/62827030/10247460)

Novices trying to understand pointers sometimes mix iterating variables with pointers
and variables at the same time.

```c
char *mystrcat(char *str1, char *str2){
    int i = 0;
    char *buffer = str1;
    while(*str1) {
        str1++; i++;
    }
    i++;
    while(*str2) {
        str1[i] = *str2;
        str2++; i++;
    }
    str1[++i] = '\0';
    str1 = buffer;
    return str1;
}
```

```
  Memory access error: writing to the outside of a memory block; abort!
  # Writing 22 bytes to 0x8141d14 will clobber other memory blocks.
  #
  # The memory-block-to-be-written ('qwerty', size:7 bytes) is allocated at
  #    file:/prog.c
  #
  #  0x8141d14           0x8141d1a
  #  +--------------------------+
  #  |memory-block-to-be-written|......
  #  +--------------------------+
  #  ^~~~~~~~~~
  #  the write starts at the memory block begin.
  #
  # Stack trace (most recent call first) of the write.
  # [0]  file:/musl-1.1.10/src/string/stpcpy.c::16, 2
  # [1]  file:/musl-1.1.10/src/string/strcpy.c::17, 2
  # [2]  file:/prog.c::23, 5
  # [3]  [libc-start-main]
```

[Demo](https://cee.studio/?bucket=200720-TmN&name=Iterating_with_ptr_and_var_at_once)
