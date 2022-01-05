# 运行时设置 C 中无符号字符数组的值

> 原文:[https://www . geesforgeks . org/set-value-of-unsigned-char-array-in-c-in-runtime/](https://www.geeksforgeeks.org/set-value-of-unsigned-char-array-in-c-during-runtime/)

本文解释了如何在 c 语言运行时设置或更改无符号字符数组的值

**给定:**
假设我们有一个大小为 n 的无符号字符数组

```
unsigned char arr[n] = {};

// currently arr = {'', '', '', ...}

```

**要做的事:**
我们想在运行时设置或更改这个数组的值。

例如，我们想要制作数组

```
arr = {'1', '2', '3', ...}

```

**解决方案:**
这个可以借助 [memcpy()方法](https://www.geeksforgeeks.org/memcpy-in-cc/)来实现。 [memcpy()](https://www.geeksforgeeks.org/memcpy-in-cc/) 用于将一个内存块从一个位置复制到另一个位置。在[字符串中声明](https://www.geeksforgeeks.org/commonly-used-string-functions-in-c-c-with-examples/)

**语法:**

```
// Copies "numBytes" bytes from address "from" to address "to"
void * memcpy(void *to, const void *from, size_t numBytes);

```

以下是上述方案的实施情况:

```
// C program to set the value
// of unsigned char array during runtime

#include <stdio.h>
#include <string.h>

int main()
{

    // Initial unsigned char array
    unsigned char arr[3] = { 0 };

    // Print the initial array
    printf("Initial unsigned char array:\n");
    for (size_t i = 0; i < sizeof(arr) / sizeof(arr[0]); i++) {
        printf("%c ", arr[i]);
    }
    printf("\n");

    // Using memcpy() to change the values
    // during runtime
    memcpy(arr,
           (unsigned char[]){ '1', '2', '3' },
           sizeof arr);

    // Print the updated array
    printf("Updated unsigned char array:\n");
    for (size_t i = 0; i < sizeof(arr) / sizeof(arr[0]); i++) {
        printf("%c ", arr[i]);
    }

    printf("\n");
    return 0;
}
```