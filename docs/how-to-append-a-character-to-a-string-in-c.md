# 如何在 C 语言中给字符串添加字符

> 原文:[https://www . geesforgeks . org/如何将字符追加到 c 字符串中/](https://www.geeksforgeeks.org/how-to-append-a-character-to-a-string-in-c/)

给定一个字符串 **str** 和一个字符 **ch** ，本文讲述如何在末尾将这个字符 **ch** 追加到这个字符串 **str** 中。
**举例:**

```
Input: str = "Geek", ch = 's'
Output: "Geeks"

Input: str = "skee", ch = 'G'
Output: "skeeG"
```

**接近** :

1.  获取字符串**字符串**和字符 **ch**
2.  使用 [strncat()函数](https://www.geeksforgeeks.org/strncat-function-in-c-cpp/)在字符串末尾追加字符 ch。strncat()是用于字符串处理的预定义函数。 **string.h** 是字符串函数需要的头文件。
    **语法:**

```
char *strncat(char *dest, const char *src, size_t n)
```

**参数:**该方法接受以下参数:

*   **dest:** 我们要追加的字符串。
*   **src:** 要追加“n”个字符的字符串。
*   **n:** 表示要追加的最大字符数。size_t 是无符号整数类型。

3.打印或返回附加的字符串。

以下是上述方法的实现:

## C

```
// C program to Append a Character to a String

#include <stdio.h>
#include <string.h>

int main()
{
    // declare and initialize string
    char str[6] = "Geek";

    // declare and initialize char
    char ch = 's';

    // print string
    printf("Original String: %s\n", str);
    printf("Character to be appended: %c\n", ch);

    // append ch to str
    strncat(str, &ch, 1);

    // print string
    printf("Appended String: %s\n", str);

    return 0;
}
```

**Output:** 

```
Original String: Geek
Character to be appended: s
Appended String: Geeks
```