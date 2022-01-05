# 打印所有小于 N 的数字，最多 2 个唯一数字

> 原文:[https://www . geeksforgeeks . org/print-all-numbers-小于 n-最多 2 个唯一数字/](https://www.geeksforgeeks.org/print-all-numbers-less-than-n-with-at-most-2-unique-digits/)

给定一个数字 n(小于 10^9).任务是打印所有小于 N 的数字，这些数字最多有 2 个唯一的数字。
**注**:100、111、101 等数字有效，因为唯一位数最多为 2，123 无效，因为它有 3 个唯一位数。
**示例:**

> **输入** : N = 12
> **输出**:数字为:1 2 3 4 5 6 7 8 9 10 11
> **输入** : N = 154
> **输出**:数字为:1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100 101

**接近** :

*   既然我们说最多两个唯一的数字，两个循环就给我们两个数字的所有组合。
*   递归函数是用两个数字生成所有数字的术语编写的。
*   调用 num 初始为 0 的函数，使用递归 **num*10+a** 和 **num*10+b** 生成数字，基本情况为 num > =n。
*   集合可以用来存储所有的数字，因为递归函数可以生成重复的元素。

以下是上述方法的实现:

## C++

```
// C++ program to print all the numbers
// less than N which have at most 2 unique digits
#include <bits/stdc++.h>
using namespace std;

set<int> st;

// Function to generate all possible numbers
void generateNumbers(int n, int num, int a, int b)
{
    // If the number is less than n
    if (num > 0 && num < n)
        st.insert(num);

    // If the number exceeds
    if (num >= n)
        return;

    // Check if it is not the same number
    if (num * 10 + a > num)
        generateNumbers(n, num * 10 + a, a, b);

    generateNumbers(n, num * 10 + b, a, b);
}

// Function to print all numbers
void printNumbers(int n)
{
    // All combination of digits
    for (int i = 0; i <= 9; i++)
        for (int j = i + 1; j <= 9; j++)
            generateNumbers(n, 0, i, j);

    cout << "The numbers are: ";

    // Print all numbers
    while (!st.empty()) {
        cout << *st.begin() << " ";
        st.erase(st.begin());
    }
}

// Driver code
int main()
{
    int n = 12;

    printNumbers(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all the numbers
// less than N which have at most 2 unique digits
import java.util.*;
class GFG{

static Set<Integer> st= new HashSet<Integer>();

// Function to generate all possible numbers
static void generateNumbers(int n, int num, int a, int b)
{
    // If the number is less than n
    if (num > 0 && num < n)
        st.add(num);

    // If the number exceeds
    if (num >= n)
        return;

    // Check if it is not the same number
    if (num * 10 + a > num)
        generateNumbers(n, num * 10 + a, a, b);

    generateNumbers(n, num * 10 + b, a, b);
}

// Function to print all numbers
static void printNumbers(int n)
{
    // All combination of digits
    for (int i = 0; i <= 9; i++)
        for (int j = i + 1; j <= 9; j++)
            generateNumbers(n, 0, i, j);

    System.out.print( "The numbers are: ");

    // Print all numbers
    System.out.print(st);

    st.clear();
}

// Driver code
public static void main(String args[])
{
    int n = 12;

    printNumbers(n);

}
}
// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to print all the
# numbers less than N which have at
# most 2 unique digits
st = set()

# Function to generate all possible numbers
def generateNumbers(n, num, a, b):

    # If the number is less than n
    if (num > 0 and num < n):
        st.add(num)

    # If the number exceeds
    if (num >= n):
        return

    # Check if it is not the same number
    if (num * 10 + a > num):
        generateNumbers(n, num * 10 + a, a, b)

    generateNumbers(n, num * 10 + b, a, b)

# Function to print all numbers
def printNumbers(n):

    # All combination of digits
    for i in range(10):
        for j in range(i + 1, 10, 1):
            generateNumbers(n, 0, i, j)

    print("The numbers are:", end = " ")

    # Print all numbers
    l = list(st)
    for i in l:
        print(i, end = " ")

# Driver code
if __name__ == '__main__':
    n = 12

    printNumbers(n)

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to print all the numbers
// less than N which have at most 2 unique digits
using System;
using System.Collections.Generic;

class GFG
{

static SortedSet<int> st = new SortedSet<int>();

// Function to generate all possible numbers
static void generateNumbers(int n, int num, int a, int b)
{
    // If the number is less than n
    if (num > 0 && num < n)
        st.Add(num);

    // If the number exceeds
    if (num >= n)
        return;

    // Check if it is not the same number
    if (num * 10 + a > num)
        generateNumbers(n, num * 10 + a, a, b);

    generateNumbers(n, num * 10 + b, a, b);
}

// Function to print all numbers
static void printNumbers(int n)
{
    // All combination of digits
    for (int i = 0; i <= 9; i++)
        for (int j = i + 1; j <= 9; j++)
            generateNumbers(n, 0, i, j);

    Console.Write( "The numbers are: ");

    // Print all numbers
    foreach(int obj in st)
        Console.Write(obj+" ");

    st.Clear();
}

// Driver code
public static void Main(String []args)
{
    int n = 12;

    printNumbers(n);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to print all the numbers
// less than N which have at most 2 unique digits

let st= new Set();

// Function to generate all possible numbers
function generateNumbers(n,num,a,b)
{
    // If the number is less than n
    if (num > 0 && num < n)
        st.add(num);

    // If the number exceeds
    if (num >= n)
        return;

    // Check if it is not the same number
    if (num * 10 + a > num)
        generateNumbers(n, num * 10 + a, a, b);

    generateNumbers(n, num * 10 + b, a, b);
}

// Function to print all numbers
function printNumbers(n)
{
    // All combination of digits
    for (let i = 0; i <= 9; i++)
        for (let j = i + 1; j <= 9; j++)
            generateNumbers(n, 0, i, j);

    document.write( "The numbers are: ");

    // Print all numbers
    document.write(Array.from(st).sort(function(a,b){return a-b;}).join(" "));

    st.clear();
}

// Driver code
let n = 12;

printNumbers(n);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
The numbers are: 1 2 3 4 5 6 7 8 9 10 11
```

**时间复杂度:** O(36* 2 <sup>30</sup> )