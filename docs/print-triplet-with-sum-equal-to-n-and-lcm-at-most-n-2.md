# 打印总和等于 N 且 LCM 最多为 N/2 的三联体

> 原文:[https://www . geeksforgeeks . org/print-three-with-sum-equal-n-and-LCM-顶多-n-2/](https://www.geeksforgeeks.org/print-triplet-with-sum-equal-to-n-and-lcm-at-most-n-2/)

给定一个正整数 **N** ，任务是找到一个三元组 **{X，Y，Z}** ，使得 **X** 、 **Y** 、 **Z** 的[最小公倍数](https://www.geeksforgeeks.org/c-program-find-lcm-two-numbers/)小于或等于 **N/2** ，且 **X** 、 **Y** 、 **Z** 之和相等如果存在多个答案，则打印其中任何一个。

**示例:**

> ***输入:*** N = 8
> ***输出:*** 4 2 2
> ***解释:***
> 一个可能的三元组是{4，2，2}。所有整数之和等于(4+2+2 = 8)，LCM 等于 4，等于 N/2( =4)。
> 
> ***输入:*** N = 5
> ***输出:*** 1 2 2
> ***解释:***
> 一个可能的三元组是{1，2，2}。所有整数之和等于(1+2+2 = 5)，LCM 等于 2，等于 N/2( =2)。

**方法:**问题可以根据以下事实解决:

> 假设， **N = X+Y+Z，**那么:
> 
> 1.  如果 **N** 为奇数，则 **X** 、 **Y** 或 **Z** 中的任何一个为奇数，或者三者都为奇数。
> 2.  如果 **N** 是偶数，那么所有的数都必须是偶数。
> 3.  因此，想法是根据上述事实在答案中包含最小可能值，这将降低 **X** 、 **Y** 和 **Z** 的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 。

按照以下步骤解决问题:

*   将 **3** 变量 **x，y，**和 **z** 初始化为 **0** 来存储三元组的值。
*   如果 **N%2** 不等于 **0** ，即 **N** 为奇数，则执行以下步骤:
    *   如果 **N** 为奇数，则 **x，y，**或 **z** 中至少有一个应为奇数，最坏情况下 **x，y，z** 的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 为 **N/2** 。
    *   将 **x** 和 **y** 的值设置为 **N/2** ，将 **z** 的值设置为 **1。**
*   否则，如果 **N%4** 不等于 **0，**则 **z** 的值可以是 **2** ，而 **x** 和 **y** 的值可以是 **N/2-1。**否则 **x** 的值可以是 **N/2** ， **y** 和 **z** 的值可以是 **N/4。**
*   执行上述步骤后，打印 **x，y，**和 **z.** 的值

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a triplet  with the
// sum equal to N and LCM less than or
// equal to N
void validTriplet(int N)
{
    // Stores the triplets
    int x, y, z;

    // If N is odd
    if ((N % 2) != 0) {
        x = N / 2;
        y = N / 2;
        z = 1;
    }
    // If N is even
    else {

        // If N is not a multiple of 4
        if ((N % 4) != 0) {
            x = (N / 2) - 1;
            y = (N / 2) - 1;
            z = 2;
        }

        // If N is a multiple of 4
        else {
            x = N / 2;
            y = N / 4;
            z = N / 4;
        }
    }

    // Finally, print the answer
    cout << x << " " << y << " " << z << '\n';
}

// Driver Code
int main()
{
    // Given Input
    int N = 5;

    // Function Call
    validTriplet(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find a triplet  with the
    // sum equal to N and LCM less than or
    // equal to N
    static void validTriplet(int N)
    {

        // Stores the triplets
        int x, y, z;

        // If N is odd
        if ((N % 2) != 0) {
            x = N / 2;
            y = N / 2;
            z = 1;
        }

        // If N is even
        else {

            // If N is not a multiple of 4
            if ((N % 4) != 0) {
                x = (N / 2) - 1;
                y = (N / 2) - 1;
                z = 2;
            }

            // If N is a multiple of 4
            else {
                x = N / 2;
                y = N / 4;
                z = N / 4;
            }
        }

        // Finally, print the answer
        System.out.print(x + " " + y + " " + z);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int N = 5;

        // Function Call
        validTriplet(N);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Function to find a triplet  with the
# sum equal to N and LCM less than or
# equal to N
def validTriplet(N):

     # If N is odd
    if (N % 2) != 0:
        x = N//2
        y = N//2
        z = 1

        # if N is even
    else:

         # If N is not a multiple of 4
        if (N % 4) != 0:
            x = N//2 - 1
            y = N//2 - 1
            z = 2

            # if N is multiple of 4
        else:
            x = N//2
            y = N//4
            z = N//4

     # Print the result
    print(str(x) + " " + str(y) + " " + str(z))

# Driver code
N = 5
validTriplet(N)

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find a triplet  with the
// sum equal to N and LCM less than or
// equal to N
static void validTriplet(int N)
{

    // Stores the triplets
    int x, y, z;

    // If N is odd
    if ((N % 2) != 0) {
        x = N / 2;
        y = N / 2;
        z = 1;
    }
    // If N is even
    else {

        // If N is not a multiple of 4
        if ((N % 4) != 0) {
            x = (N / 2) - 1;
            y = (N / 2) - 1;
            z = 2;
        }

        // If N is a multiple of 4
        else {
            x = N / 2;
            y = N / 4;
            z = N / 4;
        }
    }

    // Finally, print the answer
    Console.Write(x + " " + y + " " + z );
}

// Driver Code
public static void Main()
{
    // Given Input
    int N = 5;

    // Function Call
    validTriplet(N);

}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Java program for the above approach
// Function to find a triplet  with the
// sum equal to N and LCM less than or
// equal to N
function validTriplet(N)
    {

        // Stores the triplets
        var x, y, z;

        // If N is odd
        if ((N % 2) == 0) {
            x = N / 2;
            y = N / 2;
            z = 1;
        }

        // If N is even
        else {

            // If N is not a multiple of 4
            if ((N % 4) != 0) {
                x = (N / 2) - 1;
                y = (N / 2) - 1;
                z = 1;
            }

            // If N is a multiple of 4
            else {
                x = N / 2;
                y = N / 4;
                z = N / 4;
            }
        }

        // Finally, print the answer
        document.write(x + " " + y + " " + z);
    }

    // Driver Code
    // Given Input
       var N = 4;

       // Function Call
       validTriplet(N);

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
2 2 1
```

***时间复杂度:*** *O(1)*
***辅助空间:** O(1)*