# 惊人的数字

> 原文:[https://www.geeksforgeeks.org/astonishing-numbers/](https://www.geeksforgeeks.org/astonishing-numbers/)

**惊人数**是一个数 **N** ，其表示可以分解为两部分， **a** 和 **b** ，使得 **N** 等于从 **a** 到 **b** 和 **a + b = N** 的整数之和，其中**'+**表示串联。
很少有惊人的数字是:

> 15, 27, 429, 1353, 1863, 3388, 3591, 7119..

### 检查 N 是否是一个惊人的数字

给定一个数字 **N** ，任务是检查 **N** 是否是一个**惊人的数字**。如果 **N** 是一个惊人的数字，那么打印**“是”**否则打印**“否”**。
**示例:**

> **输入:**N = 429
> T3】输出:是
> T6】说明:T8】429 = 4+5+6……..+ 29，其中 **a** = 4、 **b** = 29
> 、 **a + b** = 429 其中+表示串联
> **输入:** N = 28
> **输出:**否

**方法:**想法是运行 I 和 j 的两个循环，找到从 I 到和变成> = N 的所有整数的和。如果在任何时间点和变成等于 N，那么我们也将检查 I 和 j 的连接是否等于 N。如果等于，那么这个数字就是一个惊人的数字
下面是上面方法的实现:

## C++

```
// C++ implementation for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to concatenate
// two integers into one
int concat(int a, int b)
{

    // Convert both the integers to string
    string s1 = to_string(a);
    string s2 = to_string(b);

    // Concatenate both strings
    string s = s1 + s2;

    // Convert the concatenated string
    // to integer
    int c = stoi(s);

    // return the formed integer
    return c;
}

// Function to check if N is a
// Astonishing number
bool isAstonishing(int n)
{
    // Loop to find sum of all integers
    // from i till the sum becomes >= n
    for (int i = 1; i < n; i++) {

        // variable to store
        // sum of all integers
        // from i to j and
        // check if sum and
        // concatenation equals n or not
        int sum = 0;
        for (int j = i; j < n; j++) {

            sum += j;

            if (sum == n) {

                // finding concatenation
                // of i and j
                int concatenation
                    = concat(i, j);

                // condition for
                // Astonishing number
                if (concatenation == n) {
                    return true;
                }
            }
        }
    }
    return false;
}

// Driver Code
int main()
{
    // Given Number
    int n = 429;

    // Function Call
    if (isAstonishing(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the
// above approach
import java.io.*;
class GFG{

// Function to concatenate
// two integers into one
static int concat(int a, int b)
{

    // Convert both the integers to String
    String s1 = Integer.toString(a);
    String s2 = Integer.toString(b);

    // Concatenate both Strings
    String s = s1 + s2;

    // Convert the concatenated String
    // to integer
    int c = Integer.parseInt(s);

    // return the formed integer
    return c;
}

// Function to check if N is a
// Astonishing number
static boolean isAstonishing(int n)
{
    // Loop to find sum of all integers
    // from i till the sum becomes >= n
    for (int i = 1; i < n; i++)
    {

        // variable to store
        // sum of all integers
        // from i to j and
        // check if sum and
        // concatenation equals n or not
        int sum = 0;
        for (int j = i; j < n; j++)
        {
            sum += j;

            if (sum == n)
            {

                // finding concatenation
                // of i and j
                int concatenation = concat(i, j);

                // condition for
                // Astonishing number
                if (concatenation == n)
                {
                    return true;
                }
            }
        }
    }
    return false;
}

// Driver Code
public static void main (String[] args)
{
    // Given Number
    int n = 429;

    // Function Call
    if (isAstonishing(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 implementation for the
# above approach

# Function to concatenate
# two integers into one
def concat(a, b):

    # Convert both the integers to string
    s1 = str(a)
    s2 = str(b)

    # Concatenate both strings
    s = s1 + s2

    # Convert the concatenated string
    # to integer
    c = int(s)

    # return the formed integer
    return c

# Function to check if N is a
# Astonishing number
def isAstonishing(n):

    # Loop to find sum of all integers
    # from i till the sum becomes >= n
    for i in range(n):

        # variable to store
        # sum of all integers
        # from i to j and
        # check if sum and
        # concatenation equals n or not
        sum = 0
        for j in range(i, n):

            sum += j

            if (sum == n):

                # finding concatenation
                # of i and j
                concatenation = concat(i, j)

                # condition for
                # Astonishing number
                if (concatenation == n):
                    return True
    return False

# Driver Code

# Given Number
n = 429

# Function Call
if (isAstonishing(n)):
    print('Yes')
else:
    print('No')

# This code is contributed by Yatin
```

## C#

```
// C# implementation for the
// above approach
using System;
class GFG{

// Function to concatenate
// two integers into one
static int concat(int a, int b)
{

    // Convert both the integers to String
    String s1 = a.ToString();
    String s2 = b.ToString();

    // Concatenate both Strings
    String s = s1 + s2;

    // Convert the concatenated String
    // to integer
    int c = Int32.Parse(s);

    // return the formed integer
    return c;
}

// Function to check if N is a
// Astonishing number
static bool isAstonishing(int n)
{
    // Loop to find sum of all integers
    // from i till the sum becomes >= n
    for (int i = 1; i < n; i++)
    {

        // variable to store
        // sum of all integers
        // from i to j and
        // check if sum and
        // concatenation equals n or not
        int sum = 0;
        for (int j = i; j < n; j++)
        {
            sum += j;

            if (sum == n)
            {

                // finding concatenation
                // of i and j
                int concatenation = concat(i, j);

                // condition for
                // Astonishing number
                if (concatenation == n)
                {
                    return true;
                }
            }
        }
    }
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    // Given Number
    int n = 429;

    // Function Call
    if (isAstonishing(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation for the
// above approach

// Function to concatenate
// two integers into one
function concat(a, b)
{

    // Convert both the integers to string
    var s1 = a.toString();
    var s2 = b.toString();

    // Concatenate both strings
    var s = s1 + s2;

    // Convert the concatenated string
    // to integer
    var c = s;

    // return the formed integer
    return c;
}

// Function to check if N is a
// Astonishing number
function isAstonishing(n)
{
    // Loop to find sum of all integers
    // from i till the sum becomes >= n
    for (var i = 1; i < n; i++) {

        // variable to store
        // sum of all integers
        // from i to j and
        // check if sum and
        // concatenation equals n or not
        var sum = 0;
        for (var j = i; j < n; j++) {

            sum += j;

            if (sum == n) {

                // finding concatenation
                // of i and j
                var concatenation
                    = concat(i, j);

                // condition for
                // Astonishing number
                if (concatenation == n) {
                    return true;
                }
            }
        }
    }
    return false;
}

// Driver Code
// Given Number
var n = 429;
// Function Call
if (isAstonishing(n))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*