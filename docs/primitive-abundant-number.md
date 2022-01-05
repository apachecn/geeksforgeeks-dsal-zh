# 原始丰富数

> 原文:[https://www.geeksforgeeks.org/primitive-abundant-number/](https://www.geeksforgeeks.org/primitive-abundant-number/)

一个数 **N** 如果 **N** 是一个[丰数](https://www.geeksforgeeks.org/abundant-number/)而它所有的定数都是[亏数](https://www.geeksforgeeks.org/deficient-number)，那么这个数就是本原丰数。
前几个原始丰富数是:

> 20、70、88、104、272、304……

### 检查 N 是否是本原富足数

给定一个数 **N** ，任务是找出这个数是否是本原丰数。
**例:**

> **输入:** N = 20
> **输出:** YES
> **解释:**
> 20 的定数之和为–1+2+4+5+10 = 22>20，
> 所以，20 是一个充裕的数。
> 1、2、4、5 和 10 的适当除数分别是 0、1、3、1 和 8，
> 这些数都是亏数
> 因此，20 是本原丰数。
> **输入:** N = 17
> **输出:**否

**进场:**

1.  检查该数是否为[大数](https://www.geeksforgeeks.org/abundant-number/)，即由和(N)表示的数的所有适当除数之和大于数 N 的值
2.  如果数量不多，则返回 false，否则执行以下操作
3.  检查 N 的所有适当除数是否都是[亏数](https://www.geeksforgeeks.org/deficient-number)，即除数和(N)所表示的数的所有除数之和小于 N 值的两倍
4.  如果以上两个条件都成立，打印**“是”**否则打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above
// approach

#include <bits/stdc++.h>
using namespace std;

// Function to sum of divisors
int getSum(int n)
{
    int sum = 0;

    // Note that this loop
    // runs till square root of N
    for (int i = 1; i <= sqrt(n); i++) {

        if (n % i == 0) {

            // If divisors are equal,
            // take only one of them
            if (n / i == i)
                sum = sum + i;

            else // Otherwise take both
            {
                sum = sum + i;
                sum = sum + (n / i);
            }
        }
    }

    return sum;
}

// Function to check Abundant Number
bool checkAbundant(int n)
{
    // Return true if sum
    // of divisors is greater
    // than N.
    return (getSum(n) - n > n);
}

// Function to check Deficient Number
bool isDeficient(int n)
{
    // Check if sum(n) < 2 * n
    return (getSum(n) < (2 * n));
}

// Function to check all proper divisors
// of N is deficient number or not
bool checkPrimitiveAbundant(int num)
{
    // if number itself is not abundant
    // return false
    if (!checkAbundant(num)) {
        return false;
    }

    // find all divisors which divides 'num'
    for (int i = 2; i <= sqrt(num); i++) {

        // if 'i' is divisor of 'num'
        if (num % i == 0 && i != num) {

            // if both divisors are same then add
            // it only once else add both
            if (i * i == num) {
                if (!isDeficient(i)) {
                    return false;
                }
            }
            else if (!isDeficient(i) || !isDeficient(num / i)) {
                return false;
            }
        }
    }

    return true;
}

// Driver Code
int main()
{

    int n = 20;
    if (checkPrimitiveAbundant(n)) {
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
// Java implementation of the above
// approach
class GFG{

// Function to sum of divisors
static int getSum(int n)
{
    int sum = 0;

    // Note that this loop runs
    // till square root of N
    for(int i = 1; i <= Math.sqrt(n); i++)
    {
       if (n % i == 0)
       {

           // If divisors are equal,
           // take only one of them
           if (n / i == i)
               sum = sum + i;

           // Otherwise take both
           else
           {
               sum = sum + i;
               sum = sum + (n / i);
           }
       }
    }
    return sum;
}

// Function to check Abundant Number
static boolean checkAbundant(int n)
{

    // Return true if sum
    // of divisors is greater
    // than N.
    return (getSum(n) - n > n);
}

// Function to check Deficient Number
static boolean isDeficient(int n)
{

    // Check if sum(n) < 2 * n
    return (getSum(n) < (2 * n));
}

// Function to check all proper divisors
// of N is deficient number or not
static boolean checkPrimitiveAbundant(int num)
{

    // If number itself is not abundant
    // return false
    if (!checkAbundant(num))
    {
        return false;
    }

    // Find all divisors which divides 'num'
    for(int i = 2; i <= Math.sqrt(num); i++)
    {

       // if 'i' is divisor of 'num'
       if (num % i == 0 && i != num)
       {

           // if both divisors are same then
           // add it only once else add both
           if (i * i == num)
           {
               if (!isDeficient(i))
               {
                   return false;
               }
           }
           else if (!isDeficient(i) ||
                    !isDeficient(num / i))
           {
               return false;
           }
       }
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int n = 20;

    if (checkPrimitiveAbundant(n))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 implementation of the above
# approach
import math

# Function to sum of divisors
def getSum(n):
    sum = 0

    # Note that this loop
    # runs till square root of N
    for i in range(1, int(math.sqrt(n) + 1)):
        if (n % i == 0):

            # If divisors are equal,
            # take only one of them
            if (n // i == i):
                sum = sum + i
            else:

                # Otherwise take both
                sum = sum + i
                sum = sum + (n // i)
    return sum

# Function to check Abundant Number
def checkAbundant(n):

    # Return True if sum
    # of divisors is greater
    # than N.
    if (getSum(n) - n > n):
        return True
    return False

# Function to check Deficient Number
def isDeficient(n):

    # Check if sum(n) < 2 * n
    if (getSum(n) < (2 * n)):
        return True
    return False

# Function to check all proper divisors
# of N is deficient number or not
def checkPrimitiveAbundant(num):

    # if number itself is not abundant
    # return False
    if not checkAbundant(num):
        return False

    # find all divisors which divides 'num'
    for i in range(2, int(math.sqrt(num) + 1)):

        # if 'i' is divisor of 'num'
        if (num % i == 0 and i != num):
            # if both divisors are same then add
            # it only once else add both
            if (i * i == num):
                if (not isDeficient(i)):
                    return False
            elif (not isDeficient(i) or
                  not isDeficient(num // i)):
                return False
    return True

# Driver Code
n = 20
if (checkPrimitiveAbundant(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation of the above
// approach
using System;
class GFG{

// Function to sum of divisors
static int getSum(int n)
{
    int sum = 0;

    // Note that this loop runs
    // till square root of N
    for(int i = 1; i <= Math.Sqrt(n); i++)
    {
       if (n % i == 0)
       {

           // If divisors are equal,
           // take only one of them
           if (n / i == i)
               sum = sum + i;

           // Otherwise take both
           else
           {
               sum = sum + i;
               sum = sum + (n / i);
           }
       }
    }
    return sum;
}

// Function to check Abundant Number
static bool checkAbundant(int n)
{

    // Return true if sum
    // of divisors is greater
    // than N.
    return (getSum(n) - n > n);
}

// Function to check Deficient Number
static bool isDeficient(int n)
{

    // Check if sum(n) < 2 * n
    return (getSum(n) < (2 * n));
}

// Function to check all proper divisors
// of N is deficient number or not
static bool checkPrimitiveAbundant(int num)
{

    // If number itself is not abundant
    // return false
    if (!checkAbundant(num))
    {
        return false;
    }

    // Find all divisors which divides 'num'
    for(int i = 2; i <= Math.Sqrt(num); i++)
    {

       // If 'i' is divisor of 'num'
       if (num % i == 0 && i != num)
       {

           // If both divisors are same then
           // add it only once else add both
           if (i * i == num)
           {
               if (!isDeficient(i))
               {
                   return false;
               }
           }
           else if (!isDeficient(i) ||
                    !isDeficient(num / i))
           {
               return false;
           }
       }
    }
    return true;
}

// Driver Code
public static void Main()
{
    int n = 20;

    if (checkPrimitiveAbundant(n))
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
// Javascript implementation of the above
// approach

    // Function to sum of divisors
    function getSum( n) {
        let sum = 0;

        // Note that this loop runs
        // till square root of N
        for ( let i = 1; i <= Math.sqrt(n); i++) {
            if (n % i == 0) {

                // If divisors are equal,
                // take only one of them
                if (n / i == i)
                    sum = sum + i;

                // Otherwise take both
                else {
                    sum = sum + i;
                    sum = sum + (n / i);
                }
            }
        }
        return sum;
    }

    // Function to check Abundant Number
    function checkAbundant( n) {

        // Return true if sum
        // of divisors is greater
        // than N.
        return (getSum(n) - n > n);
    }

    // Function to check Deficient Number
    function isDeficient( n) {

        // Check if sum(n) < 2 * n
        return (getSum(n) < (2 * n));
    }

    // Function to check all proper divisors
    // of N is deficient number or not
    function checkPrimitiveAbundant( num) {

        // If number itself is not abundant
        // return false
        if (!checkAbundant(num)) {
            return false;
        }

        // Find all divisors which divides 'num'
        for ( let i = 2; i <= Math.sqrt(num); i++) {

            // if 'i' is divisor of 'num'
            if (num % i == 0 && i != num) {

                // if both divisors are same then
                // add it only once else add both
                if (i * i == num) {
                    if (!isDeficient(i)) {
                        return false;
                    }
                } else if (!isDeficient(i) || !isDeficient(num / i)) {
                    return false;
                }
            }
        }
        return true;
    }

    // Driver Code

        let n = 20;

        if (checkPrimitiveAbundant(n)) {
            document.write("Yes");
        } else {
            document.write("No");
        }

// This code contributed by aashish1995
</script>
```

**Output:** 

```
Yes
```

时间复杂度:O(N <sup>1/2</sup> )

辅助空间:0(1)

**参考文献:**T2https://en.wikipedia.org/wiki/Primitive_abundant_number