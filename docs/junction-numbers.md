# 连接编号

> 原文:[https://www.geeksforgeeks.org/junction-numbers/](https://www.geeksforgeeks.org/junction-numbers/)

**结号**是一个数字 **N** 如果它可以写成 K + SumOfDIgits(k)至少两个 K 的话

> 101, 103, 105, 107, 109, 111, 113, 115….

### 检查数字 N 是否为交叉点编号

给定一个数字 **N** ，任务是检查 **N** 是否为**路口号**。如果 **N** 是一个连接编号，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 1106
> **输出:**是
> **说明:**
> 1106 = 1093+(1+0+9+3)= 1102+(1+1+0+2)
> **输入:** N = 11
> **输出:**否

**方法:**由于**结数**是一个数 **N** 如果它可以写成 K + SumOfDIgits(k)至少两个 K，那么对于一个循环中从 1 到 N 的所有数，我们将检查 I+SumOfDIgits(I)是否等于 N。如果等于 N 打印**“是”**否则打印**“否”**。
以下是上述方法的实施:

## C++

```
// C++ implementation for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// sum Of digits of N
int sum(int n)
{

    // To store sum of N and
    // sumOfdigitsof(N)
    int sum = 0;

    while (n != 0) {
        // extracting digit
        int r = n % 10;
        sum = sum + r;
        n = n / 10;
    }

    return sum;
}

// Function to check Junction numbers
bool isJunction(int n)
{
    // To store count of ways n can be
    // represented as i + SOD(i)
    int count = 0;
    for (int i = 1; i <= n; i++) {
        if (i + sum(i) == n)
            count++;
    }

    return count >= 2;
}

// Driver Code
int main()
{
    int N = 111;

    // Function Call
    if (isJunction(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Function to find the
// sum Of digits of N
static int sum(int n)
{

    // To store sum of N and
    // sumOfdigitsof(N)
    int sum = 0;

    while (n != 0)
    {
        // extracting digit
        int r = n % 10;
        sum = sum + r;
        n = n / 10;
    }
    return sum;
}

// Function to check Junction numbers
static boolean isJunction(int n)
{
    // To store count of ways n can be
    // represented as i + SOD(i)
    int count = 0;
    for (int i = 1; i <= n; i++)
    {
        if (i + sum(i) == n)
            count++;
    }
    return count >= 2;
}

// Driver Code
public static void main(String[] args)
{
    int N = 111;

    // Function Call
    if (isJunction(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find the
# sum Of digits of N
def sum1(n):

    # To store sum of N and
    # sumOfdigitsof(N)
    sum1 = 0

    while (n != 0):

        # extracting digit
        r = n % 10
        sum1 = sum1 + r
        n = n // 10

    return sum1

# Function to check Junction numbers
def isJunction(n):

    # To store count of ways n can be
    # represented as i + SOD(i)
    count = 0
    for i in range(1, n + 1):
        if (i + sum1(i) == n):
            count = count + 1

    return count >= 2

# Driver Code
if __name__=='__main__':

    # Given Number
    n = 111

    # Function Call
    if (isJunction(n) == 1):
        print("Yes")
    else:
        print("No")

# This code is contributed by rock_cool
```

## C#

```
// C# program for above approach
using System;
class GFG{

// Function to find the
// sum Of digits of N
static int sum(int n)
{

    // To store sum of N and
    // sumOfdigitsof(N)
    int sum = 0;

    while (n != 0)
    {
        // extracting digit
        int r = n % 10;
        sum = sum + r;
        n = n / 10;
    }
    return sum;
}

// Function to check Junction numbers
static bool isJunction(int n)
{
    // To store count of ways n can be
    // represented as i + SOD(i)
    int count = 0;
    for (int i = 1; i <= n; i++)
    {
        if (i + sum(i) == n)
            count++;
    }
    return count >= 2;
}

// Driver Code
public static void Main()
{
    int N = 111;

    // Function Call
    if (isJunction(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Nidhi Biet
```

## java 描述语言

```
<script>

// Javascript program for above approach

    // Function to find the
    // sum Of digits of N
    function sum( n) {

        // To store sum of N and
        // sumOfdigitsof(N)
        let sum = 0;

        while (n != 0) {
            // extracting digit
            let r = n % 10;
            sum = sum + r;
            n = parseInt(n / 10);
        }
        return sum;
    }

    // Function to check Junction numbers
    function isJunction( n) {
        // To store count of ways n can be
        // represented as i + SOD(i)
        let count = 0;
        for ( i = 1; i <= n; i++) {
            if (i + sum(i) == n)
                count++;
        }
        return count >= 2;
    }

    // Driver Code

        let N = 111;

        // Function Call
        if (isJunction(N))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(n)*
T5】参考:[http://www.numbersaplenty.com/set/junction_number/](http://www.numbersaplenty.com/set/junction_number/)