# 生成一个具有 K 个正数的数组，使得 arr[i]为-1 或 1，并且该数组的和为正

> 原文:[https://www . geeksforgeeks . org/生成一个带有 k 个正数的数组，这样 arri 要么是 1，要么是 1，数组之和是正数/](https://www.geeksforgeeks.org/generate-an-array-with-k-positive-numbers-such-that-arri-is-either-1-or-1-and-sum-of-the-array-is-positive/)

给定两个正整数 **N** 和 **K** ( ***1 ≤ K ≤ N*** )，任务是构造一个数组**arr【】**(*1 基索引*)使得每个数组元素 **arr[i]** 或者是 **i** 或者是 **-i** ，并且该数组精确地包含 **K** 正值，使得**I**或者是**I**如果可以生成多个这样的序列，请打印其中任何一个。否则，打印**-1”**。

**示例:**

> **输入:** N = 10，K = 6
> **输出:** -1 2 -3 4 -5 6 -7 8 9 10
> **解释:**
> 把序列看作{-1，2，-3，4，-5，6，-7，8，9，10}，构造的序列之和为(-1)+2+(-3)+4+(-5)+6+(-7)+8+9+10 = 23，其中
> 
> **输入:** N = 7，K = 2
> **输出:** -1

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，方法是使序列中的第一个**(N–K)**元素为负，剩余的 **K** 元素为正。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如说 **arr[]** ，存储结果序列。
*   初始化两个变量，将 **sumNeg** 和 **sumPos** 设为 **0** ，分别存储前**(N–K)**和剩余元素的和。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–K–1】**，并将 **arr[i]** 的值更新为 **-(i + 1)** ，并将值 **arr[i]** 添加到变量 **sumNeg** 中。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N–K，N–1】**，并将 **arr[i]** 的值更新为 **(i + 1)** ，并将值 **arr[i]** 添加到变量 **sumPos** 中。
*   如果 **sumNeg** 的[绝对值](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)的值大于 **sumPos** ，则打印 **-1** 。否则，[打印数组 **arr[]**](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) 中的求和元素作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate the resultant
// sequence of first N natural numbers
void findSequence(int n, int k)
{
    // Initialize an array of size N
    int arr[n];

    // Stores the sum of positive and
    // negative elements
    int sumPos = 0, sumNeg = 0;

    // Mark the first N - K elements
    // as negative
    for (int i = 0; i < n - k; i++) {

        // Update the value of arr[i]
        arr[i] = -(i + 1);

        // Update the value of sumNeg
        sumNeg += arr[i];
    }

    // Mark the remaining K elements
    // as positive
    for (int i = n - k; i < n; i++) {

        // Update the value of arr[i]
        arr[i] = i + 1;

        // Update the value of sumPos
        sumPos += arr[i];
    }

    // If the sum of the sequence
    // is negative, then print -1
    if (abs(sumNeg) >= sumPos) {
        cout << -1;
        return;
    }

    // Print the required sequence
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int N = 10, K = 6;
    findSequence(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to generate the resultant
// sequence of first N natural numbers
static void findSequence(int n, int k)
{

    // Initialize an array of size N
    int[] arr = new int[n];

    // Stores the sum of positive and
    // negative elements
    int sumPos = 0, sumNeg = 0;

    // Mark the first N - K elements
    // as negative
    for(int i = 0; i < n - k; i++)
    {

        // Update the value of arr[i]
        arr[i] = -(i + 1);

        // Update the value of sumNeg
        sumNeg += arr[i];
    }

    // Mark the remaining K elements
    // as positive
    for(int i = n - k; i < n; i++)
    {

        // Update the value of arr[i]
        arr[i] = i + 1;

        // Update the value of sumPos
        sumPos += arr[i];
    }

    // If the sum of the sequence
    // is negative, then print -1
    if (Math.abs(sumNeg) >= sumPos)
    {
        System.out.print(-1);
        return;
    }

    // Print the required sequence
    for(int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Driver code
public static void main(String args[])
{
    int N = 10, K = 6;

    findSequence(N, K);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python program for the above approach
# Function to generate the resultant
# sequence of first N natural numbers
def findSequence(n, k):

    # Initialize an array of size N
    arr = [0]*n

    # Stores the sum of positive and
    # negative elements
    sumPos = 0
    sumNeg = 0

    # Mark the first N - K elements
    # as negative
    for i in range(0, n - k):

        # Update the value of arr[i]
        arr[i] = -(i + 1)

        # Update the value of sumNeg
        sumNeg += arr[i]

    # Mark the remaining K elements
    # as positive
    for i in range(n - k, n):

        # Update the value of arr[i]
        arr[i] = i + 1

        # Update the value of sumPos
        sumPos += arr[i]

    # If the sum of the sequence
    # is negative, then pr -1
    if (abs(sumNeg) >= sumPos):
        print(-1)
        return

    # Pr the required sequence
    for i in range(n):
        print( arr[i], end =" ")

# Driver Code
N = 10
K = 6
findSequence(N, K)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to generate the resultant
    // sequence of first N natural numbers
    static void findSequence(int n, int k)
    {
        // Initialize an array of size N
        int[] arr = new int[n];

        // Stores the sum of positive and
        // negative elements
        int sumPos = 0, sumNeg = 0;

        // Mark the first N - K elements
        // as negative
        for (int i = 0; i < n - k; i++) {

            // Update the value of arr[i]
            arr[i] = -(i + 1);

            // Update the value of sumNeg
            sumNeg += arr[i];
        }

        // Mark the remaining K elements
        // as positive
        for (int i = n - k; i < n; i++) {

            // Update the value of arr[i]
            arr[i] = i + 1;

            // Update the value of sumPos
            sumPos += arr[i];
        }

        // If the sum of the sequence
        // is negative, then print -1
        if (Math.Abs(sumNeg) >= sumPos) {
            Console.Write(-1);
            return;
        }

        // Print the required sequence
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver Code
    public static void Main()
    {
        int N = 10, K = 6;
        findSequence(N, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to generate the resultant
// sequence of first N natural numbers
function findSequence(n, k)
{

    // Initialize an array of size N
    let arr = new Array(n);

    // Stores the sum of positive and
    // negative elements
    let sumPos = 0, sumNeg = 0;

    // Mark the first N - K elements
    // as negative
    for (let i = 0; i < n - k; i++) {

        // Update the value of arr[i]
        arr[i] = -(i + 1);

        // Update the value of sumNeg
        sumNeg += arr[i];
    }

    // Mark the remaining K elements
    // as positive
    for (let i = n - k; i < n; i++) {

        // Update the value of arr[i]
        arr[i] = i + 1;

        // Update the value of sumPos
        sumPos += arr[i];
    }

    // If the sum of the sequence
    // is negative, then print -1
    if (Math.abs(sumNeg) >= sumPos)
    {
        document.write(-1);
        return;
    }

    // Print the required sequence
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver Code
let N = 10, K = 6;
findSequence(N, K);

// This code is contributed by _saurabh_Jaiswal.
</script>
```

**Output:** 

```
-1 -2 -3 -4 5 6 7 8 9 10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)