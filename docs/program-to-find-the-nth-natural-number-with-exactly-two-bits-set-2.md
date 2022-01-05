# 程序寻找正好设置了两位的第 n 个自然数|设置 2

> 原文:[https://www . geeksforgeeks . org/program-to-find-第 n 个正好两位的自然数-set-2/](https://www.geeksforgeeks.org/program-to-find-the-nth-natural-number-with-exactly-two-bits-set-2/)

给定一个整数 **N** ，任务是找到正好有两个设定位的 **N <sup>第</sup>T5】自然数。**

**示例:**

> **输入:** N = 4
> **输出:** 9
> **说明:**正好有两个设定位的数字是 3、5、6、9、10、12、…。
> 本系列第 4<sup>项为 9。</sup>
> 
> **输入:** N = 15
> **输出:** 48
> **解释:**正好有两个设定位的数字是 3、5、6、9、10、12、17、18、20、24、33、34、36、40、48……。
> 本系列第 15<sup>项为 48。</sup>

**天真的做法:**参考本文[之前的帖子](https://www.geeksforgeeks.org/program-to-find-the-nth-natural-number-with-exactly-two-bits-set/)获得这个问题可能的最简单的解决方案。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效途径:**优化上述途径，思路为使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到 **N <sup>th</sup> 号**。按照以下步骤解决问题:

*   给定系列中的任何数字都采用 **(2 <sup>a</sup> + 2 <sup>b</sup> )** 的形式，其中 **a > b** 。
*   系列中的第 **N <sup>个</sup>术语**可以通过识别值 **a** 和 **b** 来识别。
*   求 **a** 的值，使得 **(a * (a + 1)) / 2 ≥ N** ，并保持 **a** 必须最小的约束
*   因此，在上面的步骤中，使用二分搜索法找到约束的 **a** 的值。
*   完成上述步骤后，使用 **a** 和 **N** 找到 **b** 的值，并将结果打印为**(2<sup>a</sup>+2<sup>b</sup>)**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the Nth number
// with exactly two bits set
void findNthNum(long long int N)
{
    // Initialize variables
    long long int a, b, left;
    long long int right, mid;
    long long int t, last_num = 0;

    // Initialize the range in which
    // the value of 'a' is present
    left = 1, right = N;

    // Perform Binary Search
    while (left <= right) {

        // Find the mid value
        mid = left + (right - left) / 2;

        t = (mid * (mid + 1)) / 2;

        // Update the range using the
        // mid value t
        if (t < N) {
            left = mid + 1;
        }
        else if (t == N) {
            a = mid;
            break;
        }
        else {
            a = mid;
            right = mid - 1;
        }
    }

    // Find b value using a and N
    t = a - 1;
    b = N - (t * (t + 1)) / 2 - 1;

    // Print the value 2^a + 2^b
    cout << (1 << a) + (1 << b);
}

// Driver Code
int main()
{
    long long int N = 15;

    // Function Call
    findNthNum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the Nth number
// with exactly two bits set
static void findNthNum(int N)
{
    // Initialize variables
    int a = 0, b, left;
    int right, mid;
    int t, last_num = 0;

    // Initialize the range in which
    // the value of 'a' is present
    left = 1;
    right = N;

    // Perform Binary Search
    while (left <= right) {

        // Find the mid value
        mid = left + (right - left) / 2;

        t = (mid * (mid + 1)) / 2;

        // Update the range using the
        // mid value t
        if (t < N) {
            left = mid + 1;
        }
        else if (t == N) {
            a = mid;
            break;
        }
        else {
            a = mid;
            right = mid - 1;
        }
    }

    // Find b value using a and N
    t = a - 1;
    b = N - (t * (t + 1)) / 2 - 1;

    // Print the value 2^a + 2^b
    System.out.print((1 << a) + (1 << b));
}

// Driver Code
public static void main(String[] args)
{
    int N = 15;

    // Function Call
    findNthNum(N);
}
}

// This code contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the Nth number
# with exactly two bits set
def findNthNum(N):

    # Initialize variables
    last_num = 0

    # Initialize the range in which
    # the value of 'a' is present
    left = 1
    right = N

    # Perform Binary Search
    while (left <= right):

        # Find the mid value
        mid = left + (right - left) // 2

        t = (mid * (mid + 1)) // 2

        # Update the range using the
        # mid value t
        if (t < N):
            left = mid + 1

        elif (t == N):
            a = mid
            break

        else:
            a = mid
            right = mid - 1

    # Find b value using a and N
    t = a - 1
    b = N - (t * (t + 1)) // 2 - 1

    # Print the value 2^a + 2^b
    print((1 << a) + (1 << b))

# Driver Code
if __name__ == "__main__":

    N = 15

    # Function Call
    findNthNum(N)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the Nth number
// with exactly two bits set
static void findNthNum(int N)
{

    // Initialize variables
    int a = 0, b, left;
    int right, mid;
    int t;
    //int last_num = 0;

    // Initialize the range in which
    // the value of 'a' is present
    left = 1; right = N;

    // Perform Binary Search
    while (left <= right)
    {

        // Find the mid value
        mid = left + (right - left) / 2;

        t = (mid * (mid + 1)) / 2;

        // Update the range using the
        // mid value t
        if (t < N)
        {
            left = mid + 1;
        }
        else if (t == N)
        {
            a = mid;
            break;
        }
        else
        {
            a = mid;
            right = mid - 1;
        }
    }

    // Find b value using a and N
    t = a - 1;
    b = N - (t * (t + 1)) / 2 - 1;

    // Print the value 2^a + 2^b
    Console.Write((1 << a) + (1 << b));
}

// Driver Code
public static void Main()
{
    int N = 15;

    // Function Call
    findNthNum(N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the Nth number
// with exactly two bits set
function findNthNum(N)
{
    // Initialize variables
    let a = 0, b, left;
    let right, mid;
    let t, last_num = 0;

    // Initialize the range in which
    // the value of 'a' is present
    left = 1;
    right = N;

    // Perform Binary Search
    while (left <= right) {

        // Find the mid value
        mid = left + (right - left) / 2;

        t = (mid * (mid + 1)) / 2;

        // Update the range using the
        // mid value t
        if (t < N) {
            left = mid + 1;
        }
        else if (t == N) {
            a = mid;
            break;
        }
        else {
            a = mid;
            right = mid - 1;
        }
    }

    // Find b value using a and N
    t = a - 1;
    b = N - (t * (t + 1)) / 2 - 1;

    // Print the value 2^a + 2^b
    document.write((1 << a) + (1 << b));
}

// Driver Code

    let N = 15;

    // Function Call
    findNthNum(N);

</script>
```

**Output:** 

```
48
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*