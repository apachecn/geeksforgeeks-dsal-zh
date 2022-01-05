# Tceforp 编号

> 原文:[https://www.geeksforgeeks.org/tcefrep-numbers/](https://www.geeksforgeeks.org/tcefrep-numbers/)

**t efrep 数**一个数 **N** 使得 N
的正因子之和为反(n) =

> 6, 498906, 20671542, 41673714….

### 检查 N 是否是一个 Tcefrep 号码

给定一个编号 **N** ，任务是检查 **N** 是否为 **Tcefrep 编号**。如果 **N** 是 Tcefrep 号，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 498906
> **输出:**是
> **解释:**
> 498906 的适当除数是 1、2、3、6、9、18、27、54、
> 9239、18478、27717、55434、83151、166302、249453、
> 它们的和是 6000

**进场:**

1.  我们会找到 **N** 的真除数之和
2.  我们会发现 **N** 的反义词
3.  然后检查 **N** 的适当因子之和是否等于 **N** 的倒数，如果等于则打印**“是”**否则打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ implementation to check if N
// is a Tcefrep number
#include <bits/stdc++.h>
using namespace std;

// Iterative function to
// reverse digits of num
int reverse(int num)
{
    int rev_num = 0;
    while(num > 0)
    {
        rev_num = rev_num*10 + num%10;
        num = num/10;
    }
    return rev_num;
}

// Function to calculate sum of
// all proper divisors
// num --> given natural number
int properDivSum(int num)
{
    // Final result of summation of divisors
    int result = 0;

    // find all divisors which divides 'num'
    for (int i=2; i<=sqrt(num); i++)
    {
        // if 'i' is divisor of 'num'
        if (num%i==0)
        {
            // if both divisors are same then add
            // it only once else add both
            if (i==(num/i))
                result += i;
            else
                result += (i + num/i);
        }
    }

    // Add 1 to the result as 1 is also a divisor
    return (result + 1);
}

bool isTcefrep(int n)
{
    return properDivSum(n) == reverse(n);
}

// Driver Code
int main()
{
    // Given Number N
    int N = 6;

    // Function Call
    if (isTcefrep(N))
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

// Iterative function to
// reverse digits of num
static int reverse(int num)
{
    int rev_num = 0;
    while(num > 0)
    {
        rev_num = rev_num * 10 + num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to calculate sum of
// all proper divisors
// num --> given natural number
static int properDivSum(int num)
{
    // Final result of summation of divisors
    int result = 0;

    // find all divisors which divides 'num'
    for (int i = 2; i<= Math.sqrt(num); i++)
    {
        // if 'i' is divisor of 'num'
        if (num % i == 0)
        {
            // if both divisors are same then add
            // it only once else add both
            if (i == (num / i))
                result += i;
            else
                result += (i + num / i);
        }
    }

    // Add 1 to the result as 1
    // is also a divisor
    return (result + 1);
}

static boolean isTcefrep(int n)
{
    return properDivSum(n) == reverse(n);
}

// Driver Code
public static void main(String[] args)
{
    int N = 6;

    // Function Call
    if (isTcefrep(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 implementation to check if N
# is a Tcefrep number
import math

# Iterative function to
# reverse digits of num
def reverse(num):
    rev_num = 0
    while(num > 0):
        rev_num = rev_num * 10 + num % 10
        num = num // 10

    return rev_num

# Function to calculate sum of
# all proper divisors
# num --> given natural number
def properDivSum(num):

    # Final result of summation of divisors
    result = 0

    # find all divisors which divides 'num'
    for i in range(2, (int)(math.sqrt(num)) + 1):

        # if 'i' is divisor of 'num'
        if (num % i == 0):

            # if both divisors are same then add
            # it only once else add both
            if (i == (num // i)):
                result += i
            else:
                result += (i + num / i)

    # Add 1 to the result as 1 is also a divisor
    return (result + 1)

def isTcefrep(n):
    return properDivSum(n) == reverse(n);

# Driver Code

# Given Number N
N = 6

# Function Call
if(isTcefrep(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by Sanjit Prasad
```

## C#

```
// C# program for above approach
using System;
class GFG{

// Iterative function to
// reverse digits of num
static int reverse(int num)
{
    int rev_num = 0;
    while(num > 0)
    {
        rev_num = rev_num * 10 + num % 10;
        num = num / 10;
    }
    return rev_num;
}

// Function to calculate sum of
// all proper divisors
// num --> given natural number
static int properDivSum(int num)
{
    // Final result of summation of divisors
    int result = 0;

    // find all divisors which divides 'num'
    for (int i = 2; i<= Math.Sqrt(num); i++)
    {
        // if 'i' is divisor of 'num'
        if (num % i == 0)
        {
            // if both divisors are same then add
            // it only once else add both
            if (i == (num / i))
                result += i;
            else
                result += (i + num / i);
        }
    }

    // Add 1 to the result as 1
    // is also a divisor
    return (result + 1);
}

static bool isTcefrep(int n)
{
    return properDivSum(n) == reverse(n);
}

// Driver Code
public static void Main()
{
    int N = 6;

    // Function Call
    if (isTcefrep(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>

// Javascript program for above approach

    // Iterative function to
    // reverse digits of num
    function reverse( num) {
        let rev_num = 0;
        while (num > 0) {
            rev_num = rev_num * 10 + num % 10;
            num = parseInt(num / 10);
        }
        return rev_num;
    }

    // Function to calculate sum of
    // all proper divisors
    // num --> given natural number
    function properDivSum( num) {
        // Final result of summation of divisors
        let result = 0;

        // find all divisors which divides 'num'
        for ( i = 2; i <= Math.sqrt(num); i++) {
            // if 'i' is divisor of 'num'
            if (num % i == 0) {
                // if both divisors are same then add
                // it only once else add both
                if (i == (num / i))
                    result += i;
                else
                    result += (i + num / i);
            }
        }

        // Add 1 to the result as 1
        // is also a divisor
        return (result + 1);
    }

    function isTcefrep( n) {
        return properDivSum(n) == reverse(n);
    }

    // Driver Code

        let N = 6;

        // Function Call
        if (isTcefrep(N))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***o(n^2)*
t5】参考:[http://www.numbersaplenty.com/set/tcefrep_number/](http://www.numbersaplenty.com/set/tcefrep_number/)T9】