# 用指针检查一个字符串是否是 C 中的回文

> 原文:[https://www . geesforgeks . org/check-if-a-string-is-回文-in-c-use-pointers/](https://www.geeksforgeeks.org/check-if-a-string-is-palindrome-in-c-using-pointers/)

给定一个字符串。任务是检查字符串是否是回文或者没有使用指针。不允许使用任何内置的字符串函数。

如果一个字符串的反串与原字符串相同，则称该字符串为回文。例如，“夫人”是回文，因为当字符串反转时，实现了相同的字符串，但“夫人”不是回文。

```
Input: str = "Madam"
Output: String is not a Palindrome.

Input: str = "madam"
Output: String is Palindrome.

Input: str = "radar"
Output: String is Palindrome.

```

**算法**:

1.  取两个指针，说 **ptr** 和 **rev** 。
2.  将 **ptr** 初始化为字符串的基址，并将其向前移动以指向字符串的最后一个字符。
3.  现在，将 **rev** 初始化为字符串的基址，并同时向前移动 rev 和向后移动 **ptr** ，直到到达字符串的中间。
4.  如果 ptr 和 rev 所指向的字符在任何时候都不匹配，那么从循环中断开。
5.  检查 ptr 和 rev 是否交叉，即 **rev > ptr** 。如果是，那么字符串是回文，否则不是。

下面是上述方法的实现:

```
// C program to check if a string is palindrome
// using pointers

#include <stdio.h>

// Function to check if the string is palindrome
// using pointers
void isPalindrome(char* string)
{
    char *ptr, *rev;

    ptr = string;

    while (*ptr != '\0') {
        ++ptr;
    }
    --ptr;

    for (rev = string; ptr >= rev;) {
        if (*ptr == *rev) {
            --ptr;
            rev++;
        }
        else
            break;
    }

    if (rev > ptr)
        printf("String is Palindrome");
    else
        printf("String is not a Palindrome");
}

// Driver code
int main()
{
    char str[1000] = "madam";

    isPalindrome(str);

    return 0;
}
```

**Output:**

```
String is Palindrome

```