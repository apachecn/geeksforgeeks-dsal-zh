# 令人钦佩的数字

> 原文:[https://www.geeksforgeeks.org/admirable-numbers/](https://www.geeksforgeeks.org/admirable-numbers/)

给定一个整数 **N** ，任务是检查 **N** 是否是一个令人钦佩的数字。

> 一个令人钦佩的数字是一个数字，如果存在一个适当的除数 D ' N，使得σ(N)-2D ' = 2N，其中σ(N)是 N 的所有除数之和

**示例:**

> **输入:** N = 12
> **输出:**是
> **解释:**
> 12 的适当除数是 1、2、3、4、6 和 12
> sigma(N)= 1+2+3+4+6+12 = 28
> sigma(N)–2D ' = 2N
> 28–2 * 2 = 2 * 12
> 24 = = 24
> 
> **输入:**N = 28
> T3】输出:否

**方法:**思路是求一个数的[所有因子之和，即σ(N)。然后我们将找到一个数 D’的所有适当除数，并检查是否存在一个 N 的适当除数 D’](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)

![sigma(N) - 2*D'= 2*N      ](img/f22d432d64f64cb70807c52ad189a571.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现:

## C++

```
// C++ implementation to check if
// N is an admirable number

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum of
// all divisors of a given number
int divSum(int n)
{
    // Sum of divisors
    int result = 0;

    // Find all divisors
    // which divides 'num'
    for (int i = 2; i <= sqrt(n); i++) {

        // if 'i' is divisor of 'n'
        if (n % i == 0) {

            // if both divisors are same
            // then add it once else add
            if (i == (n / i))
                result += i;
            else
                result += (i + n / i);
        }
    }

    // Add 1 and n to result as above loop
    // considers proper divisors greater
    return (result + n + 1);
}

// Function to check if there
// exists a proper divisor
// D' of N such that sigma(n)-2D' = 2N
bool check(int num)
{
    int sigmaN = divSum(num);

    // Find all divisors which divides 'num'
    for (int i = 2; i <= sqrt(num); i++) {

        // if 'i' is divisor of 'num'
        if (num % i == 0) {

            // if both divisors are same then add
            // it only once else add both
            if (i == (num / i)) {
                if (sigmaN - 2 * i == 2 * num)
                    return true;
            }
            else {
                if (sigmaN - 2 * i == 2 * num)
                    return true;
                if (sigmaN - 2 * (num / i) == 2 * num)
                    return true;
            }
        }
    }

    // Check 1 since 1 is also a divisor
    if (sigmaN - 2 * 1 == 2 * num)
        return true;

    return false;
}

// Function to check if N
// is an admirable number
bool isAdmirableNum(int N)
{
    return check(N);
}

// Driver code
int main()
{
    int n = 12;
    if (isAdmirableNum(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if N
// is a admirable number
class GFG{

// Function to calculate the sum of
// all divisors of a given number
static int divSum(int n)
{
    // Sum of divisors
    int result = 0;

    // Find all divisors
    // which divides 'num'
    for (int i = 2; i <= Math.sqrt(n); i++)
    {

        // if 'i' is divisor of 'n'
        if (n % i == 0)
        {

            // if both divisors are same
            // then add it once else add
            if (i == (n / i))
                result += i;
            else
                result += (i + n / i);
        }
    }

    // Add 1 and n to result as above loop
    // considers proper divisors greater
    return (result + n + 1);
}

// Function to check if there
// exists a proper divisor
// D' of N such that sigma(n)-2D' = 2N
static boolean check(int num)
{
    int sigmaN = divSum(num);

    // Find all divisors which divides 'num'
    for (int i = 2; i <= Math.sqrt(num); i++)
    {

        // if 'i' is divisor of 'num'
        if (num % i == 0)
        {

            // if both divisors are same then add
            // it only once else add both
            if (i == (num / i))
            {
                if (sigmaN - 2 * i == 2 * num)
                    return true;
            }
            else
            {
                if (sigmaN - 2 * i == 2 * num)
                    return true;
                if (sigmaN - 2 * (num / i) == 2 * num)
                    return true;
            }
        }
    }

    // Check 1 since 1 is also a divisor
    if (sigmaN - 2 * 1 == 2 * num)
        return true;

    return false;
}

// Function to check if N
// is an admirable number
static boolean isAdmirableNum(int N)
{
    return check(N);
}

// Driver code
public static void main(String[] args)
{
    int n = 12;
    if (isAdmirableNum(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation to check if
# N is an admirable number
import math

# Function to calculate the sum of
# all divisors of a given number
def divSum(n):

    # Sum of divisors
    result = 0

    # Find all divisors
    # which divides 'num'
    for i in range(2, int(math.sqrt(n)) + 1):

        # If 'i' is divisor of 'n'
        if (n % i == 0):

            # If both divisors are same
            # then add it once else add
            if (i == (n // i)):
                result += i
            else:
                result += (i + n // i)

    # Add 1 and n to result as above loop
    # considers proper divisors greater
    return (result + n + 1)

# Function to check if there
# exists a proper divisor
# D' of N such that sigma(n)-2D' = 2N
def check(num):

    sigmaN = divSum(num)

    # Find all divisors which divides 'num'
    for i in range(2, int(math.sqrt(num)) + 1):

        # If 'i' is divisor of 'num'
        if (num % i == 0):

            # If both divisors are same then add
            # it only once else add both
            if (i == (num // i)):
                if (sigmaN - 2 * i == 2 * num):
                    return True

            else:
                if (sigmaN - 2 * i == 2 * num):
                    return True
                if (sigmaN - 2 * (num // i) == 2 * num):
                    return True

    # Check 1 since 1 is also a divisor
    if (sigmaN - 2 * 1 == 2 * num):
        return True

    return False

# Function to check if N
# is an admirable number
def isAdmirableNum(N):

    return check(N)

# Driver code
n = 12

if (isAdmirableNum(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to check if N
// is a admirable number
using System;
class GFG{

// Function to calculate the sum of
// all divisors of a given number
static int divSum(int n)
{

    // Sum of divisors
    int result = 0;

    // Find all divisors
    // which divides 'num'
    for(int i = 2; i <= Math.Sqrt(n); i++)
    {

       // If 'i' is divisor of 'n'
       if (n % i == 0)
       {

           // If both divisors are same
           // then add it once else add
           if (i == (n / i))
               result += i;
           else
               result += (i + n / i);
       }
    }

    // Add 1 and n to result as above loop
    // considers proper divisors greater
    return (result + n + 1);
}

// Function to check if there
// exists a proper divisor
// D' of N such that sigma(n)-2D' = 2N
static bool check(int num)
{
    int sigmaN = divSum(num);

    // Find all divisors which divides 'num'
    for(int i = 2; i <= Math.Sqrt(num); i++)
    {

       // If 'i' is divisor of 'num'
       if (num % i == 0)
       {

           // If both divisors are same then add
           // it only once else add both
           if (i == (num / i))
           {
               if (sigmaN - 2 * i == 2 * num)
                   return true;
           }
           else
           {
               if (sigmaN - 2 * i == 2 * num)
                   return true;
               if (sigmaN - 2 * (num / i) == 2 * num)
                   return true;
           }
       }
    }

    // Check 1 since 1 is also a divisor
    if (sigmaN - 2 * 1 == 2 * num)
        return true;

    return false;
}

// Function to check if N
// is an admirable number
static bool isAdmirableNum(int N)
{
    return check(N);
}

// Driver code
public static void Main()
{
    int n = 12;

    if (isAdmirableNum(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation to check if N
// is a admirable number

    // Function to calculate the sum of
    // all divisors of a given number
    function divSum( n)
    {
        // Sum of divisors
        let result = 0;

        // Find all divisors
        // which divides 'num'
        for ( let i = 2; i <= Math.sqrt(n); i++)
        {

            // if 'i' is divisor of 'n'
            if (n % i == 0)
            {

                // if both divisors are same
                // then add it once else add
                if (i == (n / i))
                    result += i;
                else
                    result += (i + n / i);
            }
        }

        // Add 1 and n to result as above loop
        // considers proper divisors greater
        return (result + n + 1);
    }

    // Function to check if there
    // exists a proper divisor
    // D' of N such that sigma(n)-2D' = 2N
    function check( num) {
        let sigmaN = divSum(num);

        // Find all divisors which divides 'num'
        for (let i = 2; i <= Math.sqrt(num); i++) {

            // if 'i' is divisor of 'num'
            if (num % i == 0) {

                // if both divisors are same then add
                // it only once else add both
                if (i == (num / i)) {
                    if (sigmaN - 2 * i == 2 * num)
                        return true;
                } else {
                    if (sigmaN - 2 * i == 2 * num)
                        return true;
                    if (sigmaN - 2 * (num / i) == 2 * num)
                        return true;
                }
            }
        }

        // Check 1 since 1 is also a divisor
        if (sigmaN - 2 * 1 == 2 * num)
            return true;

        return false;
    }

    // Function to check if N
    // is an admirable number
    function isAdmirableNum( N) {
        return check(N);
    }

    // Driver code
    let n = 12;
    if (isAdmirableNum(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N <sup>1/2</sup>

**参考文献:**[OEIS](https://oeis.org/A111592)T4】