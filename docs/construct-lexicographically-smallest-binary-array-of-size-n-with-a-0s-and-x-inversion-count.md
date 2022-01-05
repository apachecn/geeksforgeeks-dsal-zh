# 用 A0 和 X 反转计数构建字典最小的二进制数组

> 原文:[https://www . geeksforgeeks . org/construct-按字典顺序排列-最小-二进制-大小为 n 的数组-带-0 和-x-反转-计数/](https://www.geeksforgeeks.org/construct-lexicographically-smallest-binary-array-of-size-n-with-a-0s-and-x-inversion-count/)

给定三个数字 **N** 、 **A** 和 **X** ，任务是构造大小为 **N** 的字典最小的[二进制数组](https://www.geeksforgeeks.org/sort-binary-array-using-one-traversal/)，包含 **A 0** s 并具有 **X** 的[反转](https://www.geeksforgeeks.org/counting-inversions/)计数。

**示例:**

> **输入:** N=5，A=2，X=1
> **输出:** 0 1 0 1 1
> **说明:**
> 此数组中的逆序数为 1(第 2 和第 3 个索引)。
> 
> **输入:** N=5，A=2，X = 3
> T3】输出: 0 1 1 1 0

**方法:**基于以下观察，使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)可以解决给定的问题:

> 1.  The array of **A0** s with **0** inversion starts with all **0** s, and then all **1** s. 。
> 
>  **i 处的元素 **0** 和索引 **j 处的元素 **1** 被交换，则反转计数增加 **1 的计数***   The maximum possible inversion count is **a * (n-a).******

按照以下步骤解决问题:

*   如果 **X** 大于 **A*(N-A)** ，则打印 **-1** 后返回。
*   初始化一个大小为 **N** 的数组 **arr[]** ，用 **0** s 填充第一个 **A** 索引，用 **1** s 填充剩余的索引
*   将两个变量**初始化为**【A-1】**，将**初始化为 **N-1** 到[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)。****
*   迭代至 **X** 大于 **0** 和 **curr** ，不小于 **0** ，并执行以下步骤:
    *   如果 **X** 大于或等于**prev cur**，则执行以下操作:
        *   [将**的两个元素替换为【上一个】、**和**的两个元素。**](https://www.geeksforgeeks.org/vectorat-vectorswap-c-stl/)
        *   从 **X** 中减去**预弯曲**。
        *   通过 **1 减少**上一个**和**当前**。**
    *   否则，请执行以下操作:
        *   交换两个元素**arr【curr】**和**arr【cur+1】**。
        *   将**电流**增加 **1** 和**T5】将 **X** 减少 **1。****
*   [印阵](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to construct lexicographically
// smallest binary string of length N, having
// A 0s and X inversions
void binaryArrayInversions(int N, int A, int X)
{
    // If X inversions are not possible
    if (A * (N - A) < X) {
        cout << "-1";
        return;
    }
    // Initialize array and fill with 0
    int Arr[N] = { 0 };

    // Fill last N-A indices with 1
    fill(Arr + A, Arr + N, 1);

    // Stores the index of current 0
    int cur = A - 1;

    // Stores the index of current 1
    int prev = N - 1;

    // Iterate until X is greater than
    // 0 and cur is greater than equal
    // to 0
    while (X && cur >= 0) {
        // If X is greater than or
        // equal to the prev-cur

        if (X >= prev - cur) {
            // Swap current 0 and current 1
            swap(Arr[prev], Arr[cur]);

            // Update X
            X -= prev - cur;

            // Decrement prev and cur by 1
            prev--;
            cur--;
        }
        // Otherwise
        else {
            // Swap current 0 with the next index
            swap(Arr[cur], Arr[cur + 1]);

            // Increment cur by 1
            cur++;
            // Decrement X by 1
            X--;
        }
    }
    // Print the array
    for (auto u : Arr)
        cout << u << " ";
}
// Driver code
int main()
{
    // Input
    int N = 5;
    int A = 2;
    int X = 1;

    // Function call
    binaryArrayInversions(N, A, X);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to construct lexicographically
// smallest binary string of length N, having
// A 0s and X inversions
static void binaryArrayInversions(int N, int A, int X)
{

    // If X inversions are not possible
    if (A * (N - A) < X)
    {
        System.out.println("-1");
        return;
    }

    // Initialize array and fill with 0
    int []Arr = new int[N];

    // Fill last N-A indices with 1
    Arrays.fill(Arr, 0);

    for(int i = A; i < N; i++)
        Arr[i] = 1;

    // Stores the index of current 0
    int cur = A - 1;

    // Stores the index of current 1
    int prev = N - 1;

    // Iterate until X is greater than
    // 0 and cur is greater than equal
    // to 0
    while (X != 0 && cur >= 0)
    {

        // If X is greater than or
        // equal to the prev-cur
        if (X >= prev - cur)
        {

            // Swap current 0 and current 1
            int temp = Arr[prev];
            Arr[prev] =  Arr[cur];
            Arr[cur] = temp;

            // Update X
            X -= prev - cur;

            // Decrement prev and cur by 1
            prev--;
            cur--;
        }

        // Otherwise
        else
        {

            // Swap current 0 with the next index
            int temp = Arr[cur];
            Arr[cur] = Arr[cur + 1];
            Arr[cur + 1] = temp;

            // Increment cur by 1
            cur++;

            // Decrement X by 1
            X--;
        }
    }

    // Print the array
    for(int i = 0; i < Arr.length; i++)
        System.out.print(Arr[i] + " ");
}

// Driver code
public static void main(String args[])
{

    // Input
    int N = 5;
    int A = 2;
    int X = 1;

    // Function call
    binaryArrayInversions(N, A, X);
}
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to construct lexicographically
# smallest binary string of length N, having
# A 0s and X inversions
def binaryArrayInversions(N, A, X):
    # If X inversions are not possible
    if (A * (N - A) < X):
        print("-1")
        return
    # Initialize array and fill with 0
    Arr = [0]*N

    for i in range(A,N):
        Arr[i]=1

    # Stores the index of current 0
    cur = A - 1

    # Stores the index of current 1
    prev = N - 1

    # Iterate until X is greater than
    # 0 and cur is greater than equal
    # to 0
    while (X and cur >= 0):
        # If X is greater than or
        # equal to the prev-cur

        if (X >= prev - cur):
            # Swap current 0 and current 1
            Arr[prev], Arr[cur] = Arr[cur],Arr[prev]

            # Update X
            X -= prev - cur

            # Decrement prev and cur by 1
            prev -= 1
            cur -= 1
        # Otherwise
        else:
            # Swap current 0 with the next index
            Arr[cur], Arr[cur + 1] = Arr[cur + 1], Arr[cur]

            # Increment cur by 1
            cur += 1
            # Decrement X by 1
            X -= 1

    # Print the array
    for u in Arr:
        print(u, end = " ")

# Driver code
if __name__ == '__main__':
    # Input
    N = 5
    A = 2
    X = 1

    # Function call
    binaryArrayInversions(N, A, X)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to construct lexicographically
// smallest binary string of length N, having
// A 0s and X inversions
static void binaryArrayInversions(int N, int A, int X)
{

    // If X inversions are not possible
    if (A * (N - A) < X) {
        Console.Write("-1");
        return;
    }
    // Initialize array and fill with 0
    int []Arr = new int[N];

    // Fill last N-A indices with 1
    Array.Clear(Arr, 0, N);
    for(int i=A;i<N;i++)
      Arr[i] = 1;

    // Stores the index of current 0
    int cur = A - 1;

    // Stores the index of current 1
    int prev = N - 1;

    // Iterate until X is greater than
    // 0 and cur is greater than equal
    // to 0
    while (X!=0 && cur >= 0)
    {

        // If X is greater than or
        // equal to the prev-cur

        if (X >= prev - cur)
        {

            // Swap current 0 and current 1
            int temp = Arr[prev];
            Arr[prev] =  Arr[cur];
            Arr[cur] = temp;

            // Update X
            X -= prev - cur;

            // Decrement prev and cur by 1
            prev--;
            cur--;
        }
        // Otherwise
        else {
            // Swap current 0 with the next index
            int temp = Arr[cur];
            Arr[cur] = Arr[cur + 1];
            Arr[cur + 1] = temp;

            // Increment cur by 1
            cur++;
            // Decrement X by 1
            X--;
        }
    }
    // Print the array
    for(int i = 0; i < Arr.Length; i++)
        Console.Write(Arr[i] +" ");
}
// Driver code
public static void Main()
{

    // Input
    int N = 5;
    int A = 2;
    int X = 1;

    // Function call
    binaryArrayInversions(N, A, X);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to construct lexicographically
// smallest binary string of length N, having
// A 0s and X inversions
function binaryArrayInversions(N, A, X) {
    // If X inversions are not possible
    if (A * (N - A) < X) {
        document.write("-1");
        return;
    }
    // Initialize array and fill with 0
    let Arr = new Array(N).fill(0);

    // Fill last N-A indices with 1

    Arr.forEach((item, i) => {
        if (i >= Arr.length - (N - A)) {
            Arr[i] = 1
        }
    })

    // Stores the index of current 0
    let cur = A - 1;

    // Stores the index of current 1
    let prev = N - 1;

    // Iterate until X is greater than
    // 0 and cur is greater than equal
    // to 0
    while (X && cur >= 0) {
        // If X is greater than or
        // equal to the prev-cur

        if (X >= prev - cur) {
            // Swap current 0 and current 1
            let temp = Arr[prev];
            Arr[prev] = Arr[cur];
            Arr[cur] = temp;

            // Update X
            X -= prev - cur;

            // Decrement prev and cur by 1
            prev--;
            cur--;
        }
        // Otherwise
        else {
            // Swap current 0 with the next index
            let temp = Arr[cur + 1];
            Arr[cur + 1] = Arr[cur];
            Arr[cur] = temp;

            // Increment cur by 1
            cur++;
            // Decrement X by 1
            X--;
        }
    }
    // Print the array

    document.write(Arr);
}
// Driver code

// Input
let N = 5;
let A = 2;
let X = 1;

// Function call
binaryArrayInversions(N, A, X);

</script>
```

**Output**

```
0 1 0 1 1 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)