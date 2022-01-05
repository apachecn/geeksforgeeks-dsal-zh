# 一个数组的最后一个元素，重复删除第一个元素并将其追加到数组末尾两次，正好 K 次

> 原文:[https://www . geeksforgeeks . org/数组的最后一个元素在重复删除第一个元素并将其追加到数组末尾两次后精确 k 次/](https://www.geeksforgeeks.org/last-element-of-an-array-after-repeatedly-removing-the-first-element-and-appending-it-to-the-end-of-the-array-twice-exactly-k-times/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**，任务是找到[数组中的最后一个元素](https://www.geeksforgeeks.org/get-first-and-last-elements-from-array-and-vector-in-cpp/)，该元素是通过重复移除数组的第一个元素并将其两次追加到数组的末尾 **K** 次而获得的。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 5
> **输出:5**
> **解释:**
> 最初，数组为{1，2，3，4，5}。以下操作执行 K(= 5)次:
> 在 1 <sup>st</sup> 操作后，数组修改为{2，3，4，5，1，1}。
> 第 2 次<sup>和</sup>操作后，数组修改为{3，4，5，1，1，2，2}。
> 3<sup>rd</sup>操作后，数组修改为{4，5，1，1，2，2，3，3}。
> 第 4 次<sup>操作后，数组修改为{5，1，1，2，2，3，3，4，4}。
> 在第 5 次<sup>操作后，数组修改为{1，1，2，2，3，3，4，4，5，5}。
> 完成以上操作后，最后一个元素为 5。因此，答案是 5。</sup></sup>
> 
> **输入:** arr[] = {1，2，3}，K = 7
> T3】输出: 2

**方法:**给定的问题可以通过观察以下模式来解决:

> 考虑一个数组 arr[] = {1，2，3，4，5}
> 前 5 次运算后，数组修改为{1，1，2，2，3，3，4，4，5，5}。
> 前 10 次操作后，数组修改为{1，1，1，1，2，2，2，3，3，3，4，4，4，4，5，5，5，5，5}。
> 
> **因此，N * 2 <sup>K</sup> 运算后的阵列大小为 2 * N * 2<sup>K</sup>T5。**

按照以下步骤解决问题:

*   [使用变量 **j** 从值 **0** 迭代一个循环](https://www.geeksforgeeks.org/range-based-loop-c/)，并将 **K** 的值更新为**(K–N * 2<sup>j</sup>)**，直到 **K** 大于 **N * 2 <sup>j</sup>** 。
*   完成以上步骤后，初始化一个变量，说 **r** 为**2<sup>j</sup>T5】，其中每个值重复自身 **R** 次。**
*   初始化一个变量，比如说 **M** 为 **1** ，该变量存储数组**arr【】**中字符的索引，该索引等于执行 **K** 操作后的最后一个字符。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，如果 **K** 的值大于 **R * i** ，则将 **M** 增加 **1** 。
*   完成上述步骤后，打印**arr[M–1]**的值作为数组的最后一个元素[的结果。](https://www.geeksforgeeks.org/get-first-and-last-elements-from-array-and-vector-in-cpp/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the last element
// after performing given operations
void findLastElement(int N, vector<int> A)
{

    // Length of the array
    int l = A.size();

    int j = 0;

    // Increment j until
    // condition is satisfied
    while (N > l * (pow(2, j)))
    {
        N = N - l * pow(2, j);
        j += 1;
    }

    int k = 1;

    // In each pair every value is
    // repeating r number of times
    int r = pow(2, j);
    for(int i = 1; i < l; i++)
    {
        if (N > r * i)
            k += 1;
    }

    // Print the result according
    // to the value of k
    for(int i = 0; i < l; i++)
    {
        if (i + 1 == k)
        {
            cout << (A[i]);
            return;
        }
    }
}

// Driver Code
int main()
{

    // Given K
    int K = 7;

    // Given arr[]
    vector<int> A = { 1, 2, 3 };

    // Function call
    findLastElement(K, A);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

    // Function to find the last element
    // after performing given operations
    static void findLastElement(int N, int[] A)
    {

        // Length of the array
        int l = A.length;

        int j = 0;

        // Increment j until
        // condition is satisfied
        while (N > l * (int)(Math.pow(2, j))) {
            N = N - l * (int)Math.pow(2, j);
            j += 1;
        }

        int k = 1;

        // In each pair every value is
        // repeating r number of times
        int r = (int)Math.pow(2, j);
        for (int i = 1; i < l; i++) {
            if (N > r * i)
                k += 1;
        }

        // Print the result according
        // to the value of k
        for (int i = 0; i < l; i++) {
            if (i + 1 == k) {
                System.out.print(A[i]);
                return;
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given K
        int K = 7;

        // Given arr[]
        int[] A = { 1, 2, 3 };

        // Function call
        findLastElement(K, A);
    }
}

// This code is contributed by subham348.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the last element
# after performing given operations
def findLastElement(N, A):

    # Length of the array
    l = len(A)

    j = 0

    # Increment j until
    # condition is satisfied
    while(N > l*(2**j)):
        N = N - l * 2**j
        j += 1

    k = 1

    # In each pair every value is
    # repeating r number of times
    r = 2**j
    for i in range(1, l):
        if N > r * i:
            k += 1

    # Print the result according
    # to the value of k
    for i in range(0, len(A)):
        if(i + 1 == k):
            print(A[i])
            return

# Driver Code
if __name__ == '__main__':

      # Given K
    K = 7

    # Given arr[]
    A = [1, 2, 3]

    # Function call
    findLastElement(K, A)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to find the last element
    // after performing given operations
    static void findLastElement(int N, int[] A)
    {

        // Length of the array
        int l = A.Length;

        int j = 0;

        // Increment j until
        // condition is satisfied
        while (N > l * (int)(Math.Pow(2, j))) {
            N = N - l * (int)Math.Pow(2, j);
            j += 1;
        }

        int k = 1;

        // In each pair every value is
        // repeating r number of times
        int r = (int)Math.Pow(2, j);
        for (int i = 1; i < l; i++) {
            if (N > r * i)
                k += 1;
        }

        // Print the result according
        // to the value of k
        for (int i = 0; i < l; i++) {
            if (i + 1 == k) {
                Console.WriteLine(A[i]);
                return;
            }
        }
    }

// Driver Code
public static void Main(String[] args)
{
    // Given K
        int K = 7;

        // Given arr[]
        int[] A = { 1, 2, 3 };

        // Function call
        findLastElement(K, A);
}
}

// This code is contributed by target_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the last element
// after performing given operations
function findLastElement(N, A)
{

    // Length of the array
    let l = A.length;

    let j = 0;

    // Increment j until
    // condition is satisfied
    while (N > l * (Math.pow(2, j)))
    {
        N = N - l * Math.pow(2, j);
        j += 1;
    }

    let k = 1;

    // In each pair every value is
    // repeating r number of times
    let r = Math.pow(2, j);
    for(let i = 1; i < l; i++)
    {
        if (N > r * i)
            k += 1;
    }

    // Print the result according
    // to the value of k
    for(let i = 0; i < l; i++)
    {
        if (i + 1 == k)
        {
            document.write(A[i]);
            return;
        }
    }
}

// Driver Code

    // Given K
    let K = 7;

    // Given arr[]
    let A = [ 1, 2, 3 ];

    // Function call
    findLastElement(K, A);

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*