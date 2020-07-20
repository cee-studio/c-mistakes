# Wrong order when calling `strcpy()` function

```c
#include <stdio.h>
#include <string.h>

int main (int argc, char ** argv)
{
    char dest[20];
    char src[5];
    strcpy(src, "test"); // correct
    strcpy(src, dest);   // wrong
    return 0;
}
```

```
  Memory access error: reading from the outside of a memory block; abort!
  # Reading 29 bytes from 0xffe41f4c will read undefined values.
  #
  # The memory-block-to-be-read (start:0xffe41f4c, size:20 bytes) is bound to 'dest' at
  #    file:/prog.c::6, 10
  #
  #  0xffe41f4c           0xffe41f5f
  #  +--------------------------+
  #  | memory-block-to-be-read  |......
  #  +--------------------------+
  #  ^~~~~~~~~~
  #  the read starts at the memory block begin.
  #
  # Stack trace (most recent call first) of the read.
  # [0]  file:/musl-1.1.10/src/string/strlen.c::91, 3
  # [1]  file:/musl-1.1.10/src/string/stpcpy.c::15, 16
  # [2]  file:/musl-1.1.10/src/string/strcpy.c::17, 2
  # [3]  file:/prog.c::9, 5
  # [4]  [libc-start-main]
Segmentation fault
```

[Demo](https://cee.studio/?bucket=200720-RDs&name=Wrong_order_strcpy)
