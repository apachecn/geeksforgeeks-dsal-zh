# 检查字符串数组是否可以对应特定的数字 X

> 原文:[https://www . geesforgeks . org/check-字符串数组是否可以对应特定的数字-x/](https://www.geeksforgeeks.org/check-whether-an-array-of-strings-can-correspond-to-a-particular-number-x/)

给定一个整数 **X** 和一个表示从**【2，36】**开始的任意基数范围内的数字的字符串数组 **str** ，任务是通过给每个字符串指定从 2 到 36 的期望基数来检查是否所有字符串都可以转换为 X，这样字符串的十进制基数等价于 X

**示例:**

> **输入:** str = {10000，20，16}，X = 16
> **输出:**是
> **说明:**
> 数组中的每个数字在转换为十进制基数时等于 16，如果选择以下基数:
> (10000)<sub>2</sub>=(16)<sub>10</sub>
> (20)<sub>8</sub>=(1)
> 
> **输入:** str = {10100，5A，1011010}，X = 90
> **输出:**是
> 数组中的每个数字在转换为十进制基数时等于 90，如果选择以下基数:
> (10100)<sub>3</sub>=(90)<sub>10</sub>
> (5A)<sub>16</sub>=(90)<sub>110</sub>

**方法:**想法是[将数组中的每个数字转换为十进制基数](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/)，方法是将其指定为从 2 到 36 的基数，然后检查每个转换后的数字是否等于 X。

上述方法的分步算法描述如下–

1.  将计数初始化为 0，以便在转换时检查等于 X 的数字的计数。
2.  运行一个循环来迭代数组的数字，然后对每个数字–
    *   运行另一个从 2 到 36 的循环，将基数赋给该数，并找到该数的[十进制等价物](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/)。
    *   如果该数字的十进制等效值等于 X，则计数增加 1，并中断循环，因为没有为同一数字指定任何其他基数。
3.  如果可转换为 X 的数字的计数等于数组的长度，则数组可以对应于数字 X

下面是上述方法的实现:

## C++

```
// C++ implementation to check
// whether array of strings
// can correspond to a number X

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// base possible for the number N
int val(char c)
{
    if (c >= '0' && c <= '9')
        return (int)c - '0';
    else
        return (int)c - 'A' + 10;
}

// Function to find the decimal
// equivalent of the number
int toDeci(string str, int base)
{
    int len = str.size();
    int power = 1;
    int num = 0;
    int i;
    for (i = len - 1; i >= 0; i--) {

        // Condition to check if the
        // number is convertible
        // to another base
        if (val(str[i]) >= base) {
            return -1;
        }
        num += val(str[i]) * power;
        power = power * base;
    }
    return num;
}

// Function to check that the
// array can correspond to a number X
void checkCorrespond(vector<string> str,
                                int x){

    // counter to count the numbers
    // those are convertible to X
    int counter = 0;
    int n = str.size();

    // Loop to iterate over the array
    for (int i = 0; i < n; i++) {
        for (int j = 2; j <= 36; j++) {

            // Convert the current string
            // to every base for checking
            // whether it will correspond
            // to X from any base
            if (toDeci(str[i], j) == x) {
                counter++;
                break;
            }
        }
    }

    // Condition to check if every
    // number of the array can
    // be converted to X
    if (counter == n)
        cout << "YES"
            << "\n";
    else
        cout << "NO"
            << "\n";
}

// Driver Code
int main()
{
    int x = 16;

    // The set of strings
    // in base from [2, 36]
    vector<string> str =
         { "10000", "20", "16" };
    checkCorrespond(str, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// whether array of Strings
// can correspond to a number X

class GFG{

// Function to find the maximum
// base possible for the number N
static int val(char c)
{
    if (c >= '0' && c <= '9')
        return (int)c - '0';
    else
        return (int)c - 'A' + 10;
}

// Function to find the decimal
// equivalent of the number
static int toDeci(String str, int base)
{
    int len = str.length();
    int power = 1;
    int num = 0;
    int i;
    for (i = len - 1; i >= 0; i--) {

        // Condition to check if the
        // number is convertible
        // to another base
        if (val(str.charAt(i)) >= base) {
            return -1;
        }
        num += val(str.charAt(i)) * power;
        power = power * base;
    }
    return num;
}

// Function to check that the
// array can correspond to a number X
static void checkCorrespond(String[] str,
                                int x){

    // counter to count the numbers
    // those are convertible to X
    int counter = 0;
    int n = str.length;

    // Loop to iterate over the array
    for (int i = 0; i < n; i++) {
        for (int j = 2; j <= 36; j++) {

            // Convert the current String
            // to every base for checking
            // whether it will correspond
            // to X from any base
            if (toDeci(str[i], j) == x) {
                counter++;
                break;
            }
        }
    }

    // Condition to check if every
    // number of the array can
    // be converted to X
    if (counter == n)
        System.out.print("YES"
           + "\n");
    else
        System.out.print("NO"
           + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int x = 16;

    // The set of Strings
    // in base from [2, 36]
    String[] str =
         { "10000", "20", "16" };
    checkCorrespond(str, x);
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to check
# whether array of strings
# can correspond to a number X

# Function to find the maximum
# base possible for the number N
def val(c):
    if (c >= '0' and c <= '9'):
        return int(c)
    else:
        return c - 'A' + 10

# Function to find the decimal
# equivalent of the number
def toDeci(strr, base):

    lenn = len(strr)
    power = 1
    num = 0
    for i in range(lenn - 1, -1, -1):

        # Condition to check if the
        # number is convertible
        # to another base
        if (val(strr[i]) >= base):
            return -1

        num += val(strr[i]) * power
        power = power * base

    return num

# Function to check that the
# array can correspond to a number X
def checkCorrespond(strr, x):

    # counter to count the numbers
    # those are convertible to X
    counter = 0
    n = len(strr)

    # Loop to iterate over the array
    for i in range(n):
        for j in range(2,37):

            # Convert the current string
            # to every base for checking
            # whether it will correspond
            # to X from any base
            if (toDeci(strr[i], j) == x):
                counter += 1
                break

    # Condition to check if every
    # number of the array can
    # be converted to X
    if (counter == n):
        print("YES")
    else:
        print("NO")

# Driver Code
x = 16

# The set of strings
# in base from [2, 36]
strr = ["10000", "20", "16"]
checkCorrespond(strr, x)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to check
// whether array of Strings
// can correspond to a number X
using System;

class GFG{

// Function to find the maximum
// base possible for the number N
static int val(char c)
{
    if (c >= '0' && c <= '9')
        return (int)c - '0';
    else
        return (int)c - 'A' + 10;
}

// Function to find the decimal
// equivalent of the number
static int toDeci(String str, int Base)
{
    int len = str.Length;
    int power = 1;
    int num = 0;
    int i;
    for (i = len - 1; i >= 0; i--) {

        // Condition to check if the
        // number is convertible
        // to another base
        if (val(str[i]) >= Base) {
            return -1;
        }
        num += val(str[i]) * power;
        power = power * Base;
    }
    return num;
}

// Function to check that the
// array can correspond to a number X
static void checkCorrespond(String[] str,
                                int x){

    // counter to count the numbers
    // those are convertible to X
    int counter = 0;
    int n = str.Length;

    // Loop to iterate over the array
    for (int i = 0; i < n; i++) {
        for (int j = 2; j <= 36; j++) {

            // Convert the current String
            // to every base for checking
            // whether it will correspond
            // to X from any base
            if (toDeci(str[i], j) == x) {
                counter++;
                break;
            }
        }
    }

    // Condition to check if every
    // number of the array can
    // be converted to X
    if (counter == n)
        Console.Write("YES"
           + "\n");
    else
        Console.Write("NO"
           + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int x = 16;

    // The set of Strings
    // in base from [2, 36]
    String[] str =
         { "10000", "20", "16" };
    checkCorrespond(str, x);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation to check
// whether array of Strings
// can correspond to a number X

// Function to find the maximum
// base possible for the number N
function val(c)
{
    if (c >= '0' && c <= '9')
        return c - '0';
    else
        return c - 'A' + 10;
}

// Function to find the decimal
// equivalent of the number
function toDeci(str, base)
{
    let len = str.length;
    let power = 1;
    let num = 0;
    let i;
    for (i = len - 1; i >= 0; i--) {

        // Condition to check if the
        // number is convertible
        // to another base
        if (val(str[i]) >= base) {
            return -1;
        }
        num += val(str[i]) * power;
        power = power * base;
    }
    return num;
}

// Function to check that the
// array can correspond to a number X
function checkCorrespond(str, x){

    // counter to count the numbers
    // those are convertible to X
    let counter = 0;
    let n = str.length;

    // Loop to iterate over the array
    for (let i = 0; i < n; i++) {
        for (let j = 2; j <= 36; j++) {

            // Convert the current String
            // to every base for checking
            // whether it will correspond
            // to X from any base
            if (toDeci(str[i], j) == x) {
                counter++;
                break;
            }
        }
    }

    // Condition to check if every
    // number of the array can
    // be converted to X
    if (counter == n)
        document.write("YES"
           + "<br/>");
    else
        document.write("NO"
           + "<br/>");
}

// Driver Code

    let x = 16;

    // The set of Strings
    // in base from [2, 36]
    let str =
         [ "10000", "20", "16" ];
    checkCorrespond(str, x);

</script>
```

**Output:** 

```
YES
```

**性能分析:**

*   **时间复杂度:** O(N)。
*   **辅助空间:** O(1)。