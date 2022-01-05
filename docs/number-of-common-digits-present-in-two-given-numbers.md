# 出现在两个给定数字中的公共数字的数量

> 原文:[https://www . geeksforgeeks . org/二进制给定数字中的常用数字个数/](https://www.geeksforgeeks.org/number-of-common-digits-present-in-two-given-numbers/)

给定两个正数 **N** 和 **M** ，任务是计算存在于 **N** 和 **M** 中的位数。

**示例:**

> **输入:** N = 748294，M = 34298156
> **输出:** 4
> **说明:**两个数字中出现的数字是{4，8，2，9}。因此，所需的计数是 4。
> 
> **输入:** N = 111222，M = 333444
> **输出:** 0
> **说明:**两个给定的数字中没有共同的数字。

**方法:**给定的问题可以使用 [**散列**](https://www.geeksforgeeks.org/hashing-data-structure/) 来解决。按照以下步骤解决问题:

*   初始化一个变量，比如说**将**计数为 **0** ，以存储两个数字中共同的位数。
*   初始化两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如 **freq1[10]** 和 **freq2[10]** 为 **{0}** ，分别存储整数 **N** 和 **M** 中的位数。
*   [迭代整数](https://www.geeksforgeeks.org/c-program-to-print-all-digits-of-a-given-number/) **N** 的位数，并将**freq 1【】**中的每个位数增加 **1** 。
*   [迭代整数](https://www.geeksforgeeks.org/c-program-to-print-all-digits-of-a-given-number/) **M** 的位数，并将**freq 2【】**中的每个位数增加 **1** 。
*   如果**频率 q1[i]** 和**频率 q2[i]** 都超过 **0** ，则迭代范围**【0，9】**并将**计数**增加 **1** 。
*   最后，完成上述步骤后，打印获得的**计数**作为所需答案。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number of digits
// that are common in both N and M
int CommonDigits(int N, int M)
{
    // Stores the count of common digits
    int count = 0;

    // Stores the count of digits of N
    int freq1[10] = { 0 };

    // Stores the count of digits of M
    int freq2[10] = { 0 };

    // Iterate over the digits of N
    while (N > 0) {

        // Increment the count of
        // last digit of N
        freq1[N % 10]++;

        // Update N
        N = N / 10;
    }
    // Iterate over the digits of M
    while (M > 0) {

        // Increment the count of
        // last digit of M
        freq2[M % 10]++;

        // Update M
        M = M / 10;
    }
    // Iterate over the range [0, 9]
    for (int i = 0; i < 10; i++) {

        // If freq1[i] and freq2[i] both exceeds 0
        if (freq1[i] > 0 & freq2[i] > 0) {

            // Increment count by 1
            count++;
        }
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    // Input
    int N = 748294;
    int M = 34298156;

    cout << CommonDigits(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count number of digits
// that are common in both N and M
static int CommonDigits(int N, int M)
{

    // Stores the count of common digits
    int count = 0;

    // Stores the count of digits of N
    int freq1[] = new int[10];

    // Stores the count of digits of M
    int freq2[] = new int[10];

    // Iterate over the digits of N
    while (N > 0)
    {

        // Increment the count of
        // last digit of N
        freq1[N % 10]++;

        // Update N
        N = N / 10;
    }

    // Iterate over the digits of M
    while (M > 0)
    {

        // Increment the count of
        // last digit of M
        freq2[M % 10]++;

        // Update M
        M = M / 10;
    }

    // Iterate over the range [0, 9]
    for(int i = 0; i < 10; i++)
    {

        // If freq1[i] and freq2[i] both exceeds 0
        if (freq1[i] > 0 & freq2[i] > 0)
        {

            // Increment count by 1
            count++;
        }
    }

    // Return the count
    return count;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int N = 748294;
    int M = 34298156;

    System.out.print(CommonDigits(N, M));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count number of digits
# that are common in both N and M
def CommonDigits(N, M):

    # Stores the count of common digits
    count = 0

    # Stores the count of digits of N
    freq1 = [0] * 10

    # Stores the count of digits of M
    freq2 = [0] * 10

    # Iterate over the digits of N
    while (N > 0):

        # Increment the count of
        # last digit of N
        freq1[N % 10] += 1

        # Update N
        N = N // 10

    # Iterate over the digits of M
    while (M > 0):

        # Increment the count of
        # last digit of M
        freq2[M % 10] += 1

        # Update M
        M = M // 10

    # Iterate over the range [0, 9]
    for i in range(10):

        # If freq1[i] and freq2[i] both exceeds 0
        if (freq1[i] > 0 and freq2[i] > 0):

            # Increment count by 1
            count += 1

    # Return the count
    return count

# Driver Code
if __name__ == '__main__':

    # Input
    N = 748294
    M = 34298156

    print (CommonDigits(N, M))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count number of digits
// that are common in both N and M
static int CommonDigits(int N, int M)
{

    // Stores the count of common digits
    int count = 0;

    // Stores the count of digits of N
    int[] freq1 = new int[10];

    // Stores the count of digits of M
    int[] freq2 = new int[10];

    // Iterate over the digits of N
    while (N > 0)
    {

        // Increment the count of
        // last digit of N
        freq1[N % 10]++;

        // Update N
        N = N / 10;
    }

    // Iterate over the digits of M
    while (M > 0)
    {

        // Increment the count of
        // last digit of M
        freq2[M % 10]++;

        // Update M
        M = M / 10;
    }

    // Iterate over the range [0, 9]
    for(int i = 0; i < 10; i++)
    {

        // If freq1[i] and freq2[i]
        // both exceeds 0
        if (freq1[i] > 0 & freq2[i] > 0)
        {

            // Increment count by 1
            count++;
        }
    }

    // Return the count
    return count;
}

// Driver code
static void Main()
{

    // Input
    int N = 748294;
    int M = 34298156;

    Console.WriteLine(CommonDigits(N, M));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to count number of digits
// that are common in both N and M
function CommonDigits(N,M)
{
    // Stores the count of common digits
    var count = 0;

    // Stores the count of digits of N
    var freq1 = Array(10).fill(0);

    // Stores the count of digits of M
    var freq2 = Array(10).fill(0);

    // Iterate over the digits of N
    while (N > 0) {

        // Increment the count of
        // last digit of N
        freq1[N % 10]++;

        // Update N
        N = Math.floor(N / 10);
    }
    // Iterate over the digits of M
    while (M > 0) {

        // Increment the count of
        // last digit of M
        freq2[M % 10]++;

        // Update M
        M = Math.floor(M / 10);
    }
    var i;
    // Iterate over the range [0, 9]
    for (i = 0; i < 10; i++) {

        // If freq1[i] and freq2[i] both exceeds 0
        if (freq1[i] > 0 & freq2[i] > 0) {

            // Increment count by 1
            count++;
        }
    }

    // Return the count
    return count;
}

// Driver Code

    // Input
    var N = 748294;
    var M = 34298156;

    document.write(CommonDigits(N, M));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(位数(N)+位数(M))
**辅助空间:** O(10)