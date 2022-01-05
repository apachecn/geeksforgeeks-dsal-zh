# 生成随机字母的程序

> 原文:[https://www . geesforgeks . org/program-generate-random-alphabets/](https://www.geeksforgeeks.org/program-generate-random-alphabets/)

先决条件: [rand()和 srand()](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/)
给定字符数组中的所有字母，打印给定大小的随机字符串。
我们将使用 rand()函数打印随机字符。它返回随机整数值。这个数字是由一种算法生成的，这种算法在每次调用时都会返回一系列明显不相关的数字。

1.  不可预测的随机字符的普遍使用是在密码学中，这是大多数试图在现代通信中提供安全性的方案(例如机密性、认证、电子商务等)的基础。
2.  随机数也用于通过随机化来近似“公平”的情况，例如选择陪审员和军队征兵彩票。
3.  随机数在物理学中有用途，如电子噪声研究、工程和运筹学。许多统计分析方法，如自举法，都需要随机数。

**伪代码:**
1。首先我们初始化两个字符数组，一个包含所有字母，另一个给定大小 n 来存储结果。
2。然后，我们将种子初始化为当前系统时间，以便每次生成新的随机种子时。
3。接下来，我们使用 for 循环直到 n 并存储随机生成的字母。
下面是上述方法的 C++实现:

## C++

```
// CPP Program to generate random alphabets
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Returns a string of random alphabets of
// length n.
string printRandomString(int n)
{
    char alphabet[MAX] = { 'a', 'b', 'c', 'd', 'e', 'f', 'g',
                          'h', 'i', 'j', 'k', 'l', 'm', 'n',
                          'o', 'p', 'q', 'r', 's', 't', 'u',
                          'v', 'w', 'x', 'y', 'z' };

    string res = "";
    for (int i = 0; i < n; i++)
        res = res + alphabet[rand() % MAX];

    return res;
}

// Driver code
int main()
{
   srand(time(NULL));
   int n = 10;
   cout << printRandomString(n);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Program to generate random alphabets
import java.util.*;

class GFG
{

static int MAX = 26;

// Returns a String of random alphabets of
// length n.
static String printRandomString(int n)
{
    char []alphabet = { 'a', 'b', 'c', 'd', 'e', 'f', 'g',
                        'h', 'i', 'j', 'k', 'l', 'm', 'n',
                        'o', 'p', 'q', 'r', 's', 't', 'u',
                        'v', 'w', 'x', 'y', 'z' };

    String res = "";
    for (int i = 0; i < n; i++)
        res = res + alphabet[(int) (Math.random() * 10 % MAX)];

    return res;
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    System.out.print(printRandomString(n));
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# Program to generate random alphabets
using System;

class GFG
{
static int MAX = 26;

// Returns a String of random alphabets of
// length n.
static String printRandomString(int n)
{
    char []alphabet = { 'a', 'b', 'c', 'd', 'e', 'f', 'g',
                        'h', 'i', 'j', 'k', 'l', 'm', 'n',
                        'o', 'p', 'q', 'r', 's', 't', 'u',
                        'v', 'w', 'x', 'y', 'z' };

    Random random = new Random();
    String res = "";
    for (int i = 0; i < n; i++)
        res = res + alphabet[(int)(random.Next(0, MAX))];

    return res;
}

// Driver code
public static void Main()
{
    int n = 10;
    Console.Write(printRandomString(n));
}
}
```

## java 描述语言

```
<script>
// JAVAscript Program to generate random alphabets
let MAX = 26;

// Returns a String of random alphabets of
// length n.
function printRandomString(n)
{
    let alphabet = ['a', 'b', 'c', 'd', 'e', 'f', 'g',
        'h', 'i', 'j', 'k', 'l', 'm', 'n',
        'o', 'p', 'q', 'r', 's', 't', 'u',
        'v', 'w', 'x', 'y', 'z'];

    let res = "";
    for (let i = 0; i < n; i++)
    {
        res = res + alphabet[Math.floor(Math.random() * 10) % MAX];
    }

    return res;
}

// Driver code
let n = 10;
document.write(printRandomString(n));

// This code is contributed by gfgking.
</script>
```

**输出:**

```
jgyuihhlxb
```

这个程序会在我们每次运行代码时打印不同的字符。