# 乘积严格大于 N 的两个整数的最小和

> 原文:[https://www . geesforgeks . org/两个整数的最小和-其乘积严格大于-n/](https://www.geeksforgeeks.org/minimum-sum-of-two-integers-whose-product-is-strictly-greater-than-n/)

给定一个整数 **N** ，任务是找到两个具有最小可能和的整数，使得它们的乘积严格大于 **N** 。

**示例:**

> **输入:** N = 10
> **输出:** 7
> **说明:**整数为 3 和 4。他们的乘积是 3 × 4 = 12，大于 n。
> 
> **输入:** N = 1
> **输出:** 3
> **说明:**整数为 1 和 2。他们的乘积是 1 × 2 = 2，大于 n。

**天真的做法:**让要求的数字为 **A** 和 **B** 。这个想法是基于这样的观察:为了最小化它们的和 **A** 应该是大于 **√N** 的最小数。一旦找到 **A** ，则 **B** 将等于 **A×B > N** 的最小数，可以线性地找到。

***时间复杂度:** O(√N)*
***辅助空间:** O(1)*

**高效途径:**以上解决方案可以通过[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到 **A** 和 **B** 进行优化。按照以下步骤解决问题:

*   初始化两个变量**低= 0** 和**高= 10 <sup>9</sup>** 。
*   迭代直到(高–低)大于 1，并执行以下操作:
    *   求中档**中间**的值为**(低+高)/2** 。
    *   现在将 **√N** 与中间元素**中**进行比较，如果 **√N** 小于等于中间元素，则**高**为**中**。
    *   否则，将**低**更新为**中**。
*   完成上述所有步骤后，设置 **A =高**。
*   重复同样的程序找到 **B** ，这样 **A×B > N** 。
*   完成上述步骤后，打印 **A** 和 **B** 的和作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to find the minimum sum of
// two integers such that their product
// is strictly greater than N
void minSum(int N)
{
    // Initialise low as 0 and
    // high as 1e9
    ll low = 0, high = 1e9;

    // Iterate to find the first number
    while (low + 1 < high) {

        // Find the middle value
        ll mid = low + (high - low) / 2;

        // If mid^2 is greater than
        // equal to A, then update
        // high to mid
        if (mid * mid >= N) {
            high = mid;
        }

        // Otherwise update low
        else {
            low = mid;
        }
    }

    // Store the first number
    ll first = high;

    // Again, set low as 0 and
    // high as 1e9
    low = 0;
    high = 1e9;

    // Iterate to find the second number
    while (low + 1 < high) {

        // Find the middle value
        ll mid = low + (high - low) / 2;

        // If first number * mid is
        // greater than N then update
        // high to mid
        if (first * mid > N) {
            high = mid;
        }

        // Else, update low to mid
        else {
            low = mid;
        }
    }

    // Store the second number
    ll second = high;

    // Print the result
    cout << first + second;
}

// Driver Code
int main()
{
    int N = 10;

    // Function Call
    minSum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the minimum sum of
// two integers such that their product
// is strictly greater than N
static void minSum(int N)
{

    // Initialise low as 0 and
    // high as 1e9
    long low = 0, high = 1000000000;

    // Iterate to find the first number
    while (low + 1 < high)
    {

        // Find the middle value
        long mid = low + (high - low) / 2;

        // If mid^2 is greater than
        // equal to A, then update
        // high to mid
        if (mid * mid >= N)
        {
            high = mid;
        }

        // Otherwise update low
        else
        {
            low = mid;
        }
    }

    // Store the first number
    long first = high;

    // Again, set low as 0 and
    // high as 1e9
    low = 0;
    high = 1000000000;

    // Iterate to find the second number
    while (low + 1 < high)
    {

        // Find the middle value
        long mid = low + (high - low) / 2;

        // If first number * mid is
        // greater than N then update
        // high to mid
        if (first * mid > N)
        {
            high = mid;
        }

        // Else, update low to mid
        else
        {
            low = mid;
        }
    }

    // Store the second number
    long second = high;

    // Print the result
    System.out.println(first + second);
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;

    // Function Call
    minSum(N);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum sum of
# two integers such that their product
# is strictly greater than N
def minSum(N):

    # Initialise low as 0 and
    # high as 1e9
    low = 0
    high = 1000000000

    # Iterate to find the first number
    while (low + 1 < high):

        # Find the middle value
        mid = low + (high - low) / 2

        # If mid^2 is greater than
        # equal to A, then update
        # high to mid
        if (mid * mid >= N):
            high = mid

        # Otherwise update low
        else:
            low = mid

    # Store the first number
    first = high

    # Again, set low as 0 and
    # high as 1e9
    low = 0
    high = 1000000000

    # Iterate to find the second number
    while (low + 1 < high):

        # Find the middle value
        mid = low + (high - low) / 2

        # If first number * mid is
        # greater than N then update
        # high to mid
        if (first * mid > N):
            high = mid

        # Else, update low to mid
        else:
            low = mid

    # Store the second number
    second = high

    # Print the result
    print(round(first + second))

# Driver Code
N = 10

# Function Call
minSum(N)

# This code is contributed by Dharanendra L V
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum sum of
// two integers such that their product
// is strictly greater than N
static void minSum(int N)
{

    // Initialise low as 0 and
    // high as 1e9
    long low = 0, high = 1000000000;

    // Iterate to find the first number
    while (low + 1 < high)
    {

        // Find the middle value
        long mid = low + (high - low) / 2;

        // If mid^2 is greater than
        // equal to A, then update
        // high to mid
        if (mid * mid >= N)
        {
            high = mid;
        }

        // Otherwise update low
        else
        {
            low = mid;
        }
    }

    // Store the first number
    long first = high;

    // Again, set low as 0 and
    // high as 1e9
    low = 0;
    high = 1000000000;

    // Iterate to find the second number
    while (low + 1 < high)
    {

        // Find the middle value
        long mid = low + (high - low) / 2;

        // If first number * mid is
        // greater than N then update
        // high to mid
        if (first * mid > N)
        {
            high = mid;
        }

        // Else, update low to mid
        else
        {
            low = mid;
        }
    }

    // Store the second number
    long second = high;

    // Print the result
    Console.WriteLine( first + second);
}

// Driver Code
static public void Main()
{
    int N = 10;

    // Function Call
    minSum(N);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum sum of
// two integers such that their product
// is strictly greater than N
function minSum(N)
{
    // Initialise low as 0 and
    // high as 1e9
    let low = 0, high = 1000000000;

    // Iterate to find the first number
    while (low + 1 < high) {

        // Find the middle value
        let mid = low + parseInt((high - low) / 2);

        // If mid^2 is greater than
        // equal to A, then update
        // high to mid
        if (mid * mid >= N) {
            high = mid;
        }

        // Otherwise update low
        else {
            low = mid;
        }
    }

    // Store the first number
    let first = high;

    // Again, set low as 0 and
    // high as 1e9
    low = 0;
    high = 1000000000;

    // Iterate to find the second number
    while (low + 1 < high) {

        // Find the middle value
        let mid = low + parseInt((high - low) / 2);

        // If first number * mid is
        // greater than N then update
        // high to mid
        if (first * mid > N) {
            high = mid;
        }

        // Else, update low to mid
        else {
            low = mid;
        }
    }

    // Store the second number
    let second = high;

    // Print the result
    document.write(first + second);
}

// Driver Code
    let N = 10;

    // Function Call
    minSum(N);

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*

**最有效的方法:**为了优化上述方法，该思想基于如下所示的[算术和几何级数](https://www.geeksforgeeks.org/progressions-ap-gp-hp/)的不等式。

> 从不等式看，如果有两个整数 **A** 和 **B、**T4**(A + B)/2≥√(A×B)**
> 现在，A×B =两个整数的乘积，即 N，A+B 为和 **(=S)** 。
> 因此， **S ≥ 2*√N**
> 为了得到严格大于 N 的乘积，上述方程转化为: **S ≥ 2*√(N+1)**

以下是上述方法的程序:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum of
// two integers such that their product
// is strictly greater than N
void minSum(int N)
{
    // Store the answer using the
    // AP-GP inequality
    int ans = ceil(2 * sqrt(N + 1));

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    int N = 10;

    // Function Call
    minSum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;

class GFG{

// Function to find the minimum sum of
// two integers such that their product
// is strictly greater than N
static void minSum(int N)
{

    // Store the answer using the
    // AP-GP inequality
    int ans = (int)Math.ceil(2 * Math.sqrt(N + 1));

    // Print the answer
    System.out.println( ans);
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;

    // Function Call
    minSum(N);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find the minimum sum of
# two integers such that their product
# is strictly greater than N
def minSum(N):

    # Store the answer using the
    # AP-GP inequality
    ans = math.ceil(2 * math.sqrt(N + 1))

    # Print the result
    print(math.trunc(ans))

# Driver Code
N = 10

# Function Call
minSum(N)

# This code is contributed by Dharanendra L V
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum sum of
// two integers such that their product
// is strictly greater than N
static void minSum(int N)
{

    // Store the answer using the
    // AP-GP inequality
    int ans = (int)Math.Ceiling(2 * Math.Sqrt(N + 1));

    // Print the answer
    Console.WriteLine( ans);
}

// Driver Code
static public void Main()
{
    int N = 10;

    // Function Call
    minSum(N);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum sum of
// two integers such that their product
// is strictly greater than N
function minSum(N)
{
    // Store the answer using the
    // AP-GP inequality
    let ans = Math.ceil(2 * Math.sqrt(N + 1));

    // Print the answer
    document.write(ans);
}

// Driver Code
let N = 10;

// Function Call
minSum(N);

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)