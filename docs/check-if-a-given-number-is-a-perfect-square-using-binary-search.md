# 使用二分搜索法

检查给定的数字是否是完美的正方形

> 原文:[https://www . geesforgeks . org/check-if-a-给定的数字是一个完美的正方形-使用-binary-search/](https://www.geeksforgeeks.org/check-if-a-given-number-is-a-perfect-square-using-binary-search/)

检查给定的数字 **N** 是否是一个完美的正方形。如果是，那么返回它是一个完美正方形的数字，否则打印-1。

**示例:**

> **输入:** N = 4900
> **输出** 70
> **说明:**
> 4900 是 70 的完美平方数，因为 70 * 70 = 4900
> 
> **输入:** N = 81
> **输出:** 9
> **说明:**
> 81 是 9 的完美平方数，因为 9 * 9 = 81

**方法:**为了解决上述问题，我们将使用[二分搜索法算法。](https://www.geeksforgeeks.org/binary-search/)

*   从开始和最后一个值找到中间元素，并将中间(中间*中间)的平方值与 n 进行比较。
*   如果它相等，则返回 mid，否则检查正方形(mid*mid)是否**大于 N** ，然后使用相同的开始值递归调用，但最后更改为 mid-1 值，如果正方形(mid*mid)小于 N ，则使用相同的最后值但更改了开始值递归调用。
*   如果 N 不是平方根，则返回-1。

下面是上述方法的实现:

## C++

```
// C++ program to check if a
// given number is Perfect
// square using Binary Search

#include <iostream>
using namespace std;

// function to check for
// perfect square number
int checkPerfectSquare(
    long int N,
    long int start,
    long int last)
{
    // Find the mid value
    // from start and last
    long int mid = (start + last) / 2;

    if (start > last) {
        return -1;
    }

    // check if we got the number which
    // is square root of the perfect
    // square number N
    if (mid * mid == N) {
        return mid;
    }

    // if the square(mid) is greater than N
    // it means only lower values then mid
    // will be possibly the square root of N
    else if (mid * mid > N) {
        return checkPerfectSquare(
            N, start, mid - 1);
    }

    // if the square(mid) is less than N
    // it means only higher values then mid
    // will be possibly the square root of N
    else {
        return checkPerfectSquare(
            N, mid + 1, last);
    }
}

// Driver code
int main()
{
    long int N = 65;

    cout << checkPerfectSquare(N, 1, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// given number is Perfect
// square using Binary Search
import java.util.*;

class GFG {

// Function to check for
// perfect square number
static int checkPerfectSquare(long N,
                              long start,
                              long last)
{
    // Find the mid value
    // from start and last
    long mid = (start + last) / 2;

    if (start > last)
    {
        return -1;
    }

    // Check if we got the number which
    // is square root of the perfect
    // square number N
    if (mid * mid == N)
    {
        return (int)mid;
    }

    // If the square(mid) is greater than N
    // it means only lower values then mid
    // will be possibly the square root of N
    else if (mid * mid > N)
    {
        return checkPerfectSquare(N, start,
                                  mid - 1);
    }

    // If the square(mid) is less than N
    // it means only higher values then mid
    // will be possibly the square root of N
    else
    {
        return checkPerfectSquare(N, mid + 1,
                                  last);
    }
}

// Driver code
public static void main(String[] args)
{
    long N = 65;
    System.out.println(checkPerfectSquare(N, 1, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to check if a
# given number is perfect
# square using Binary Search

# Function to check for
# perfect square number
def checkPerfectSquare(N, start, last):

    # Find the mid value
    # from start and last
    mid = int((start + last) / 2)

    if (start > last):
        return -1

    # Check if we got the number which
    # is square root of the perfect
    # square number N
    if (mid * mid == N):
        return mid

    # If the square(mid) is greater than N
    # it means only lower values then mid
    # will be possibly the square root of N
    elif (mid * mid > N):
        return checkPerfectSquare(N, start,
                                  mid - 1)

    # If the square(mid) is less than N
    # it means only higher values then mid
    # will be possibly the square root of N
    else:
        return checkPerfectSquare(N, mid + 1,
                                  last)

# Driver code
N = 65
print (checkPerfectSquare(N, 1, N))

# This code is contributed by PratikBasu
```

## C#

```
// C# program to check if a
// given number is Perfect
// square using Binary Search
using System;

class GFG{

// Function to check for
// perfect square number
public static int checkPerfectSquare(int N,
                                     int start,
                                     int last)
{
    // Find the mid value
    // from start and last
    int mid = (start + last) / 2;

    if (start > last)
    {
        return -1;
    }

    // Check if we got the number which
    // is square root of the perfect
    // square number N
    if (mid * mid == N)
    {
        return mid;
    }

    // If the square(mid) is greater than N
    // it means only lower values then mid
    // will be possibly the square root of N
    else if (mid * mid > N)
    {
        return checkPerfectSquare(N, start,
                                  mid - 1);
    }

    // If the square(mid) is less than N
    // it means only higher values then mid
    // will be possibly the square root of N
    else
    {
        return checkPerfectSquare(N, mid + 1,
                                  last);
    }
}

// Driver code
public static int Main()
{
    int N = 65;

    Console.Write(checkPerfectSquare(N, 1, N));
    return 0;
}
}

// This code is contributed by sayesha
```

## java 描述语言

```
<script>

// Javascript program to check if a
// given number is Perfect
// square using Binary Search

// Function to check for
// perfect square number
function checkPerfectSquare(N, start, last)
{

    // Find the mid value
    // from start and last
    let mid = parseInt((start + last) / 2);

    if (start > last)
    {
        return -1;
    }

    // Check if we got the number which
    // is square root of the perfect
    // square number N
    if (mid * mid == N)
    {
        return mid;
    }

    // If the square(mid) is greater than N
    // it means only lower values then mid
    // will be possibly the square root of N
    else if (mid * mid > N)
    {
        return checkPerfectSquare(
            N, start, mid - 1);
    }

    // If the square(mid) is less than N
    // it means only higher values then mid
    // will be possibly the square root of N
    else
    {
        return checkPerfectSquare(
            N, mid + 1, last);
    }
}

// Driver code
let N = 65;

document.write(checkPerfectSquare(N, 1, N));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
-1
```

***时间复杂度:** O(Logn)*