# 多余的数字

> 原文:[https://www.geeksforgeeks.org/superabundant-numbers/](https://www.geeksforgeeks.org/superabundant-numbers/)

一个数是一个**余数**如果σ(n)/n>σ(m)/m 为所有 m < n，其中σ是 n 的除数之和

> 1, 2, 4, 6, 12, 24, 36, 48…

### 检查 N 是否是一个多余的数字

给定一个数字 **N** ，任务是检查 **N** 是否为**多余数字**。如果 **N** 是多余的号码，则打印**“是”**否则打印**“否”**。

**示例:**

> **输入:**N = 4
> T3】输出:是
> T6】解释:T8】σ(4)/4 = 7/4 = 1.75
> σ(1)/1 = 1/1 = 1
> σ(2)/2 = 3/2 = 1.5
> σ(3)/3 = 4/3 = 1.333333
> σ(N)/N>σ(m)/m 为所有 m【T11
> 
> **输入:**N = 10
> T3】输出:否

**方法:**对于从 1 到小于 N 的所有数字 I，检查σ(N)/N>σ(m)/m 是否为假，否则返回真。

**例如:**

> 如果 N = 4，则 i = 1 至 3 的σ(4)/4 = 7/4 = 1.75
> 
> σ(1)/1 = 1/1 = 1
> σ(2)/2 = 3/2 = 1.5
> σ(3)/3 = 4/3 = 1.333333
> σ(N)/N>σ(m)/m 所有 m < n、
> 因此最终返回真

下面是上述方法的实现:

## C++

```
// C++ implementation to check if
// a number is Superabundant

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum of all
// divisors of a given number
int sigma(int n)
{
    if (n == 1)
        return 1;

    // Sum of divisors
    int result = 0;

    // find all divisors which divides 'num'
    for (int i = 2; i <= sqrt(n); i++) {
        // if 'i' is divisor of 'n'
        if (n % i == 0) {

            // if both divisors are same
            // then add it once else add
            // both
            if (i == (n / i))
                result += i;
            else
                result += (i + n / i);
        }
    }

    // Add 1 and n to result as above loop
    // considers proper divisors greater
    // than 1.
    return (result + n + 1);
}

// Function to check if N is a
// superabundant number
bool isSuperabundant(int N)
{

    // to check all numbers from 1 to N
    for (float i = 1; i < N; i++) {
        float x = sigma(i) / i;
        float y = sigma(N) / (N * 1.0);
        if (x > y)
            return false;
    }
    return true;
}

// Driver code
int main()
{
    int N = 4;
    isSuperabundant(N) ? cout << "Yes"
                       : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if
// a number is Superabundant
class GFG{

// Function to calculate the sum of all
// divisors of a given number
static int sigma(int n)
{
    if (n == 1)
        return 1;

    // Sum of divisors
    int result = 0;

    // Find all divisors which divides 'num'
    for(int i = 2; i <= Math.sqrt(n); i++)
    {

        // If 'i' is divisor of 'n'
        if (n % i == 0)
        {

            // If both divisors are same
            // then add it once else add
            // both
            if (i == (n / i))
                result += i;
            else
                result += (i + n / i);
        }
    }

    // Add 1 and n to result as above loop
    // considers proper divisors greater
    // than 1.
    return (result + n + 1);
}

// Function to check if N is a
// superabundant number
static boolean isSuperabundant(int N)
{

    // To check all numbers from 1 to N
    for(double i = 1; i < N; i++)
    {
        double x = sigma((int)(i)) / i;
        double y = sigma((int)(N)) / (N * 1.0);
        if (x > y)
            return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    if(isSuperabundant(N))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation to check if 
# a number is Superabundant

# Function to calculate the sum of all
# divisors of a given number
def sigma(n):

    if (n == 1):
        return 1

    # Sum of divisors
    result = 0

    # Find all divisors which divides 'num'
    for i in range(2, pow(n, 1 // 2)):

        # If 'i' is divisor of 'n'
        if (n % i == 0):

            # If both divisors are same
            # then add it once else add
            # both
            if (i == (n / i)):
                result += i
            else:
                result += (i + n / i)

    # Add 1 and n to result as above loop
    # considers proper divisors greater
    # than 1.
    return (result + n + 1)

# Function to check if N is a
# superabundant number
def isSuperabundant(N):

    # To check all numbers from 1 to N
    for i in range(1, N):
        x = sigma((int)(i)) / i
        y = sigma((int)(N)) / (N * 1.0)

        if (x > y):
            return False

    return True

# Driver code
if __name__ == '__main__':

    N = 4

    if (isSuperabundant(N) != True):
        print("Yes")
    else:
        print("No")

# This code is contributed by shikhasingrajput
```

## C#

```
// C# implementation to check if
// a number is Superabundant
using System;

class GFG{

// Function to calculate the sum of
// all divisors of a given number
static int sigma(int n)
{
    if (n == 1)
        return 1;

    // Sum of divisors
    int result = 0;

    // Find all divisors which divides 'num'
    for(int i = 2; i <= Math.Sqrt(n); i++)
    {

        // If 'i' is divisor of 'n'
        if (n % i == 0)
        {

            // If both divisors are same
            // then add it once else add
            // both
            if (i == (n / i))
                result += i;
            else
                result += (i + n / i);
        }
    }

    // Add 1 and n to result as above loop
    // considers proper divisors greater
    // than 1.
    return (result + n + 1);
}

// Function to check if N is a
// superabundant number
static bool isSuperabundant(int N)
{

    // To check all numbers from 1 to N
    for(double i = 1; i < N; i++)
    {
        double x = sigma((int)(i)) / i;
        double y = sigma((int)(N)) / (N * 1.0);
        if (x > y)
            return false;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;

    if(isSuperabundant(N))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation to check if
// a number is Superabundant

// Function to calculate the sum of all
// divisors of a given number
function sigma(n)
{
    if (n == 1)
        return 1;

    // Sum of divisors
    var result = 0;

    // find all divisors which divides 'num'
    for (var i = 2; i <= Math.sqrt(n); i++) {
        // if 'i' is divisor of 'n'
        if (n % i == 0) {

            // if both divisors are same
            // then add it once else add
            // both
            if (i == (n / i))
                result += i;
            else
                result += (i + n / i);
        }
    }

    // Add 1 and n to result as above loop
    // considers proper divisors greater
    // than 1.
    return (result + n + 1);
}

// Function to check if N is a
// superabundant number
function isSuperabundant(N)
{

    // to check all numbers from 1 to N
    for (var i = 1; i < N; i++) {
        var x = sigma(i) / i;
        var y = sigma(N) / (N * 1.0);
        if (x > y)
            return false;
    }
    return true;
}

// Driver code
var N = 4;
isSuperabundant(N) ? document.write( "Yes")
                   : document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**T2【O(n)T4】