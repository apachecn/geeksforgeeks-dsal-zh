# C

中的 sprintf()

> 原文:[https://www.geeksforgeeks.org/sprintf-in-c/](https://www.geeksforgeeks.org/sprintf-in-c/)

**语法:**

```
int sprintf(char *str, const char *string,...); 

```

**返回:**

```
If successful,
it returns the total number of 
characters written excluding 
null-character appended in the string, 
in case of failure a negative number 
is returned .

```

sprintf 代表“字符串打印”。它不是在控制台上打印，而是将输出存储在 sprintf 中指定的字符缓冲区中。

## C

```
// Example program to demonstrate sprintf()
#include <stdio.h>
int main()
{
    char buffer[50];
    int a = 10, b = 20, c;
    c = a + b;
    sprintf(buffer, "Sum of %d and %d is %d", a, b, c);

    // The string "sum of 10 and 20 is 30" is stored
    // into buffer instead of printing on stdout
    printf("%s", buffer);

    return 0;
}
```

**Output**

```
Sum of 10 and 20 is 30
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。