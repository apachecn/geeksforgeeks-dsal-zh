# 丢失的最小非负整数，直到每个数组索引

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，对于每个数组索引，任务是找到[最小的丢失的非负整数](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/) ]直到给定数组的索引。

**示例：**

> **输入：** arr [] = {1、3、0、2}
> **输出：** 0 0 2 4
> **说明：**
> 从索引 0 到 0 的最小丢失的非负整数是 0。
> 从索引 0 到 1 的最小丢失的非负整数是 0。
> 从索引 0 到 2 的最小丢失的非负整数是 2。
> 从索引 0 到 3 的最小丢失的非负整数是 4。
> 
> **输入：** arr [] = {0，1，2，3，5}
> **输出：** 1 2 3 4 4

**方法：**可以使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)解决此问题。 请按照以下步骤解决问题：

*   初始化一个变量，例如 **smNonNeg** ，以在给定数组的起始索引和当前索引之间存储[最小丢失的非负整数](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)。
*   初始化一个数组，例如说 **hash [N]** ，以检查在起始索引和当前索引之间是否存在 **smNonNeg** 。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并检查 **hash [smNonNeg]** 是否等于 **0** 。 如果发现是真的，则打印 **smNonNeg** 的值。
*   否则，增加 **smNonNeg** 的值，而 **hash [smNonNeg]** 不等于 **0** 。

下面是上述方法的实现：

## C ++

```

// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the smallest
// missing non-negative integer
// up to every array indices
void smlstNonNeg(int arr[], int N)
{
    // Stores the smallest missing
    // non-negative integers between
    // start index to current index
    int smNonNeg = 0;

    // Store the boolean value to check
    // smNonNeg present between start
    // index to each index of the array
    bool hash[N + 1] = { 0 };

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Since output always lies
        // in the range[0, N - 1]
        if (arr[i] >= 0 and arr[i] < N) {
            hash[arr[i]] = true;
        }

        // Check if smNonNeg is
        // present between start index
        // and current index or not
        while (hash[smNonNeg]) {
            smNonNeg++;
        }

        // Print smallest missing
        // non-negative integer
        cout << smNonNeg << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 2, 3, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    smlstNonNeg(arr, N);
}

```

## 爪哇

```

// Java program to implement
// the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to print the smallest
// missing non-negative integer
// up to every array indices
static void smlstNonNeg(int arr[], int N)
{

    // Stores the smallest missing
    // non-negative integers between
    // start index to current index
    int smNonNeg = 0;

    // Store the boolean value to check
    // smNonNeg present between start
    // index to each index of the array
    Boolean[] hash = new Boolean[N + 1];
    Arrays.fill(hash, false);

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Since output always lies
        // in the range[0, N - 1]
        if (arr[i] >= 0 && arr[i] < N)
        {
            hash[arr[i]] = true;
        }

        // Check if smNonNeg is
        // present between start index
        // and current index or not
        while (hash[smNonNeg]) 
        {
            smNonNeg++;
        }

        // Print smallest missing
        // non-negative integer
        System.out.print(smNonNeg + " ");
    }
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 0, 1, 2, 3, 5 };
    int N = arr.length;

    smlstNonNeg(arr, N);
}
}

// This code is contributed by sanjoy_62

```

## Python3

```

# Python3 program to implement
# the above approach

# Function to prthe smallest
# missing non-negative integer
# up to every array indices
def smlstNonNeg(arr, N):

    # Stores the smallest missing
    # non-negative integers between
    # start index to current index
    smNonNeg = 0

    # Store the boolean value to check
    # smNonNeg present between start
    # index to each index of the array
    hash = [0] * (N + 1)

    # Traverse the array
    for i in range(N):

        # Since output always lies
        # in the range[0, N - 1]
        if (arr[i] >= 0 and arr[i] < N):
            hash[arr[i]] = True

        # Check if smNonNeg is
        # present between start index
        # and current index or not
        while (hash[smNonNeg]):
            smNonNeg += 1

        # Print smallest missing
        # non-negative integer
        print(smNonNeg, end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 0, 1, 2, 3, 5 ]
    N = len(arr)

    smlstNonNeg(arr, N)

# This code is contributed by mohit kumar 29

```

## C＃

```

// C# program to implement
// the above approach
using System;

class GFG{

// Function to print the smallest
// missing non-negative integer
// up to every array indices
static void smlstNonNeg(int[] arr, int N)
{

    // Stores the smallest missing
    // non-negative integers between
    // start index to current index
    int smNonNeg = 0;

    // Store the boolean value to check
    // smNonNeg present between start
    // index to each index of the array
    bool[] hash = new bool[N + 1];

    for(int i = 0; i < N; i++)
    {
        hash[i] = false;
    }

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Since output always lies
        // in the range[0, N - 1]
        if (arr[i] >= 0 && arr[i] < N)
        {
            hash[arr[i]] = true;
        }

        // Check if smNonNeg is
        // present between start index
        // and current index or not
        while (hash[smNonNeg]) 
        {
            smNonNeg++;
        }

        // Print smallest missing
        // non-negative integer
        Console.Write(smNonNeg + " ");
    }
}

// Driver Code
public static void Main ()
{
    int[] arr = { 0, 1, 2, 3, 5 };
    int N = arr.Length;

    smlstNonNeg(arr, N);
}
}

// This code is contributed by code_hunt

```

**Output:** 

```
1 2 3 4 4

```

***时间复杂度：** O（N）*
***辅助空间：** O（N）*

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。