# 按照给定的顺序排列数组的元素

> 原文:[https://www . geesforgeks . org/permute-数组的元素遵循给定的顺序/](https://www.geeksforgeeks.org/permute-the-elements-of-an-array-following-given-order/)

置换是将序列的成员重新排列成新的序列。比如**【a、b、c、d】**有 24 种排列。其中有**【b、a、d、c】****【d、a、b、c】****【a、d、b、c】**。
排列可以通过数组 **P[]** 来指定，其中 **P[i]** 表示排列中索引 **i** 处元素的位置。
例如，数组**【3，2，1，0】**表示将索引 0 处的元素映射到索引 3，索引 1 处的元素映射到索引 2，索引 2 处的元素映射到索引 1，索引 3 处的元素映射到索引 0 的排列。
给定 **N** 元素的数组 **arr[]** 和置换数组 **P[]** ，任务是基于置换数组 **P[]** 置换给定的数组 **arr[]** 。
**例:**

> **输入:** arr[] = {1，2，3，4}，P[] = {3，2，1，0}
> **输出:**4 3 2 1
> T6】输入: arr[] = {11，3 2，3，42}，P[] = {2，3，0，1}
> **输出:** 3 42 11 32

**方法:**每个排列都可以用一组独立的排列来表示，每个排列都是循环的，即它以固定的偏移量环绕移动所有元素。要找到并应用指示进入 **i** 的循环，只需继续前进(从 **i** 到**P【I】**)直到我们回到 **i** 。完成当前周期后，找到另一个尚未应用的周期。要检查这一点，涂抹后从 **P[i]** 中减去 **n** 。这意味着如果 **P[i]** 中的一个条目为负，我们已经执行了相应的移动。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to permute the the given
// array based on the given conditions
int permute(int A[], int P[], int n)
{
    // For each element of P
    for (int i = 0; i < n; i++) {
        int next = i;

        // Check if it is already
        // considered in cycle
        while (P[next] >= 0) {

            // Swap the current element according
            // to the permutation in P
            swap(A[i], A[P[next]]);
            int temp = P[next];

            // Subtract n from an entry in P
            // to make it negative which indicates
            // the corresponding move
            // has been performed
            P[next] -= n;
            next = temp;
        }
    }
}

// Driver code
int main()
{
    int A[] = { 5, 6, 7, 8 };
    int P[] = { 3, 2, 1, 0 };
    int n = sizeof(A) / sizeof(int);

    permute(A, P, n);

    // Print the new array after
    // applying the permutation
    for (int i = 0; i < n; i++)
        cout << A[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to permute the the given
// array based on the given conditions
static void permute(int A[], int P[], int n)
{
    // For each element of P
    for (int i = 0; i < n; i++)
    {
        int next = i;

        // Check if it is already
        // considered in cycle
        while (P[next] >= 0)
        {

            // Swap the current element according
            // to the permutation in P
            swap(A, i, P[next]);
            int temp = P[next];

            // Subtract n from an entry in P
            // to make it negative which indicates
            // the corresponding move
            // has been performed
            P[next] -= n;
            next = temp;
        }
    }
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 5, 6, 7, 8 };
    int P[] = { 3, 2, 1, 0 };
    int n = A.length;

    permute(A, P, n);

    // Print the new array after
    // applying the permutation
    for (int i = 0; i < n; i++)
        System.out.print(A[i]+ " ");

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to permute the the given
# array based on the given conditions
def permute(A, P, n):

    # For each element of P
    for i in range(n):
        next = i

        # Check if it is already
        # considered in cycle
        while (P[next] >= 0):

            # Swap the current element according
            # to the permutation in P
            t = A[i]
            A[i] = A[P[next]]
            A[P[next]] = t

            temp = P[next]

            # Subtract n from an entry in P
            # to make it negative which indicates
            # the corresponding move
            # has been performed
            P[next] -= n
            next = temp

# Driver code
if __name__ == '__main__':
    A = [5, 6, 7, 8]
    P = [3, 2, 1, 0]
    n = len(A)

    permute(A, P, n)

    # Print the new array after
    # applying the permutation
    for i in range(n):
        print(A[i], end = " ")

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to permute the the given
    // array based on the given conditions
    static void permute(int []A, int []P, int n)
    {
        // For each element of P
        for (int i = 0; i < n; i++)
        {
            int next = i;

            // Check if it is already
            // considered in cycle
            while (P[next] >= 0)
            {

                // Swap the current element according
                // to the permutation in P
                swap(A, i, P[next]);
                int temp = P[next];

                // Subtract n from an entry in P
                // to make it negative which indicates
                // the corresponding move
                // has been performed
                P[next] -= n;
                next = temp;
            }
        }
    }

    static int[] swap(int []arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Driver code
    public static void Main()
    {
        int []A = { 5, 6, 7, 8 };
        int []P = { 3, 2, 1, 0 };
        int n = A.Length;

        permute(A, P, n);

        // Print the new array after
        // applying the permutation
        for (int i = 0; i < n; i++)
            Console.Write(A[i]+ " ");

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to permute the the given
// array based on the given conditions
function permute(A, P, n) {
    // For each element of P
    for (let i = 0; i < n; i++) {
        let next = i;

        // Check if it is already
        // considered in cycle
        while (P[next] >= 0) {

            // Swap the current element according
            // to the permutation in P
            let x = A[i];
            A[i] = A[P[next]];
            A[P[next]] = x;

            let temp = P[next];

            // Subtract n from an entry in P
            // to make it negative which indicates
            // the corresponding move
            // has been performed
            P[next] -= n;
            next = temp;
        }
    }
}

// Driver code

let A = [5, 6, 7, 8];
let P = [3, 2, 1, 0];
let n = A.length;

permute(A, P, n);

// Print the new array after
// applying the permutation
for (let i = 0; i < n; i++)
    document.write(A[i] + " ");

</script>
```

**Output:** 

```
8 7 6 5
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)