# 直线编号

> 原文:[https://www.geeksforgeeks.org/straight-line-number/](https://www.geeksforgeeks.org/straight-line-number/)

给定一个数字 **N** ，任务是检查 **N** 是否为**直线数字**。如果 **N** 是**直线编号**，则打印**“是”**否则打印**“否”**。

> 直线数字是一个大于 99 的数字，其中的数字组成一个[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)。

**示例:**

> **输入:** N = 135
> **输出:**是
> **说明:**
> 数字 N 的位数是 1、3、5。
> 1 3 5 是一个 d = 2 的 AP
> 
> **输入:**N = 136
> T3】输出:否

**方法:**想法是把给定的数字 **N** 转换成字符串，检查连续数字之间的差异是否相同。如果所有对应数字之间的差异相同，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if N is a
// Straight Line number or not
bool isStraighLineNum(int N)
{
    // N must be > 99
    if (N <= 99)
        return false;

    string str = to_string(N);

    // Difference between consecutive
    // digits must be same
    int d = str[1] - str[0];

    for (int i = 2; i < str.length(); i++)
        if (str[i] - str[i - 1] != d)
            return false;

    return true;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 135;

    // Function Call
    if (isStraighLineNum(n))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if N is a
// Straight Line number or not
static boolean isStraighLineNum(int N)
{

    // N must be > 99
    if (N <= 99)
        return false;

    String s = Integer.toString(N);

    // Difference between consecutive
    // digits must be same
    int d = s.charAt(1) - s.charAt(0);

    for(int i = 2; i < s.length(); i++)
       if (s.charAt(i) - s.charAt(i - 1) != d)
           return false;

    return true;
}

// Driver code
public static void main(String[] args)
{

    // Given Number N
    int n = 135;

    // Function Call
    if (isStraighLineNum(n))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if N is a
# Straight Line number or not
def isStraighLineNum(N):

    # N must be > 99
    if (N <= 99):
        return False;

    str1 = str(N);

    # Difference between consecutive
    # digits must be same
    d = int(str1[1]) - int(str1[0]);

    for i in range(2, len(str1)):
        if (int(str1[i]) -
            int(str1[i - 1]) != d):
            return False;

    return True;

# Driver Code

# Given Number N
N = 135;

# Function Call
if (isStraighLineNum(N)):
    print("Yes");
else:
    print("No");

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if N is a
// Straight Line number or not
static bool isStraighLineNum(int N)
{

    // N must be > 99
    if (N <= 99)
        return false;

    string s = N.ToString();

    // Difference between consecutive
    // digits must be same
    int d = s[1] - s[0];

    for(int i = 2; i < s.Length; i++)
       if (s[i] - s[i - 1] != d)
           return false;

    return true;
}

// Driver code
public static void Main()
{

    // Given Number N
    int n = 135;

    // Function Call
    if (isStraighLineNum(n))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if N is a
// Straight Line number or not
function isStraighLineNum(N)
{

    // N must be > 99
    if (N <= 99)
        return false;

    let s = N.toString();

    // Difference between consecutive
    // digits must be same
    let d = s[1] - s[0];

    for(let i = 2; i < s.length; i++)
       if (s[i] - s[i - 1] != d)
           return false;

    return true;
}

// Driver Code

// Given Number N
let n = 135;

// Function Call
if (isStraighLineNum(n))
{
    document.write("Yes");
}
else
{
    document.write("No");
}

// This code is contributed by susmitakundugoaldanga   

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(log<sub>10</sub>N)*