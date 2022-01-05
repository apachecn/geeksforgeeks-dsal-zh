# 检查一个数字是否是好素数

> 原文:[https://www . geesforgeks . org/check-a-number-good-prime-or-not/](https://www.geeksforgeeks.org/check-whether-a-number-is-good-prime-or-not/)

给定一个正整数 **N** ，任务是检查给定的数字是否为**好素数**。如果给定的数字是好的主打印'**是**'否则打印'**否**。

> **好素数:**在数学中，好素数是在素数序列中，其平方大于前后相同位置任意两个素数之积的素数。换句话说，一个质数 **Pn** 如果是每一个**1<= I<n**的![Pn^2 > P(n-i) . P(n+1)      ](img/11ea96be785b5b79f7ed8fea946f55d9.png "Rendered by QuickLaTeX.com")就被认为是好质数
> 
> 前几个好素数是:5，11，17，29，37，41，53，59，67，71，97，101，127，149，179，191，223，…

**示例:**

> **输入:** N = 5
> **输出:** YES
> **解释:** 5 是一个好的素数
> 因为 5^2 = 25 大于 3.7 = 21
> 和 2.11 = 22。
> 
> **输入:** N = 20
> **输出:**否

**进场:**

1.得到数字 n。

2.初始化上一个素数= N-1 和下一个素数= N+1

3.当 prev_prime 大于或等于 2 时迭代循环。并检查 next_prime 和 prev_prime 是否都是不使用[素数的素数。](https://www.geeksforgeeks.org/prime-numbers/)

4.如果两者都不是质数，则重复步骤 2 和 3。

5.如果 next_prime 和 prev_prime 都是 prime，那么检查 **N^2 > next_prime。prev_prime** 与否。

*   如果不是，则数字不是好质数，停止执行并返回否
*   如果是，则重复步骤 2、3、4 和 5。

下面是上述方法的实现:

## C++

```
// C++ program to check if a number
// is good prime or not
#include<bits/stdc++.h>
using namespace std;

// Function to check if a
// number is Prime or not
bool isPrime (int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can
    // skip middle five numbers in loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i += 6)
    {
       if (n % i == 0 || n % (i + 2) == 0)
           return false;
    }
    return true;
}

// Function to check if the
// given number is Good prime
bool isGoodprime (int n)
{

    // Smallest good prime is 5
    // So the number less than 5
    // can not be a Good prime

    if (n < 5)
        return false;

    int prev_prime = n - 1;
    int next_prime = n + 1;

    while (prev_prime >= 2)
    {

        // Calculate first prime number < n
        while (!isPrime(prev_prime))
        {
            prev_prime--;
        }

        // Calculate first prime number > n
        while (!isPrime(next_prime))
        {
            next_prime++;
        }

        // Check if product of next_prime
        // and prev_prime is less than n^2
        if ((prev_prime * next_prime) >= n * n)
            return false;

        prev_prime -= 1;
        next_prime += 1;
    }
    return true;
}

// Driver code
int main()
{
    int n = 11;

    if (isGoodprime(n))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}

// This code is contributed by himanshu77
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is
// good prime or not
class GFG{

// Function to check if a
// number is prime or not
static boolean isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
    {
       if (n % i == 0 || n % (i + 2) == 0)
       {
           return false;
       }
    }
    return true;
}

// Function to check if the given
// number is good prime or not
static boolean isGoodrprime(int n)
{

    // Smallest good prime is 5
    // So the number less than 5
    // can not be a good prime

    if (n < 5)
        return false;

    int prev_prime = n - 1;
    int next_prime = n + 1;

    while (prev_prime >= 2)
    {

        // Calculate first prime number < n
        while (!isPrime(prev_prime))
        {
            prev_prime--;
        }

        // Calculate first prime number > n
        while (!isPrime(next_prime))
        {
            next_prime++;
        }

        // Check if product of next_prime
        // and prev_prime
        // is less than n^2
        if ((prev_prime * next_prime) >= n * n)
            return false;

        prev_prime -= 1;
        next_prime += 1;
    }
    return true;
}

// Driver code
public static void main(String []args)
{
    int n = 11;

    if (isGoodrprime(n))
        System.out.println("YES");
    else
        System.out.println("NO");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to check if a number is
# good prime or not

# Utility function to check
# if a number is prime or not
def isPrime(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    i = 5
    while (i * i <= n):
        if (n % i == 0 or n % (i + 2) == 0):
            return False
        i = i + 6
    return True

# Function to check if the given number
# is good prime or not
def isGoodrPrime(n):

    # Declaring variables as global
    global next_prime, prev_prime

    # Smallest good prime is 5
    # So the number less than 5
    # can not be a good prime
    if(n < 5):
        return False

    # Initialize previous_prime to n - 1
    # and next_prime to n + 1
    prev_prime = n - 1
    next_prime = n + 1

    while(prev_prime >= 2):

        # Calculate first prime number < n
        while (not isPrime(prev_prime)):
            prev_prime -= 1

        # Calculate first prime number > n
        while(not isPrime(next_prime)):
            next_prime += 1

        # Check if product of next_prime
        # and prev_prime
        # is less than n^2
        if((prev_prime * next_prime) >= n * n):
            return False

        prev_prime -= 1
        next_prime += 1

    return True

# Driver code
if __name__ == '__main__':

    n = 11

    if(isGoodrPrime(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to check if a number is
// good prime  or not

using System;
class GFG {

    // Function to check if a
    // number is prime or not
    static bool isPrime(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6) {
            if (n % i == 0 || n % (i + 2) == 0) {
                return false;
            }
        }
        return true;
    }

    // Function to check
    // if the given number is good prime or not
    static bool isGoodrprime(int n)
    {

        // Smallest good prime is 5
        // So the number less than 5
        // can not be a good prime

        if (n < 5)
            return false;

        int prev_prime = n - 1;
        int next_prime = n + 1;

        while (prev_prime >= 2) {
            // Calculate first prime number < n
            while (!isPrime(prev_prime)) {
                prev_prime--;
            }

            // Calculate first prime number > n
            while (!isPrime(next_prime)) {
                next_prime++;
            }

            // check if product of next_prime
            // and prev_prime
            // is less than n^2

            if ((prev_prime * next_prime)
                >= n * n)
                return false;

            prev_prime -= 1;
            next_prime += 1;
        }
        return true;
    }

    public static void Main()
    {

        int n = 11;
        if (isGoodrprime(n))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}
```

## java 描述语言

```
<script>

// Javascript program to check if a number
// is good prime or not

// Function to check if a
// number is Prime or not
function isPrime (n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can
    // skip middle five numbers in loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(let i = 5; i * i <= n; i += 6)
    {
    if (n % i == 0 || n % (i + 2) == 0)
        return false;
    }
    return true;
}

// Function to check if the
// given number is Good prime

function isGoodprime (n)
{

    // Smallest good prime is 5
    // So the number less than 5
    // can not be a Good prime

    if (n < 5)
        return false;

    let prev_prime = n - 1;
    let next_prime = n + 1;

    while (prev_prime >= 2)
    {

        // Calculate first prime number < n
        while (!isPrime(prev_prime))
        {
            prev_prime--;
        }

        // Calculate first prime number > n
        while (!isPrime(next_prime))
        {
            next_prime++;
        }

        // Check if product of next_prime
        // and prev_prime is less than n^2
        if ((prev_prime * next_prime) >= n * n)
            return false;

        prev_prime -= 1;
        next_prime += 1;
    }
    return true;
}

// Driver code

    let n = 11;

    if (isGoodprime(n))
        document.write("YES");
    else
        document.write("NO");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(n <sup>3/2</sup> )*

***辅助空间:** O(1)*