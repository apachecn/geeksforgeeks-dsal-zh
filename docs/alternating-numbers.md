# 交替数字

> 原文:[https://www.geeksforgeeks.org/alternating-numbers/](https://www.geeksforgeeks.org/alternating-numbers/)

给定一个数字 **N** ，任务是检查 **N** 是否为**交替数字**。如果 **N** 是**交替号**，则打印**“是”**否则打印**“否”**。

> **交替数**是正整数，在基数-10 中，其位数的奇偶性是交替的，即数字 **N** 中的位数后面是奇数、偶数、奇数、…或偶数、奇数、偶数、…的顺序。

**示例:**

> **输入:** N = 129
> **输出:**是
> **说明:**
> 129 有交替的奇数偶数奇数形式的数字。
> 
> **输入:** N = 28
> **输出:**否
> **说明:**
> 28 的位数不是交替的奇偶形式。

**方法:**想法是将数字转换成字符串，并检查是否有任何数字后跟相同奇偶校验的数字，然后 **N** 不是**交替数字**，否则 **N** 是**交替数字**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a string is
// of the form even odd even odd...
bool isEvenOddForm(string s)
{
    int n = s.length();
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0 && s[i] % 2 != 0)
            return false;

        if (i % 2 == 1 && s[i] % 2 != 1)
            return false;
    }
    return true;
}

// Function to check if a string is
// of the form odd even odd even  ...
bool isOddEvenForm(string s)
{
    int n = s.length();
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0 && s[i] % 2 != 1)
            return false;

        if (i % 2 == 1 && s[i] % 2 != 0)
            return false;
    }
    return true;
}

// Function to check if n is an
// alternating number
bool isAlternating(int n)
{
    string str = to_string(n);
    return (isEvenOddForm(str)
            || isOddEvenForm(str));
}

// Driver Code
int main()
{
    // Given Number N
    int N = 129;

    // Function Call
    if (isAlternating(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if a string is
// of the form even odd even odd...
static boolean isEvenOddForm(String s)
{
    int n = s.length();
    for(int i = 0; i < n; i++)
    {
       if (i % 2 == 0 && s.charAt(i) % 2 != 0)
           return false;
       if (i % 2 == 1 && s.charAt(i) % 2 != 1)
           return false;
    }
    return true;
}

// Function to check if a string is
// of the form odd even odd even ...
static boolean isOddEvenForm(String s)
{
    int n = s.length();
    for(int i = 0; i < n; i++)
    {
       if (i % 2 == 0 && s.charAt(i) % 2 != 1)
           return false;
       if (i % 2 == 1 && s.charAt(i) % 2 != 0)
           return false;
    }
    return true;
}

// Function to check if n is an
// alternating number
static boolean isAlternating(int n)
{
    String str = Integer.toString(n);
    return (isEvenOddForm(str) ||
            isOddEvenForm(str));
}

// Driver Code
public static void main(String[] args)
{

    // Given number N
    int N = 129;

    // Function call
    if (isAlternating(N))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This Code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a string is
# of the form even odd even odd...
def isEvenOddForm(s):
    n = len(s)
    for i in range(n):
        if (i % 2 == 0 and
            int(s[i]) % 2 != 0):
            return False
        if (i % 2 == 1 and
            int(s[i]) % 2 != 1):
            return False
    return True

# Function to check if a string is
# of the form odd even odd even ...
def isOddEvenForm(s):
    n = len(s)
    for i in range(n):
        if (i % 2 == 0 and
            int(s[i]) % 2 != 1):
            return False
        if (i % 2 == 1 and
            int(s[i]) % 2 != 0):
            return False
    return True

# Function to check if n is an
# alternating number
def isAlternating(n):
    s = str(n)
    return (isEvenOddForm(s) or
            isOddEvenForm(s))

# Driver Code

# Given Number N
N = 129

# Function Call
if (isAlternating(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by Vishal Maurya
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if a string is
// of the form even odd even odd...
static bool isEvenOddForm(String s)
{
    int n = s.Length;
    for(int i = 0; i < n; i++)
    {
        if (i % 2 == 0 && s[i] % 2 != 0)
            return false;
        if (i % 2 == 1 && s[i] % 2 != 1)
            return false;
    }
    return true;
}

// Function to check if a string is
// of the form odd even odd even ...
static bool isOddEvenForm(String s)
{
    int n = s.Length;
    for(int i = 0; i < n; i++)
    {
        if (i % 2 == 0 && s[i] % 2 != 1)
            return false;
        if (i % 2 == 1 && s[i] % 2 != 0)
            return false;
    }
    return true;
}

// Function to check if n is an
// alternating number
static bool isAlternating(int n)
{
    String str = n.ToString();
    return (isEvenOddForm(str) ||
            isOddEvenForm(str));
}

// Driver Code
public static void Main(String[] args)
{

    // Given number N
    int N = 129;

    // Function call
    if (isAlternating(N))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if a string is
// of the form even odd even odd...
function isEvenOddForm(s)
{
    let n = s.length;
    for(let i = 0; i < n; i++)
    {
        if (i % 2 == 0 && s[i] % 2 != 0)
            return false;
        if (i % 2 == 1 && s[i] % 2 != 1)
            return false;
    }
    return true;
}

// Function to check if a string is
// of the form odd even odd even ...
function isOddEvenForm(s)
{
    let n = s.length;
    for(let i = 0; i < n; i++)
    {
        if (i % 2 == 0 && s[i] % 2 != 1)
            return false;
        if (i % 2 == 1 && s[i] % 2 != 0)
            return false;
    }
    return true;
}

// Function to check if n is an
// alternating number
function isAlternating(n)
{
    let str = n.toString();
    return (isEvenOddForm(str) ||
            isOddEvenForm(str));
}

// Driver code   

// Given number N
let N = 129;

// Function call
if (isAlternating(N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(log<sub>10</sub>N)*