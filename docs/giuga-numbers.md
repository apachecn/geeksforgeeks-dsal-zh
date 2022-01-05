# 吉加号

> 原文:[https://www.geeksforgeeks.org/giuga-numbers/](https://www.geeksforgeeks.org/giuga-numbers/)

给定一个数字 **N** ，任务是检查 **N** 是否为**朱加号**。如果 **N** 是 **Giuga 编号**，则打印**“是”**否则打印**“否”**。

> 一个吉加数是一个复合数 **N** 这样 p 除**(N/p–1)**为每一个[质因数](https://www.geeksforgeeks.org/prime-factor/) **p** 的 **N** 。

**示例:**

> **输入:** N = 30
> **输出:**是
> **说明:**
> 30 是一个复合数，其素数因子为{2，3，5}，这样
> 2 除 30/2–1 = 14，
> 3 除 30/3–1 = 9，
> 5 除 30/5–1 = 5。
> 
> **输入:**N = 161
> T3】输出:否

**进场:**思路是检查 **N** 是否为复合数。如果没有，则打印“否”。
如果 **N** 是一个复合数，那么找出一个数的质因数，对于每个质因数 **p** 检查条件 p 除(N/p–1)是否成立。如果上述条件成立，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if n is
// a composite number
bool isComposite(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // This is checked to skip
    // middle 5 numbers
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function to check if N is a
// Giuga Number
bool isGiugaNum(int n)
{
    // N should be composite to be
    // a Giuga Number
    if (!(isComposite(n)))
        return false;

    int N = n;

    // Print the number of 2s
    // that divide n
    while (n % 2 == 0) {

        if ((N / 2 - 1) % 2 != 0)
            return false;

        n = n / 2;
    }

    // N must be odd at this point.
    // So we can skip one element
    for (int i = 3; i <= sqrt(n);
         i = i + 2) {

        // While i divides n,
        // print i and divide n
        while (n % i == 0) {
            if ((N / i - 1) % i != 0)
                return false;

            n = n / i;
        }
    }

    // This condition is to handle
    // the case when n
    // is a prime number > 2
    if (n > 2)
        if ((N / n - 1) % n != 0)
            return false;

    return true;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 30;

    // Function Call
    if (isGiugaNum(N))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if n is
// a composite number
static boolean isComposite(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // This is checked to skip
    // middle 5 numbers
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return true;

    return false;
}

// Function to check if N is a
// Giuga Number
static boolean isGiugaNum(int n)
{

    // N should be composite to be
    // a Giuga Number
    if (!(isComposite(n)))
        return false;

    int N = n;

    // Print the number of 2s
    // that divide n
    while (n % 2 == 0)
    {
        if ((N / 2 - 1) % 2 != 0)
            return false;
        n = n / 2;
    }

    // N must be odd at this point.
    // So we can skip one element
    for(int i = 3; i <= Math.sqrt(n);
                   i = i + 2)
    {

       // While i divides n,
       // print i and divide n
       while (n % i == 0)
       {
           if ((N / i - 1) % i != 0)
               return false;
           n = n / i;
        } 
    }

    // This condition is to handle
    // the case when n
    // is a prime number > 2
    if (n > 2)
        if ((N / n - 1) % n != 0)
            return false;

    return true;
}

// Driver code
public static void main(String[] args)
{

    // Given Number N
    int n = 30;

    // Function Call
    if (isGiugaNum(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to check if n is
# a composite number
def isComposite(n):

    # Corner cases
    if(n <= 1):
        return False
    if(n <= 3):
        return False

    # This is checked to skip
    # middle 5 numbers
    if(n % 2 == 0 or n % 3 == 0):
        return True

    i = 5
    while(i * i <= n):
        if(n % i == 0 or n % (i + 2) == 0):
            return True
        i += 6
    return False

# Function to check if N is a
# Giuga Number
def isGiugaNum(n):

    # N should be composite to be
    # a Giuga Number
    if(not(isComposite(n))):
        return False
    N = n

    # Print the number of 2s
    # that divide n
    while(n % 2 == 0):
        if((int(N / 2) - 1) % 2 != 0):
            return False
        n = int(n / 2)

    # N must be odd at this point.
    # So we can skip one element
    for i in range(3, int(math.sqrt(n)) + 1, 2):

        # While i divides n, 
           # print i and divide n
        while(n % i == 0):
            if((int(N / i) - 1) % i != 0):
                return False
            n = int(n / i)

    # This condition is to handle 
    # the case when n 
    # is a prime number > 2
    if(n > 2):
        if((int(N / n) - 1) % n != 0):
            return False
    return True

# Driver code 

# Given Number N
n = 30
if(isGiugaNum(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if n is
// a composite number
static bool isComposite(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // This is checked to skip
    // middle 5 numbers
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return true;

    return false;
}

// Function to check if N is a
// Giuga Number
static bool isGiugaNum(int n)
{

    // N should be composite to be
    // a Giuga Number
    if (!(isComposite(n)))
        return false;

    int N = n;

    // Print the number of 2s
    // that divide n
    while (n % 2 == 0)
    {
        if ((N / 2 - 1) % 2 != 0)
            return false;
        n = n / 2;
    }

    // N must be odd at this point.
    // So we can skip one element
    for(int i = 3; i <= Math.Sqrt(n);
            i = i + 2)
    {

       // While i divides n,
       // print i and divide n
       while (n % i == 0)
       {
           if ((N / i - 1) % i != 0)
               return false;
           n = n / i;
       }
    }

    // This condition is to handle
    // the case when n
    // is a prime number > 2
    if (n > 2)
        if ((N / n - 1) % n != 0)
            return false;

    return true;
}

// Driver code
static void Main()
{

    // Given Number N
    int N = 30;

    // Function Call
    if (isGiugaNum(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if n is
// a composite number
function isComposite(n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // This is checked to skip
    // middle 5 numbers
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    for(let i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return true;

    return false;
}

// Function to check if N is a
// Giuga Number
function isGiugaNum(n)
{

    // N should be composite to be
    // a Giuga Number
    if (!(isComposite(n)))
        return false;

    let N = n;

    // Print the number of 2s
    // that divide n
    while (n % 2 == 0)
    {
        if ((N / 2 - 1) % 2 != 0)
            return false;

        n = n / 2;
    }

    // N must be odd at this point.
    // So we can skip one element
    for(let i = 3;
            i <= Math.sqrt(n);
            i = i + 2)
    {

       // While i divides n,
       // print i and divide n
       while (n % i == 0)
       {
           if ((N / i - 1) % i != 0)
               return false;

           n = n / i;
        } 
    }

    // This condition is to handle
    // the case when n
    // is a prime number > 2
    if (n > 2)
        if ((N / n - 1) % n != 0)
            return false;

    return true;
}

// Driver Code

// Given Number N
let n = 30;

// Function Call
if (isGiugaNum(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by susmitakundugoaldanga     

</script>
```

**Output:** 

```
Yes
```