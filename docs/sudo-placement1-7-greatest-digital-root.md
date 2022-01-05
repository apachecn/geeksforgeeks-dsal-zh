# Sudo 放置[1.7] |最大数字根

> 原文:[https://www . geesforgeks . org/sudo-placement 1-7-great-digital-root/](https://www.geeksforgeeks.org/sudo-placement1-7-greatest-digital-root/)

给定一个数 N，你需要找到一个除数 N，这样这个除数的数字根是所有其他除数 N 中最大的。如果多个除数给出相同的最大数字根，那么输出最大除数。
一个非负数的数字根，可以通过反复对这个数的位数求和，直到我们达到一个位数来得到。例:digital root(98)= 9+8 =>17 =>1+7 =>8(个位数！).任务是打印具有最大数字根的最大除数，后跟一个空格和该除数的数字根。
**例:**

> **输入:**N = 10
> T3】输出:5 5
> 10 的除数是:1，2，5，10。这些除数的数字根如下:
> 1= > 1，2= > 2，5= > 5，10= > 1。最大的数字根是除数 5 产生的 5，所以答案是 5 5
> **输入:** N = 18
> **输出:**18 9
> 18 的除数是:1，2，3，6，9，18。这些除数的数字根如下:
> 1= > 1，2= > 2，3= > 3，6= > 6，9= > 9，18= > 9。我们可以看到，9 和 18 都有最大的数字根 9。所以我们选择这些除数的最大值，也就是 Max(9，18)=18。所以答案是 18 9

一种天真的方法是迭代到 N，找到所有的因子和它们的 T2 数字和 T3。存储其中最大的并打印出来。
**时间复杂度:** O(N)
一种**高效的方法**是循环直到 **sqrt(N)** ，那么因子将是 I 和 n/i，检查其中最大的[数字和](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)，如果数字和相似，则存储较大的因子。迭代完成后，打印它们。
以下是上述办法的实施情况。

## C++

```
// C++ program to print the
// digital roots of a number
#include <bits/stdc++.h>
using namespace std;

// Function to return
// dig-sum
int summ(int n)
{
    if (n == 0)
        return 0;
    return (n % 9 == 0) ? 9 : (n % 9);
}

// Function to print the Digital Roots
void printDigitalRoot(int n)
{

    // store the largest digital roots
    int maxi = 1;
    int dig = 1;

    // Iterate till sqrt(n)
    for (int i = 1; i <= sqrt(n); i++) {

        // if i is a factor
        if (n % i == 0) {
            // get the digit sum of both
            // factors i and n/i
            int d1 = summ(n / i);
            int d2 = summ(i);

            // if digit sum is greater
            // then previous maximum
            if (d1 > maxi) {
                dig = n / i;
                maxi = d1;
            }

            // if digit sum is greater
            // then previous maximum
            if (d2 > maxi) {
                dig = i;
                maxi = d2;
            }

            // if digit sum is same as
            // then previous maximum, then
            // check for larger divisor
            if (d1 == maxi) {
                if (dig < (n / i)) {
                    dig = n / i;
                    maxi = d1;
                }
            }

            // if digit sum is same as
            // then previous maximum, then
            // check for larger divisor
            if (d2 == maxi) {
                if (dig < i) {
                    dig = i;
                    maxi = d2;
                }
            }
        }
    }

    // Print the digital roots
    cout << dig << " " << maxi << endl;
}

// Driver Code
int main()
{
    int n = 10;

    // Function call to print digital roots
    printDigitalRoot(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the digital
// roots of a number
class GFG
{

// Function to return dig-sum
static int summ(int n)
{
    if (n == 0)
        return 0;
    return (n % 9 == 0) ? 9 : (n % 9);
}

// Function to print the Digital Roots
static void printDigitalRoot(int n)
{

    // store the largest digital roots
    int maxi = 1;
    int dig = 1;

    // Iterate till sqrt(n)
    for (int i = 1; i <= Math.sqrt(n); i++)
    {

        // if i is a factor
        if (n % i == 0)
        {
            // get the digit sum of both
            // factors i and n/i
            int d1 = summ(n / i);
            int d2 = summ(i);

            // if digit sum is greater
            // then previous maximum
            if (d1 > maxi)
            {
                dig = n / i;
                maxi = d1;
            }

            // if digit sum is greater
            // then previous maximum
            if (d2 > maxi)
            {
                dig = i;
                maxi = d2;
            }

            // if digit sum is same as
            // then previous maximum, then
            // check for larger divisor
            if (d1 == maxi)
            {
                if (dig < (n / i))
                {
                    dig = n / i;
                    maxi = d1;
                }
            }

            // if digit sum is same as
            // then previous maximum, then
            // check for larger divisor
            if (d2 == maxi)
            {
                if (dig < i)
                {
                    dig = i;
                    maxi = d2;
                }
            }
        }
    }

    // Print the digital roots
    System.out.println(dig + " " + maxi);
}

// Driver Code
public static void main(String[] args)
{
    int n = 10;

    // Function call to print digital roots
    printDigitalRoot(n);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to print the digital
# roots of a number

# Function to return dig-sum
def summ(n):
    if (n == 0):
        return 0;
    if(n % 9 == 0):
        return 9;
    else:
        return (n % 9);

# Function to print the Digital Roots
def printDigitalRoot(n):

    # store the largest digital roots
    maxi = 1;
    dig = 1;

    # Iterate till sqrt(n)
    for i in range(1, int(pow(n, 1/2) + 1)):

        # if i is a factor
        if (n % i == 0):

            # get the digit sum of both
            # factors i and n/i
            d1 = summ(n / i);
            d2 = summ(i);

            # if digit sum is greater
            # then previous maximum
            if (d1 > maxi):
                dig = n / i;
                maxi = d1;

            # if digit sum is greater
            # then previous maximum
            if (d2 > maxi):
                dig = i;
                maxi = d2;

            # if digit sum is same as
            # then previous maximum, then
            # check for larger divisor
            if (d1 == maxi):
                if (dig < (n / i)):
                    dig = n / i;
                    maxi = d1;

            # if digit sum is same as
            # then previous maximum, then
            # check for larger divisor
            if (d2 == maxi):
                if (dig < i):
                    dig = i;
                    maxi = d2;

    # Print the digital roots
    print(int(dig), " ", int(maxi));

# Driver Code
if __name__ == '__main__':
    n = 10;

    # Function call to prdigital roots
    printDigitalRoot(n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to print the digital
// roots of a number
using System;

class GFG
{

// Function to return dig-sum
static int summ(int n)
{
    if (n == 0)
        return 0;
    return (n % 9 == 0) ? 9 : (n % 9);
}

// Function to print the Digital Roots
static void printDigitalRoot(int n)
{

    // store the largest digital roots
    int maxi = 1;
    int dig = 1;

    // Iterate till sqrt(n)
    for (int i = 1; i <= Math.Sqrt(n); i++)
    {

        // if i is a factor
        if (n % i == 0)
        {
            // get the digit sum of both
            // factors i and n/i
            int d1 = summ(n / i);
            int d2 = summ(i);

            // if digit sum is greater
            // then previous maximum
            if (d1 > maxi)
            {
                dig = n / i;
                maxi = d1;
            }

            // if digit sum is greater
            // then previous maximum
            if (d2 > maxi)
            {
                dig = i;
                maxi = d2;
            }

            // if digit sum is same as
            // then previous maximum, then
            // check for larger divisor
            if (d1 == maxi)
            {
                if (dig < (n / i))
                {
                    dig = n / i;
                    maxi = d1;
                }
            }

            // if digit sum is same as
            // then previous maximum, then
            // check for larger divisor
            if (d2 == maxi)
            {
                if (dig < i)
                {
                    dig = i;
                    maxi = d2;
                }
            }
        }
    }

    // Print the digital roots
    Console.WriteLine(dig + " " + maxi);
}

// Driver Code
public static void Main()
{
    int n = 10;

    // Function call to print digital roots
    printDigitalRoot(n);
}
}

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// javascript program to print the digital
// roots of a number    // Function to return dig-sum
    function summ(n) {
        if (n == 0)
            return 0;
        return (n % 9 == 0) ? 9 : (n % 9);
    }

    // Function to print the Digital Roots
    function printDigitalRoot(n) {

        // store the largest digital roots
        var maxi = 1;
        var dig = 1;

        // Iterate till sqrt(n)
        for (i = 1; i <= Math.sqrt(n); i++) {

            // if i is a factor
            if (n % i == 0) {
                // get the digit sum of both
                // factors i and n/i
                var d1 = summ(n / i);
                var d2 = summ(i);

                // if digit sum is greater
                // then previous maximum
                if (d1 > maxi) {
                    dig = n / i;
                    maxi = d1;
                }

                // if digit sum is greater
                // then previous maximum
                if (d2 > maxi) {
                    dig = i;
                    maxi = d2;
                }

                // if digit sum is same as
                // then previous maximum, then
                // check for larger divisor
                if (d1 == maxi) {
                    if (dig < (n / i)) {
                        dig = n / i;
                        maxi = d1;
                    }
                }

                // if digit sum is same as
                // then previous maximum, then
                // check for larger divisor
                if (d2 == maxi) {
                    if (dig < i) {
                        dig = i;
                        maxi = d2;
                    }
                }
            }
        }

        // Print the digital roots
        document.write(dig + " " + maxi);
    }

    // Driver Code

        var n = 10;

        // Function call to print digital roots
        printDigitalRoot(n);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
5 5
```

**时间复杂度:** O(sqrt(N))