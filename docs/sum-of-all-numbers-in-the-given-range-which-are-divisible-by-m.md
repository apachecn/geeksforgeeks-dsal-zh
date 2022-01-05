# 给定范围内可被 M 整除的所有数字之和

> 原文:[https://www . geesforgeks . org/给定范围内可被 m 整除的所有数字的总和/](https://www.geeksforgeeks.org/sum-of-all-numbers-in-the-given-range-which-are-divisible-by-m/)

给定三个数字 **A，B** 和 **M** ，使得 **A < B** ，任务是在**【A，B】**范围内找到可被 M 整除的数字**之和。**

示例:

> **输入:** A = 25，B = 100，M = 30
> **输出:** 180
> **说明:**
> 在给定的范围内【25，100】30，60，90 是可以被 M = 30
> 整除的数，因此，这些数的和= 180。
> 
> **输入:** A = 6，B = 15，M = 3
> **输出:** 42
> **说明:**
> 在给定的范围内【6，15】6，9，12，15 是可被 M = 3 整除的数。
> 因此，这些数字之和= 42。

***天真方法:*** 检查[A，B]范围内的每个数字是否能被 M 整除。最后，把所有能被 m 整除的数字相加。

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of numbers
// divisible by M in the given range

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of numbers
// divisible by M in the given range
int sumDivisibles(int A, int B, int M)
{
    // Variable to store the sum
    int sum = 0;

    // Running a loop from A to B and check
    // if a number is divisible by i.
    for (int i = A; i <= B; i++)

        // If the number is divisible,
        // then add it to sum
        if (i % M == 0)
            sum += i;

    // Return the sum
    return sum;
}

// Driver code
int main()
{
    // A and B define the range
    // M is the dividend
    int A = 6, B = 15, M = 3;

    // Printing the result
    cout << sumDivisibles(A, B, M) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of numbers
// divisible by M in the given range
import java.util.*;

class GFG{

// Function to find the sum of numbers
// divisible by M in the given range
static int sumDivisibles(int A, int B, int M)
{
    // Variable to store the sum
    int sum = 0;

    // Running a loop from A to B and check
    // if a number is divisible by i.
    for (int i = A; i <= B; i++)

        // If the number is divisible,
        // then add it to sum
        if (i % M == 0)
            sum += i;

    // Return the sum
    return sum;
}

// Driver code
public static void main(String[] args)
{
    // A and B define the range
    // M is the dividend
    int A = 6, B = 15, M = 3;

    // Printing the result
    System.out.print(sumDivisibles(A, B, M) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find the sum of numbers
# divisible by M in the given range

# Function to find the sum of numbers
# divisible by M in the given range
def sumDivisibles(A, B, M):

    # Variable to store the sum
    sum = 0

    # Running a loop from A to B and check
    # if a number is divisible by i.
    for i in range(A, B + 1):

        # If the number is divisible,
        # then add it to sum
        if (i % M == 0):
            sum += i

    # Return the sum
    return sum

# Driver code
if __name__=="__main__":

    # A and B define the range
    # M is the dividend
    A = 6
    B = 15
    M = 3

    # Printing the result
    print(sumDivisibles(A, B, M))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the sum of numbers
// divisible by M in the given range
using System;

class GFG{

// Function to find the sum of numbers
// divisible by M in the given range
static int sumDivisibles(int A, int B, int M)
{
    // Variable to store the sum
    int sum = 0;

    // Running a loop from A to B and check
    // if a number is divisible by i.
    for (int i = A; i <= B; i++)

        // If the number is divisible,
        // then add it to sum
        if (i % M == 0)
            sum += i;

    // Return the sum
    return sum;
}

// Driver code
public static void Main(String[] args)
{
    // A and B define the range
    // M is the dividend
    int A = 6, B = 15, M = 3;

    // Printing the result
    Console.Write(sumDivisibles(A, B, M) +"\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find the sum of numbers
// divisible by M in the given range

// Function to find the sum of numbers
// divisible by M in the given range
function sumDivisibles(A, B, M)
{

    // Variable to store the sum
    var sum = 0;

    // Running a loop from A to B and check
    // if a number is divisible by i.
    for(var i = A; i <= B; i++)

        // If the number is divisible,
        // then add it to sum
        if (i % M == 0)
            sum += i;

    // Return the sum
    return sum;
}

// Driver code

// A and B define the range
// M is the dividend
var A = 6, B = 15, M = 3;

// Printing the result
document.write(sumDivisibles(A, B, M));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
42
```

**时间复杂度:** O(N)。
***高效方法:*** 想法是使用[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)和可除性的概念。

*   通过可视化，可以看到 M 的倍数形成一个系列

```
M, 2M, 3M, ...
```

*   如果我们能找到可被 M 整除的范围[A，B]中的第一项 K 的值，那么直接，级数将是:

```
K, (K + M), (K + 2M), ------  (K + (N - 1)*M )
where N is the number of elements in the series. 
```

*   因此，级数中的第一项**‘K’**只不过是小于或等于 A 的最大[数，可被 m](https://www.geeksforgeeks.org/largest-number-smaller-than-or-equal-to-n-divisible-by-k/)整除
*   同样，最后一项是大于或等于 B 的[最小数，可被 M](https://www.geeksforgeeks.org/smallest-number-greater-than-or-equal-to-n-divisible-by-k/) 整除。
*   但是，如果上面的任何一个数字超出了范围，那么我们可以直接从中减去 M，使其进入范围。
*   并且，可被 M 整除的项数可以通过以下公式计算出来:

```
N = B / M - (A - 1)/ M
```

*   因此，这些元素的总和可以通过下式求出:

```
sum = N * ( (first term + last term) / 2)
```

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of numbers
// divisible by M in the given range

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest number
// smaller than or equal to N
// that is divisible by K
int findSmallNum(int N, int K)
{
    // Finding the remainder when N is
    // divided by K
    int rem = N % K;

    // If the remainder is 0, then the
    // number itself is divisible by K
    if (rem == 0)
        return N;
    else

        // Else, then the difference between
        // N and remainder is the largest number
        // which is divisible by K
        return N - rem;
}

// Function to find the smallest number
// greater than or equal to N
// that is divisible by K
int findLargeNum(int N, int K)
{
    // Finding the remainder when N is
    // divided by K
    int rem = (N + K) % K;

    // If the remainder is 0, then the
    // number itself is divisible by K
    if (rem == 0)
        return N;
    else

        // Else, then the difference between
        // N and remainder is the largest number
        // which is divisible by K
        return N + K - rem;
}

// Function to find the sum of numbers
// divisible by M in the given range
int sumDivisibles(int A, int B, int M)
{
    // Variable to store the sum
    int sum = 0;
    int first = findSmallNum(A, M);
    int last = findLargeNum(B, M);

    // To bring the smallest and largest
    // numbers in the range [A, B]
    if (first < A)
        first += M;

    if (last > B)
        first -= M;

    // To count the number of terms in the AP
    int n = (B / M) - (A - 1) / M;

    // Sum of n terms of an AP
    return n * (first + last) / 2;
}

// Driver code
int main()
{
    // A and B define the range,
    // M is the dividend
    int A = 6, B = 15, M = 3;

    // Printing the result
    cout << sumDivisibles(A, B, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of numbers
// divisible by M in the given range

class GFG{

// Function to find the largest number
// smaller than or equal to N
// that is divisible by K
static int findSmallNum(int N, int K)
{
    // Finding the remainder when N is
    // divided by K
    int rem = N % K;

    // If the remainder is 0, then the
    // number itself is divisible by K
    if (rem == 0)
        return N;
    else

        // Else, then the difference between
        // N and remainder is the largest number
        // which is divisible by K
        return N - rem;
}

// Function to find the smallest number
// greater than or equal to N
// that is divisible by K
static int findLargeNum(int N, int K)
{
    // Finding the remainder when N is
    // divided by K
    int rem = (N + K) % K;

    // If the remainder is 0, then the
    // number itself is divisible by K
    if (rem == 0)
        return N;
    else

        // Else, then the difference between
        // N and remainder is the largest number
        // which is divisible by K
        return N + K - rem;
}

// Function to find the sum of numbers
// divisible by M in the given range
static int sumDivisibles(int A, int B, int M)
{
    // Variable to store the sum
    int first = findSmallNum(A, M);
    int last = findLargeNum(B, M);

    // To bring the smallest and largest
    // numbers in the range [A, B]
    if (first < A)
        first += M;

    if (last > B)
        first -= M;

    // To count the number of terms in the AP
    int n = (B / M) - (A - 1) / M;

    // Sum of n terms of an AP
    return n * (first + last) / 2;
}

// Driver code
public static void main(String[] args)
{
    // A and B define the range,
    // M is the dividend
    int A = 6, B = 15, M = 3;

    // Printing the result
    System.out.print(sumDivisibles(A, B, M));

}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the sum of numbers
# divisible by M in the given range

# Function to find the largest number
# smaller than or equal to N
# that is divisible by K
def findSmallNum(N, K):

    # Finding the remainder when N is
    # divided by K
    rem = N % K

    # If the remainder is 0, then the
    # number itself is divisible by K
    if (rem == 0):
        return N
    else:
        # Else, then the difference between
        # N and remainder is the largest number
        # which is divisible by K
        return N - rem

# Function to find the smallest number
# greater than or equal to N
# that is divisible by K
def findLargeNum(N, K):

    # Finding the remainder when N is
    # divided by K
    rem = (N + K) % K

    # If the remainder is 0, then the
    # number itself is divisible by K
    if (rem == 0):
        return N
    else:
        # Else, then the difference between
        # N and remainder is the largest number
        # which is divisible by K
        return N + K - rem

# Function to find the sum of numbers
# divisible by M in the given range
def sumDivisibles(A, B, M):

    # Variable to store the sum
    sum = 0
    first = findSmallNum(A, M)
    last = findLargeNum(B, M)

    # To bring the smallest and largest
    # numbers in the range [A, B]
    if (first < A):
        first += M

    if (last > B):
        first -= M

    # To count the number of terms in the AP
    n = (B // M) - (A - 1) // M

    # Sum of n terms of an AP
    return n * (first + last) // 2

# Driver code
if __name__ == '__main__':

    # A and B define the range,
    # M is the dividend
    A = 6
    B = 15
    M = 3

    # Printing the result
    print(sumDivisibles(A, B, M))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to find the sum of numbers
// divisible by M in the given range
using System;
using System.Collections.Generic;

class GFG{

// Function to find the largest number
// smaller than or equal to N
// that is divisible by K
static int findSmallNum(int N, int K)
{
    // Finding the remainder when N is
    // divided by K
    int rem = N % K;

    // If the remainder is 0, then the
    // number itself is divisible by K
    if (rem == 0)
        return N;
    else

        // Else, then the difference between
        // N and remainder is the largest number
        // which is divisible by K
        return N - rem;
}

// Function to find the smallest number
// greater than or equal to N
// that is divisible by K
static int findLargeNum(int N, int K)
{
    // Finding the remainder when N is
    // divided by K
    int rem = (N + K) % K;

    // If the remainder is 0, then the
    // number itself is divisible by K
    if (rem == 0)
        return N;
    else

        // Else, then the difference between
        // N and remainder is the largest number
        // which is divisible by K
        return N + K - rem;
}

// Function to find the sum of numbers
// divisible by M in the given range
static int sumDivisibles(int A, int B, int M)
{
    // Variable to store the sum
    int first = findSmallNum(A, M);
    int last = findLargeNum(B, M);

    // To bring the smallest and largest
    // numbers in the range [A, B]
    if (first < A)
        first += M;

    if (last > B)
        first -= M;

    // To count the number of terms in the AP
    int n = (B / M) - (A - 1) / M;

    // Sum of n terms of an AP
    return n * (first + last) / 2;
}

// Driver code
public static void Main(String[] args)
{
    // A and B define the range,
    // M is the dividend
    int A = 6, B = 15, M = 3;

    // Printing the result
    Console.Write(sumDivisibles(A, B, M));

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find the sum of numbers
// divisible by M in the given range

// Function to find the largest number
// smaller than or equal to N
// that is divisible by K
function findSmallNum(N, K)
{

    // Finding the remainder when N is
    // divided by K
    var rem = N % K;

    // If the remainder is 0, then the
    // number itself is divisible by K
    if (rem == 0)
        return N;
    else

        // Else, then the difference between
        // N and remainder is the largest number
        // which is divisible by K
        return N - rem;
}

// Function to find the smallest number
// greater than or equal to N
// that is divisible by K
function findLargeNum(N, K)
{

    // Finding the remainder when N is
    // divided by K
    var rem = (N + K) % K;

    // If the remainder is 0, then the
    // number itself is divisible by K
    if (rem == 0)
        return N;
    else

        // Else, then the difference between
        // N and remainder is the largest number
        // which is divisible by K
        return N + K - rem;
}

// Function to find the sum of numbers
// divisible by M in the given range
function sumDivisibles(A, B, M)
{

    // Variable to store the sum
    var sum = 0;
    var first = findSmallNum(A, M);
    var last = findLargeNum(B, M);

    // To bring the smallest and largest
    // numbers in the range [A, B]
    if (first < A)
        first += M;

    if (last > B)
        first -= M;

    // To count the number of terms in the AP
    var n = (parseInt(B / M) -
             parseInt((A - 1) / M));

    // Sum of n terms of an AP
    return n * (first + last) / 2;
}

// Driver code

// A and B define the range,
// M is the dividend
var A = 6, B = 15, M = 3;

// Printing the result
document.write( sumDivisibles(A, B, M));

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
42
```

**时间复杂度:** O(1)。