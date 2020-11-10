# 使用多项式滚动哈希函数

> 原文：[https://www.geeksforgeeks.org/string-hashing-using-polynomial-rolling-hash-function/](https://www.geeksforgeeks.org/string-hashing-using-polynomial-rolling-hash-function/)

的字符串哈希

### **什么是字符串哈希？**

字符串哈希是将字符串转换为整数的方式，该整数称为该字符串的哈希。

理想的散列是发生冲突的机会最小的散列（即 2 个具有相同散列的不同字符串）。

### **多项式滚动哈希函数**

在这种哈希技术中，字符串的哈希计算为：

![hash = (s[0]*P^{0} + s[1]*P^{1} + ....s[m]*P^{m}) mod M    ](img/a4a2055291e80c13bb3dfbc8a1ce14d3.png "Rendered by QuickLaTeX.com")

其中`P`和`M`是一些正数。 `s[0], s[1], s[2] … s[n-1]`是分配给英语字母中每个字符的值（`a -> 1, b -> 2, … z -> 26`）。

**`P`和`M`的适当值**

*   `P`：值可以是任何等于与所使用的不同字符数相等的质数。

    例如：如果输入字符串仅包含英语字母的小写字母，则`P = 31`是`P`的适当值。

    如果输入字符串同时包含大写和小写字母，则`P = 53`是 适当的选择。

*   `M`：两个随机字符串碰撞的概率与`m`成反比，因此`m`应该是一个大质数。

    `M = 10 ^ 9 + 9`是一个不错的选择。

以下是使用多项式哈希函数实现的字符串哈希：

## C++

```cpp

// C++ implementation of the
// Polynomial Rolling Hash Function

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// the hash of a string
long long polynomialRollingHash(
    string const& str)
{
    // P and M
    int p = 31;
    int m = 1e9 + 9;
    long long power_of_p = 1;
    long long hash_val = 0;

    // Loop to calculate the hash value
    // by iterating over the elements of string
    for (int i = 0; i < str.length(); i++) {
        hash_val
            = (hash_val
               + (str[i] - 'a' + 1) * power_of_p)
              % m;
        power_of_p
            = (power_of_p * p) % m;
    }
    return hash_val;
}

/// Driver Code
int main()
{
    // Given strings
    string str1 = "geeksforgeeks";
    string str2 = "geeks";

    cout << "Hash of '" << str1 << "' = "
         << polynomialRollingHash(str1);
    cout << endl;
}

```

## Java

```java

// Java implementation of the
// Polynomial Rolling Hash Function
class GFG{

// Function to calculate
// the hash of a String
static long polynomialRollingHash(String str)
{

    // P and M
    int p = 31;
    int m = (int)(1e9 + 9);
    long power_of_p = 1;
    long hash_val = 0;

    // Loop to calculate the hash value
    // by iterating over the elements of String
    for(int i = 0; i < str.length(); i++) 
    {
        hash_val = (hash_val + (str.charAt(i) -
                    'a' + 1) * power_of_p) % m;
        power_of_p = (power_of_p * p) % m;
    }
    return hash_val;
}

// Driver Code
public static void main(String[] args)
{

    // Given Strings
    String str1 = "geeksforgeeks";
    String str2 = "geeks";

    System.out.print("Hash of '" + str1 + "' = " +
                     polynomialRollingHash(str1));
}
}

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 implementation of the
# Polynomial Rolling Hash Function

# Function to calculate
# the hash of a string
def polynomialRollingHash(str):

    # P and M
    p = 31
    m = 1e9 + 9
    power_of_p = 1
    hash_val = 0

    # Loop to calculate the hash value
    # by iterating over the elements of string
    for i in range(len(str)):
        hash_val = ((hash_val + (ord(str[i]) -
                                 ord('a') + 1) *
                              power_of_p) % m)

        power_of_p = (power_of_p * p) % m

    return int(hash_val)

# Driver Code
if __name__ == '__main__':

    # Given string
    str1 = "geeksforgeeks"

    print("Hash of '{}' = {}".format(
          str1, polynomialRollingHash(str1)))

# This code is contributed by Shivam Singh

```

## C#

```cs

// C# implementation of the
// Polynomial Rolling Hash Function
using System;
class GFG{

// Function to calculate
// the hash of a String
static long polynomialRollingHash(String str)
{    
    // P and M
    int p = 31;
    int m = (int)(1e9 + 9);
    long power_of_p = 1;
    long hash_val = 0;

    // Loop to calculate the hash value
    // by iterating over the elements of String
    for(int i = 0; i < str.Length; i++) 
    {
        hash_val = (hash_val + (str[i] -
                    'a' + 1) * power_of_p) % m;
        power_of_p = (power_of_p * p) % m;
    }
    return hash_val;
}

// Driver Code
public static void Main(String[] args)
{    
    // Given Strings
    String str1 = "geeksforgeeks";
    String str2 = "geeks";

    Console.Write("Hash of '" + str1 + "' = " +
                   polynomialRollingHash(str1));
}
}

// This code is contributed by 29AjayKumar

```

**输出**： 

```
Hash of 'geeksforgeeks' = 111226362

```



* * *

* * *



