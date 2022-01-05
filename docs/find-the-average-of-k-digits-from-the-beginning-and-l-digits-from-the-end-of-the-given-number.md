# 求给定数字开始的 k 位数和结束的 l 位数的平均值

> 原文:[https://www . geesforgeks . org/find-从给定数字的开头和结尾找到 k 位数的平均值/](https://www.geeksforgeeks.org/find-the-average-of-k-digits-from-the-beginning-and-l-digits-from-the-end-of-the-given-number/)

给定三个整数 **N** 、 **K** 和 **L** 。任务是找到给定编号 **N** 的前 **K** 位和后 **L** 位的平均值，没有任何数字重叠。
**示例:**

> **输入:** N = 123456，K = 2，L = 3
> **输出:** 3.0
> 前 K 位之和为 1 + 2 = 3
> 后 L 位之和为 4 + 5 + 6 = 15
> 平均值= (3 + 15) / (2 + 3) = 18 / 5 = 3
> **输入:** N = 456966，K = 1，L = 1 【T11

**方法:**如果 n 中的位数小于 **(K + L)** ，则不可能找到没有位数重叠的平均值，打印 **-1** 。如果不是这样，求 **N** 的最后 **L** 位的和，存入一个变量，比如 **sum1** ，然后求 **N** 的第一个 **K** 位的和，存入 **sum2** 。现在，将平均值打印为 **(sum1 + sum2) / (K + L)** 。
以下是上述办法的实施:

## C++

```
// implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of digits in num
int countDigits(int num)
{
    int cnt = 0;
    while (num > 0)
    {
        cnt++;
        num /= 10;
    }
    return cnt;
}

// Function to return the sum
// of first n digits of num
int sumFromStart(int num, int n, int rem)
{

    // Remove the unnecessary digits
    num /= ((int)pow(10, rem));

    int sum = 0;
    while (num > 0)
    {
        sum += (num % 10);
        num /= 10;
    }
    return sum;
}

// Function to return the sum
// of the last n digits of num
int sumFromEnd(int num, int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
    {
        sum += (num % 10);
        num /= 10;
    }
    return sum;
}

float getAverage(int n, int k, int l)
{

    // If the average can't be calculated without
    // using the same digit more than once
    int totalDigits = countDigits(n);
    if (totalDigits < (k + l))
        return -1;

    // Sum of the last l digits of n
    int sum1 = sumFromEnd(n, l);

    // Sum of the first k digits of n
    // (totalDigits - k) must be removed from the
    // end of the number to get the remaining
    // k digits from the beginning
    int sum2 = sumFromStart(n, k, totalDigits - k);

    // Return the average
    return ((float)(sum1 + sum2) / 
            (float)(k + l));
}

// Driver code
int main()
{
    int n = 123456, k = 2, l = 3;
    cout << getAverage(n, k, l);

    return 0;
}

// This code is contributed by PrinciRaj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count
    // of digits in num
    public static int countDigits(int num)
    {
        int cnt = 0;
        while (num > 0) {
            cnt++;
            num /= 10;
        }
        return cnt;
    }

    // Function to return the sum
    // of first n digits of num
    public static int sumFromStart(int num, int n, int rem)
    {

        // Remove the unnecessary digits
        num /= ((int)Math.pow(10, rem));

        int sum = 0;
        while (num > 0) {
            sum += (num % 10);
            num /= 10;
        }
        return sum;
    }

    // Function to return the sum
    // of the last n digits of num
    public static int sumFromEnd(int num, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum += (num % 10);
            num /= 10;
        }
        return sum;
    }

    public static float getAverage(int n, int k, int l)
    {

        // If the average can't be calculated without
        // using the same digit more than once
        int totalDigits = countDigits(n);
        if (totalDigits < (k + l))
            return -1;

        // Sum of the last l digits of n
        int sum1 = sumFromEnd(n, l);

        // Sum of the first k digits of n
        // (totalDigits - k) must be removed from the
        // end of the number to get the remaining
        // k digits from the beginning
        int sum2 = sumFromStart(n, k, totalDigits - k);

        // Return the average
        return ((float)(sum1 + sum2) / (float)(k + l));
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 123456, k = 2, l = 3;
        System.out.print(getAverage(n, k, l));
    }
}
```

## 蟒蛇 3

```
# implementation of the approach
from math import pow

# Function to return the count
# of digits in num
def countDigits(num):
    cnt = 0
    while (num > 0):
        cnt += 1
        num //= 10
    return cnt

# Function to return the sum
# of first n digits of num
def sumFromStart(num, n, rem):

    # Remove the unnecessary digits
    num //= pow(10, rem)

    sum = 0
    while (num > 0):
        sum += (num % 10)
        num //= 10
    return sum

# Function to return the sum
# of the last n digits of num
def sumFromEnd(num, n):
    sum = 0
    for i in range(n):
        sum += (num % 10)
        num //= 10

    return sum

def getAverage(n, k, l):

    # If the average can't be calculated without
    # using the same digit more than once
    totalDigits = countDigits(n)
    if (totalDigits < (k + l)):
        return -1

    # Sum of the last l digits of n
    sum1 = sumFromEnd(n, l)

    # Sum of the first k digits of n
    # (totalDigits - k) must be removed from the
    # end of the number to get the remaining
    # k digits from the beginning
    sum2 = sumFromStart(n, k, totalDigits - k)

    # Return the average
    return (sum1 + sum2) / (k + l)

# Driver code
if __name__ == '__main__':
    n = 123456
    k = 2
    l = 3
    print(getAverage(n, k, l))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of digits in num
    public static int countDigits(int num)
    {
        int cnt = 0;
        while (num > 0)
        {
            cnt++;
            num /= 10;
        }
        return cnt;
    }

    // Function to return the sum
    // of first n digits of num
    public static int sumFromStart(int num,
                                   int n, int rem)
    {

        // Remove the unnecessary digits
        num /= ((int)Math.Pow(10, rem));

        int sum = 0;
        while (num > 0)
        {
            sum += (num % 10);
            num /= 10;
        }
        return sum;
    }

    // Function to return the sum
    // of the last n digits of num
    public static int sumFromEnd(int num, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum += (num % 10);
            num /= 10;
        }
        return sum;
    }

    public static float getAverage(int n, int k, int l)
    {

        // If the average can't be calculated without
        // using the same digit more than once
        int totalDigits = countDigits(n);
        if (totalDigits < (k + l))
            return -1;

        // Sum of the last l digits of n
        int sum1 = sumFromEnd(n, l);

        // Sum of the first k digits of n
        // (totalDigits - k) must be removed from the
        // end of the number to get the remaining
        // k digits from the beginning
        int sum2 = sumFromStart(n, k, totalDigits - k);

        // Return the average
        return ((float)(sum1 + sum2) /
                (float)(k + l));
    }

    // Driver code
    public static void Main(String []args)
    {
        int n = 123456, k = 2, l = 3;
        Console.WriteLine(getAverage(n, k, l));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript implementation of the approach   

    // Function to return the count
    // of digits in num
    function countDigits(num)
    {
        var cnt = 0;
        while (num > 0)
        {
            cnt++;
            num = parseInt(num/10);
        }
        return cnt;
    }

    // Function to return the sum
    // of first n digits of num
    function sumFromStart(num, n, rem)
    {

        // Remove the unnecessary digits
        num = (parseInt( num/Math.pow(10, rem)));

        var sum = 0;
        while (num > 0)
        {
            sum += (num % 10);
            num = parseInt(num/10);
        }
        return sum;
    }

    // Function to return the sum
    // of the last n digits of num
    function sumFromEnd(num , n)
    {
        var sum = 0;
        for (i = 0; i < n; i++)
        {
            sum += (num % 10);
            num = parseInt(num/10);
        }
        return sum;
    }

    function getAverage(n , k , l) {

        // If the average can't be calculated without
        // using the same digit more than once
        var totalDigits = countDigits(n);
        if (totalDigits < (k + l))
            return -1;

        // Sum of the last l digits of n
        var sum1 = sumFromEnd(n, l);

        // Sum of the first k digits of n
        // (totalDigits - k) must be removed from the
        // end of the number to get the remaining
        // k digits from the beginning
        var sum2 = sumFromStart(n, k, totalDigits - k);

        // Return the average
        return ( (sum1 + sum2) /  (k + l));
    }

    // Driver code
    var n = 123456, k = 2, l = 3;
    document.write(getAverage(n, k, l));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
3.6
```