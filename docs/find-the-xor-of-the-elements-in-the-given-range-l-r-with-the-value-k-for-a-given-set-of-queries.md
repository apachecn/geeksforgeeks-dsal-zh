# 对于给定的一组查询，求给定范围[L，R]内元素与值 K 的异或

> 原文:[https://www . geeksforgeeks . org/find-the-xor-of-the-elements-in-给定范围-l-r-with-value-k-for-给定查询集/](https://www.geeksforgeeks.org/find-the-xor-of-the-elements-in-the-given-range-l-r-with-the-value-k-for-a-given-set-of-queries/)

给定一个数组 **arr[]** 和 **Q** 查询，任务是在 Q 查询之后找到结果更新的数组。查询有两种类型，由它们执行以下操作:

1.  **更新(L，R，K):** 用 K 对 L 到 R 范围内的每个元素进行异或运算
2.  **Display():** 显示给定数组的当前状态。

**例:**

> **输入:** arr[] = {1，2，3，4，5，6}，Q = 2
> 查询 1:更新(1，5，3)
> 查询 2:显示()
> **输出:**2 1 0 7 6
> **解释:**
> 更新查询对范围【1，5】内的所有元素进行异或运算。
> 执行更新查询后，显示上述数组进行显示查询，因为:
> 1 ^ 3 = 2
> 2 ^ 3 = 1
> 3 ^ 3 = 0
> 4 ^ 3 = 7
> 5 ^ 3 = 6
> **输入:** arr[] = {2，4，6，8，10}，Q = 3
> 查询 1:更新(1，3，2)
> 查询 2:更新(2，4，3)
> 执行第一次更新查询后，给定数组被更改为{0，6，4，8，10}。这是因为:
> 2 ^ 2 = 0
> 4 ^ 2 = 6
> 6 ^ 2 = 4
> 获取此数组后，此数组在第二次查询中进一步更改为{0，5，7，11，10}。这是因为:
> 6 ^ 3 = 5
> 4 ^ 3 = 7
> 8 ^ 3 = 11

**天真方法:**这个问题的天真方法是，对于每个更新查询，运行一个从 L 到 R 的循环，并用从 arr[L]到 arr[R]的所有元素对给定的 K 执行异或运算。为了执行显示查询，只需打印数组 arr[]。这种方法的时间复杂度是 O(NQ)，其中 N 是数组的长度，Q 是查询的数量。
**高效方法:**想法是用一个[卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)来解决这个问题。

*   空数组 res[]的长度与原始数组相同。
*   对于每个更新查询{ 1，R，K}，res[]数组被修改为:
    1.  异或 K 到 res[L]
    2.  异或 K 到 res[R + 1]
*   每当用户给出显示查询时:
    1.  将计数器变量“I”初始化为索引 1。
    2.  执行操作:

```
res[i] = res[i] ^ res[i - 1]
```

1.  将计数器变量“I”初始化为索引 0。
2.  对于数组中的每个索引，所需的答案是:

```
arr[i] ^ res[i]
```

以下是上述方法的实现:

## C++

```
// C++ implementation to perform the
// XOR range updates on an array
#include <bits/stdc++.h>
using namespace std;

// Function to perform the update operation
// on the given array
void update(int res[], int L, int R, int K)
{

    // Converting the indices to
    // 0 indexing.
    L -= 1;
    R -= 1;

    // Saving the XOR of K from the starting
    // index in the range [L, R].
    res[L] ^= K;

    // Saving the XOR of K at the ending index
    // in the given [L, R].
    res[R + 1] ^= K;
}

// Function to display the resulting array
void display(int arr[], int res[], int n)
{
    for (int i = 1; i < n; i++) {

        // Finding the resultant value in the
        // result array
        res[i] = res[i] ^ res[i - 1];
    }

    for (int i = 0; i < n; i++) {

        // Combining the effects of the updates
        // with the original array without
        // changing the initial array.
        cout << (arr[i] ^ res[i]) << " ";
    }
    cout << endl;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6, 8, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int res[N];
    memset(res, 0, sizeof(res));

    // Query 1
    int L = 1, R = 3, K = 2;
    update(res, L, R, K);

    // Query 2
    L = 2;
    R = 4;
    K = 3;
    update(res, L, R, K);

    // Query 3
    display(arr, res, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to perform the
// XOR range updates on an array
class GFG{

// Function to perform the update
// operation on the given array
static void update(int res[], int L,
                   int R, int K)
{

    // Converting the indices to
    // 0 indexing.
    L -= 1;
    R -= 1;

    // Saving the XOR of K from the
    // starting index in the range [L, R].
    res[L] ^= K;

    // Saving the XOR of K at the ending
    // index in the given [L, R].
    res[R + 1] ^= K;
}

// Function to display the resulting array
static void display(int arr[],
                    int res[], int n)
{
    int i;
    for(i = 1; i < n; i++)
    {

       // Finding the resultant value
       // in the result array
       res[i] = res[i] ^ res[i - 1];
    }

    for(i = 0; i < n; i++)
    {

       // Combining the effects of the
       // updates with the original array
       // without changing the initial array.
       System.out.print((arr[i] ^ res[i]) + " ");
    }
    System.out.println();
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 2, 4, 6, 8, 10 };
    int N = arr.length;
    int res[] = new int[N];

    // Query 1
    int L = 1, R = 3, K = 2;
    update(res, L, R, K);

    // Query 2
    L = 2;
    R = 4;
    K = 3;
    update(res, L, R, K);

    // Query 3
    display(arr, res, N);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to perform the
# XOR range updates on an array

# Function to perform the update operation
# on the given array
def update(res, L, R, K):

    # Converting the indices to
    # 0 indexing.
    L = L - 1
    R = R - 1

    # Saving the XOR of K from the starting
    # index in the range [L, R].
    res[L] = res[L] ^ K

    # Saving the XOR of K at the ending index
    # in the given [L, R].
    res[R + 1] = res[R + 1] ^ K

# Function to display the resulting array
def display(arr, res, n):

    for i in range(1, n):

        # Finding the resultant value in the
        # result array
        res[i] = res[i] ^ res[i - 1]

    for i in range(0, n):

        # Combining the effects of the updates
        # with the original array without
        # changing the initial array.
        print (arr[i] ^ res[i], end = " ")

# Driver code
arr = [ 2, 4, 6, 8, 10 ]
N = len(arr)
res = [0] * N

# Query 1
L = 1
R = 3
K = 2
update(res, L, R, K)

# Query 2
L = 2
R = 4
K = 3
update(res, L, R, K)

# Query 3
display(arr, res, N)

# This code is contributed by Pratik Basu
```

## C#

```
// C# implementation to perform the
// XOR range updates on an array
using System;
class GFG{

// Function to perform the update
// operation on the given array
static void update(int []res, int L,
                   int R, int K)
{

    // Converting the indices to
    // 0 indexing.
    L -= 1;
    R -= 1;

    // Saving the XOR of K from the
    // starting index in the range [L, R].
    res[L] ^= K;

    // Saving the XOR of K at the ending
    // index in the given [L, R].
    res[R + 1] ^= K;
}

// Function to display the resulting array
static void display(int []arr,
                    int []res, int n)
{
    int i;
    for(i = 1; i < n; i++)
    {

        // Finding the resultant value
        // in the result array
        res[i] = res[i] ^ res[i - 1];
    }

    for(i = 0; i < n; i++)
    {

        // Combining the effects of the
        // updates with the original array
        // without changing the initial array.
        Console.Write((arr[i] ^ res[i]) + " ");
    }
    Console.WriteLine();
}

// Driver code
public static void Main()
{
    int []arr = { 2, 4, 6, 8, 10 };
    int N = arr.Length;
    int []res = new int[N];

    // Query 1
    int L = 1, R = 3, K = 2;
    update(res, L, R, K);

    // Query 2
    L = 2;
    R = 4;
    K = 3;
    update(res, L, R, K);

    // Query 3
    display(arr, res, N);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation to perform the
// XOR range updates on an array

// Function to perform the update
// operation on the given array
function update(res, L, R, K)
{

    // Converting the indices to
    // 0 indexing.
    L -= 1;
    R -= 1;

    // Saving the XOR of K from the
    // starting index in the range [L, R].
    res[L] ^= K;

    // Saving the XOR of K at the ending
    // index in the given [L, R].
    res[R + 1] ^= K;
}

// Function to display the resulting array
function display(arr, res, n)
{
    let i;
    for(i = 1; i < n; i++)
    {

       // Finding the resultant value
       // in the result array
       res[i] = res[i] ^ res[i - 1];
    }

    for(i = 0; i < n; i++)
    {

       // Combining the effects of the
       // updates with the original array
       // without changing the initial array.
       document.write((arr[i] ^ res[i]) + " ");
    }
    document.write( "<br/>");
}

// Driver Code

    let arr = [ 2, 4, 6, 8, 10 ];
    let N = arr.length;
    let res = Array.from({length: N}, (_, i) => 0);

    // Query 1
    let L = 1, R = 3, K = 2;
    update(res, L, R, K);

    // Query 2
    L = 2;
    R = 4;
    K = 3;
    update(res, L, R, K);

    // Query 3
    display(arr, res, N);

</script>
```

**Output:** 

```
0 5 7 11 10
```

**时间复杂度:**

*   更新的时间复杂度为 *O(1)* 。
*   显示数组的时间复杂度为 *O(N)* 。

**辅助空间:** O(N)

**注意:**当更新查询与显示查询相比非常高时，这种方法非常有效。