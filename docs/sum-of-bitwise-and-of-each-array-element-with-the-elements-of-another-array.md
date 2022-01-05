# 每个数组元素与另一个数组元素的按位“与”之和

> 原文:[https://www . geeksforgeeks . org/每个数组元素与另一个数组元素的按位求和/](https://www.geeksforgeeks.org/sum-of-bitwise-and-of-each-array-element-with-the-elements-of-another-array/)

给定两个大小为 **M** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr 1【】**和大小为 **N** 的**arr 2【】**，任务是求**arr 1【】**的每个元素与数组**arr 2【】**的元素之和。

**示例:**

> **输入:** arr1[] = {1，2，3}，arr2[] = {1，2，3}，M = 3，N = 3
> **输出:** 2 4 6
> **解释:**
> 对于 arr1[]，Sum = arr 1[0]&arr 2[0]+arr 1[0]&arr 2[1]+arr 1[0]&arr 2[2]，Sum = 1【T11 Sum = arr 1[1]&arr 2[0]+arr 1[1]&arr 2[1]+arr 1[1]&arr 2[2]，Sum = 2&1+2&2+2&3 = 4
> 对于 arr1[]中索引 2 处的元素，Sum = arr 1[2]&arr 2[0]+arr 1[2]&arr 2[1]+arr 1[2]&arr 2
> 
> **输入:** arr1[] = {2，4，8，16}，arr2[] = {2，4，8，16}，M = 4，N = 4
> **输出:** 2 4 8 16

**天真法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr 1【】**并针对数组的每个元素**arr 1【】**、[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)T10】arr 2【】并计算**arr 1【】**当前元素与**arr 2【】**所有元素的和 [**位运算**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 求

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效途径:**思路是利用[位操纵](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)解决上述问题。假设数组的每个元素只能用 **32** 位来表示。

*   根据[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)属性，在执行运算时， **i <sup>第</sup>T5】位只有在两个数字在的 **i <sup>第</sup>T15】位置都有位时才会被置位，其中 **0≤i < 32** 。****
*   因此，对于 **arr1【】、**中的一个数字，如果 **i <sup>第</sup>T5】位是设定位，那么 **i <sup>第</sup>T9】位将贡献**K * 2<sup>I</sup>T13】的和，其中 **K** 是**arr 2【】**中具有[设定](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)的[位**的数字总数**](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)******

按照以下步骤解决问题:

1.  初始化一个整数数组**频率【】**以存储在**arr 2【】**中的数字计数，已经将位设置在**I<sup>th</sup>T7】位置，其中 **0≤i < 32****
2.  在数组**中遍历 **arr2[]** ，对于每个元素，以[二进制形式](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)表示，并在[二进制表示](https://www.geeksforgeeks.org/binary-representations-in-digital-logic/)中具有 **1** 的位置将**频率[]** 数组中的计数增加 1。**
3.  [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr 1】
    1.  用 **0** 初始化一个整数变量**位与和**。
    2.  使用变量 **j** 在范围**【0，31】**内遍历。
    3.  如果第**j**位被设置为**arr 2【I】**的二进制表示中的位，则按**频率【j】* 2<sup>j</sup>**递增**位次 _AND_sum** 。
    4.  打印得出的总和，即**位的 _AND_sum** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to compute the AND sum
// for each element of an array
void Bitwise_AND_sum_i(int arr1[], int arr2[], int M, int N)
{

    // Declaring an array of
    // size 32 for storing the
    // count of each bit
    int frequency[32] = { 0 };

    // Traverse the array arr2[]
    // and store the count of a
    // bit in frequency array
    for (int i = 0; i < N; i++) {

        // Current bit position
        int bit_position = 0;
        int num = arr1[i];

        // While num is greater
        // than 0
        while (num) {

            // Checks if ith bit is
            // set or not
            if (num & 1) {

                // Increment the count of
                // bit by one
                frequency[bit_position] += 1;
            }

            // Increment the bit position
            // by one
            bit_position += 1;

            // Right shift the num by one
            num >>= 1;
        }
    }

    // Traverse in the arr2[]
    for (int i = 0; i < M; i++) {

        int num = arr2[i];

        // Store the ith bit
        // value
        int value_at_that_bit = 1;

        // Total required sum
        int bitwise_AND_sum = 0;

        // Traverse in the range [0, 31]
        for (int bit_position = 0; bit_position < 32;
             bit_position++) {

            // Checks if current bit is set
            if (num & 1) {

                // Increment the bitwise sum
                // by frequency[bit_position]
                // * value_at_that_bit;
                bitwise_AND_sum += frequency[bit_position]
                                   * value_at_that_bit;
            }

            // Right shift num by one
            num >>= 1;

            // Left shift vale_at_that_bit by one
            value_at_that_bit <<= 1;
        }

        // Print the sum obtained for ith
        // number in arr1[]
        cout << bitwise_AND_sum << ' ';
    }

    return;
}

// Driver Code
int main()
{

    // Given arr1[]
    int arr1[] = { 1, 2, 3 };

    // Given arr2[]
    int arr2[] = { 1, 2, 3 };

    // Size of arr1[]
    int N = sizeof(arr1) / sizeof(arr1[0]);

    // Size of arr2[]
    int M = sizeof(arr2) / sizeof(arr2[0]);

    // Function Call
    Bitwise_AND_sum_i(arr1, arr2, M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

      // Driver Code
    public static void main(String[] args)
    {

        // Given arr1[]
        int[] arr1 = { 1, 2, 3 };

        // Given arr2[]
        int[] arr2 = { 1, 2, 3 };

        // Size of arr1[]
        int N = arr1.length;

        // Size of arr2[]
        int M = arr2.length;

        // Function Call
        Bitwise_AND_sum_i(arr1, arr2, M, N);
    }

    // Function to compute the AND sum
    // for each element of an array
    static void Bitwise_AND_sum_i(int arr1[], int arr2[],
                                  int M, int N)
    {

        // Declaring an array of
        // size 32 for storing the
        // count of each bit
        int[] frequency = new int[32];

        // Traverse the array arr2[]
        // and store the count of a
        // bit in frequency array
        for (int i = 0; i < N; i++)
        {

            // Current bit position
            int bit_position = 0;
            int num = arr1[i];

            // While num is greater
            // than 0
            while (num != 0)
            {

                // Checks if ith bit is
                // set or not
                if ((num & 1) != 0)
                {

                    // Increment the count of
                    // bit by one
                    frequency[bit_position] += 1;
                }

                // Increment the bit position
                // by one
                bit_position += 1;

                // Right shift the num by one
                num >>= 1;
            }
        }

        // Traverse in the arr2[]
        for (int i = 0; i < M; i++)
        {
            int num = arr2[i];

            // Store the ith bit
            // value
            int value_at_that_bit = 1;

            // Total required sum
            int bitwise_AND_sum = 0;

            // Traverse in the range [0, 31]
            for (int bit_position = 0; bit_position < 32;
                 bit_position++)
            {

                // Checks if current bit is set
                if ((num & 1) != 0)
                {

                    // Increment the bitwise sum
                    // by frequency[bit_position]
                    // * value_at_that_bit;
                    bitwise_AND_sum
                        += frequency[bit_position]
                           * value_at_that_bit;
                }

                // Right shift num by one
                num >>= 1;

                // Left shift vale_at_that_bit by one
                value_at_that_bit <<= 1;
            }

            // Print the sum obtained for ith
            // number in arr1[]
            System.out.print( bitwise_AND_sum + " ");
        }
    }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to compute the AND sum
# for each element of an array
def Bitwise_AND_sum_i(arr1, arr2, M, N):

    # Declaring an array of
    # size 32 for storing the
    # count of each bit
    frequency = [0]*32

    # Traverse the array arr2[]
    # and store the count of a
    # bit in frequency array
    for i in range(N):

        # Current bit position
        bit_position = 0
        num = arr1[i]

        # While num is greater
        # than 0
        while (num):

            # Checks if ith bit is
            # set or not
            if (num & 1):

                # Increment the count of
                # bit by one
                frequency[bit_position] += 1

            # Increment the bit position
            # by one
            bit_position += 1

            # Right shift the num by one
            num >>= 1

    # Traverse in the arr2[]
    for i in range(M):
        num = arr2[i]

        # Store the ith bit
        # value
        value_at_that_bit = 1

        # Total required sum
        bitwise_AND_sum = 0

        # Traverse in the range [0, 31]
        for bit_position in range(32):

            # Checks if current bit is set
            if (num & 1):

                # Increment the bitwise sum
                # by frequency[bit_position]
                # * value_at_that_bit
                bitwise_AND_sum += frequency[bit_position] * value_at_that_bit

            # Right shift num by one
            num >>= 1

            # Left shift vale_at_that_bit by one
            value_at_that_bit <<= 1

        # Print sum obtained for ith
        # number in arr1[]
        print(bitwise_AND_sum, end = " ")
    return

# Driver Code
if __name__ == '__main__':

    # Given arr1[]
    arr1 = [1, 2, 3]

    # Given arr2
    arr2 = [1, 2, 3]

    # Size of arr1[]
    N = len(arr1)

    # Size of arr2[]
    M = len(arr2)

    # Function Call
    Bitwise_AND_sum_i(arr1, arr2, M, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

      // Driver code
    static public void Main()
    {

        // Given arr1[]
        int[] arr1 = { 1, 2, 3 };

        // Given arr2[]
        int[] arr2 = { 1, 2, 3 };

        // Size of arr1[]
        int N = arr1.Length;

        // Size of arr2[]
        int M = arr2.Length;

        // Function Call
        Bitwise_AND_sum_i(arr1, arr2, M, N);
    }

    // Function to compute the AND sum
    // for each element of an array
    static void Bitwise_AND_sum_i(int[] arr1, int[] arr2,
                                  int M, int N)
    {

        // Declaring an array of
        // size 32 for storing the
        // count of each bit
        int[] frequency = new int[32];

        // Traverse the array arr2[]
        // and store the count of a
        // bit in frequency array
        for (int i = 0; i < N; i++)
        {

            // Current bit position
            int bit_position = 0;
            int num = arr1[i];

            // While num is greater
            // than 0
            while (num != 0)
            {

                // Checks if ith bit is
                // set or not
                if ((num & 1) != 0)
                {

                    // Increment the count of
                    // bit by one
                    frequency[bit_position] += 1;
                }

                // Increment the bit position
                // by one
                bit_position += 1;

                // Right shift the num by one
                num >>= 1;
            }
        }

        // Traverse in the arr2[]
        for (int i = 0; i < M; i++)
        {

            int num = arr2[i];

            // Store the ith bit
            // value
            int value_at_that_bit = 1;

            // Total required sum
            int bitwise_AND_sum = 0;

            // Traverse in the range [0, 31]
            for (int bit_position = 0; bit_position < 32;
                 bit_position++) {

                // Checks if current bit is set
                if ((num & 1) != 0)
                {

                    // Increment the bitwise sum
                    // by frequency[bit_position]
                    // * value_at_that_bit;
                    bitwise_AND_sum
                        += frequency[bit_position]
                           * value_at_that_bit;
                }

                // Right shift num by one
                num >>= 1;

                // Left shift vale_at_that_bit by one
                value_at_that_bit <<= 1;
            }

            // Print the sum obtained for ith
            // number in arr1[]
            Console.Write(bitwise_AND_sum + " ");
        }
    }
}

// The code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to compute the AND sum
// for each element of an array
function Bitwise_AND_sum_i(arr1, arr2, M, N) {

    // Declaring an array of
    // size 32 for storing the
    // count of each bit
    let frequency = new Array(32).fill(0);

    // Traverse the array arr2[]
    // and store the count of a
    // bit in frequency array
    for (let i = 0; i < N; i++) {

        // Current bit position
        let bit_position = 0;
        let num = arr1[i];

        // While num is greater
        // than 0
        while (num) {

            // Checks if ith bit is
            // set or not
            if (num & 1) {

                // Increment the count of
                // bit by one
                frequency[bit_position] += 1;
            }

            // Increment the bit position
            // by one
            bit_position += 1;

            // Right shift the num by one
            num >>= 1;
        }
    }

    // Traverse in the arr2[]
    for (let i = 0; i < M; i++) {

        let num = arr2[i];

        // Store the ith bit
        // value
        let value_at_that_bit = 1;

        // Total required sum
        let bitwise_AND_sum = 0;

        // Traverse in the range [0, 31]
        for (let bit_position = 0; bit_position < 32; bit_position++) {

            // Checks if current bit is set
            if (num & 1) {

                // Increment the bitwise sum
                // by frequency[bit_position]
                // * value_at_that_bit;
                bitwise_AND_sum += frequency[bit_position] * value_at_that_bit;
            }

            // Right shift num by one
            num >>= 1;

            // Left shift vale_at_that_bit by one
            value_at_that_bit <<= 1;
        }

        // Print the sum obtained for ith
        // number in arr1[]
        document.write(bitwise_AND_sum + ' ');
    }

    return;
}

// Driver Code

// Given arr1[]
let arr1 = [1, 2, 3];

// Given arr2[]
let arr2 = [1, 2, 3];

// Size of arr1[]
let N = arr1.length;

// Size of arr2[]
let M = arr2.length

// Function Call
Bitwise_AND_sum_i(arr1, arr2, M, N);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
2 4 6
```

***时间复杂度:** O(N * 32)*
***辅助空间:** O(N * 32)*