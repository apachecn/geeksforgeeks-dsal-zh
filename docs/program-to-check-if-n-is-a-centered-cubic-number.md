# 检查 N 是否为中心立方数的程序

> 原文:[https://www . geesforgeks . org/program-to-check-if-n-a-centered-cubid-number/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-centered-cubic-number/)

给定一个数字 **N** ，任务是检查 N 是否是一个[中心立方数](https://www.geeksforgeeks.org/centered-cube-number/)。

> A [心立方数](https://www.geeksforgeeks.org/centered-cube-number/)计算由第 I 层的正方形面上的 i <sup>2</sup> 点在 3D 中被同心立方体层包围的点形成的点数。前几个居中的立方体编号是 **1、9、35、91、189、341、559、855……**

**示例:**

> **输入:** N = 9
> **输出:**是
> **说明:**
> 9 是第二个居中的立方数
> **输入:** N = 6
> **输出:**否

**方法:**思想是从 1 开始迭代，检查第 i <sup>个</sup>项是否等于 N。

1.  [心立方数](https://www.geeksforgeeks.org/centered-cube-number/)的第 N 个<sup>项由![(2 * N + 1) * ( N^2 + N + 1)    ](img/6403e1af9225901c943b1119d3824600.png "Rendered by QuickLaTeX.com")给出。</sup>
2.  从 1 开始运行一个循环，找到第 I<sup>[个以立方体为中心的数字。](https://www.geeksforgeeks.org/centered-cube-number/)</sup>
3.  检查第一项是否等于 N。如果相等，则返回真。
4.  如果第 I 项大于 N，则返回 false。

以下是上述方法的实现:

## C++

```
// C++ program to check if N
// is a centered cubic number
#include <bits/stdc++.h>
using namespace std;

// Function to check if the number N
// is a centered cubic number
bool isCenteredcube(int N)
{
// Iterating from 1
    int i = 1;

// Infinite loop
    while (true) {

        // Finding ith_term
        int ith_term = (2 * i + 1)
* (i * i + i + 1);

        // Checking if the number N
        // is a Centered cube number
        if (ith_term == N) {
            return true;
        }

        // If ith_term > N then
        // N is not a Centered cube number
        if (ith_term > N) {
            return false;
        }

        // Incrementing i
        i++;
    }
}

// Driver code
int main()
{
    int N = 9;

    // Function call
    if (isCenteredcube(N)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if N
// is a centered cubic number
class GFG{

// Function to check if N
// is a centered cubic number
static boolean isCenteredcube(int N)
{

    // Iterating from 1
    int i = 1;

    // Infinite loop
    while (true)
    {

        // Finding ith_term
        int ith_term = (2 * i + 1) *
                       (i * i + i + 1);

        // Checking if the number N
        // is a centered cube number
        if (ith_term == N)
        {
            return true;
        }

        // If ith_term > N then N is 
        // not a centered cube number
        if (ith_term > N)
        {
            return false;
        }

        // Incrementing i
        i++;
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 9;

    // Function call
    if (isCenteredcube(N))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 program to check if N
# is a centered cubic number

# Function to check if N
# is a centered cubic number
def isCenteredcube(N):

    # Iterating from 1
    i = 1;

    # Infinite loop
    while (True):

        # Finding ith_term
        ith_term = ((2 * i + 1) *
                    (i * i + i + 1));

        # Checking if the number N
        # is a centered cube number
        if (ith_term == N):
            return True;

        # If ith_term > N then N is
        # not a centered cube number
        if (ith_term > N):
            return False;

        # Incrementing i
        i += 1;

# Driver code
N = 9;

# Function call
if (isCenteredcube(N)):
    print("Yes");
else:
    print("No");

# This code is contributed by Code_Mech
```

## C#

```
// C# program to check if N
// is a centered cubic number
using System;
class GFG{

// Function to check if N
// is a centered cubic number
static Boolean isCenteredcube(int N)
{

    // Iterating from 1
    int i = 1;

    // Infinite loop
    while (true)
    {

        // Finding ith_term
        int ith_term = (2 * i + 1) *
                       (i * i + i + 1);

        // Checking if the number N
        // is a centered cube number
        if (ith_term == N)
        {
            return true;
        }

        // If ith_term > N then N is
        // not a centered cube number
        if (ith_term > N)
        {
            return false;
        }

        // Incrementing i
        i++;
    }
}

// Driver code
public static void Main()
{
    int N = 9;

    // Function call
    if (isCenteredcube(N))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
    // Javascript program to check if N 
    // is a centered cubic number

    // Function to check if the number N
    // is a centered cubic number
    function isCenteredcube(N)
    {
        // Iterating from 1
        let i = 1;

        // Infinite loop
        while (true) {

            // Finding ith_term
            let ith_term = (2 * i + 1) * (i * i + i + 1);

            // Checking if the number N
            // is a Centered cube number
            if (ith_term == N) {
                return true;
            }

            // If ith_term > N then
            // N is not a Centered cube number
            if (ith_term > N) {
                return false;
            }

            // Incrementing i
            i++;
        }
    }

    let N = 9;

    // Function call
    if (isCenteredcube(N)) {
        document.write("Yes");
    }
    else {
        document.write("No");
    }

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N)。