# atoi()的递归实现

> 原文:[https://www . geeksforgeeks . org/recursive-implementation-of-atoi/](https://www.geeksforgeeks.org/recursive-implementation-of-atoi/)

[atoi()](http://www.cplusplus.com/reference/cstdlib/atoi/) 函数以一个字符串(代表一个整数)为参数，返回其值。

我们已经讨论了 atoi() 的[迭代实现。如何递归计算？
**我们强烈建议你最小化浏览器，先自己试试这个**
想法是分离最后一位数字，递归计算剩余 n-1 位数字的结果，将结果乘以 10，将得到的值加到最后一位数字上。
下面是想法的实现。](https://www.geeksforgeeks.org/write-your-own-atoi/) 

## C++

```
// Recursive C program to compute atoi()
#include <stdio.h>
#include <string.h>

// Recursive function to compute atoi()
int myAtoiRecursive(char *str, int n)
{
    // Base case (Only one digit)
    if (n == 1)
        return *str - '0';

    // If more than 1 digits, recur for (n-1), multiply result with 10
    // and add last digit
    return (10 * myAtoiRecursive(str, n - 1) + str[n-1] - '0');
}

// Driver Program
int main(void)
{
    char str[] = "112";
    int n = strlen(str);
    printf("%d", myAtoiRecursive(str, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to compute atoi()
class GFG{

// Recursive function to compute atoi()
static int myAtoiRecursive(String str, int n)
{

    // Base case (Only one digit)
    if (n == 1)
    {
        return str.charAt(0) - '0';
    }

    // If more than 1 digits, recur for (n-1),
    // multiply result with 10 and add last digit
    return (10 * myAtoiRecursive(str, n - 1) +
                      str.charAt(n - 1) - '0');
}

// Driver code
public static void main(String[] s)
{
    String str = "112";
    int n = str.length();

    System.out.println(myAtoiRecursive(str, n));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to compute atoi()

# Recursive function to compute atoi()
def myAtoiRecursive(string, num):

    # base case, we've hit the end of the string,
    # we just return the last value
    if len(string) == 1:
        return int(string) + (num * 10)

    # add the next string item into our num value
    num = int(string[0:1]) + (num * 10)

    # recurse through the rest of the string
    # and add each letter to num
    return myAtoiRecursive(string[1:], num)

# Driver Code   
string = "112"

print(myAtoiRecursive(string, 0))

# This code is contributed by Frank-Hu-MSFT
```

## C#

```
// Recursive C# program to compute atoi()
using System;
class GFG{

// Recursive function to compute atoi()
static int myAtoiRecursive(string str, int n)
{

    // Base case (Only one digit)
    if (n == 1)
    {
        return str[0] - '0';
    }

    // If more than 1 digits, recur for (n-1),
    // multiply result with 10 and add last digit
    return (10 * myAtoiRecursive(str, n - 1) +
                                  str[n - 1] - '0');
}

// Driver code
public static void Main()
{
    string str = "112";
    int n = str.Length;

    Console.Write(myAtoiRecursive(str, n));
}
}

// This code is contributed by Nidhi_Biet
```

**输出:**

```
112
```

本文由**纳伦德拉·康拉尔卡尔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息