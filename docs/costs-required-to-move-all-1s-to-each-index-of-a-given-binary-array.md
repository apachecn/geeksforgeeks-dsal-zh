# 将所有 1 移动到给定二进制数组的每个索引所需的成本

> 原文:[https://www . geesforgeks . org/costs-将所有 1 移动到给定二进制数组的每个索引所需的成本/](https://www.geeksforgeeks.org/costs-required-to-move-all-1s-to-each-index-of-a-given-binary-array/)

给定一个**二进制数组**，其中，将一个元素从索引 **i** 移动到索引 **j** 需要[ABS(I–j)](https://www.geeksforgeeks.org/program-to-find-absolute-value-of-a-given-number/)成本。任务是找到将所有 **1** s 移动到给定数组的每个索引的成本。

**示例:**

> **输入:** arr[] = {0，1，0，1}
> **输出** : 4 2 2 2
> **解释:**
> 将元素从索引 1、索引 3 移动到索引 0 需要 ABS(0–1)+ABS(0–3)= 4。
> 将元素从指数 1、指数 3 移动到指数 1 需要 ABS(1–1)+ABS(1–3)= 2。
> 将元素从指数 1、指数 2 移动到指数 2 需要 ABS(2–1)+ABS(2–3)= 2。
> 将元素从指数 1、指数 2 移动到指数 3 需要 ABS(3–1)+ABS(3–3)= 2。
> 因此，要求的输出是 4 2 2 2。
> 
> **输入:** arr[] = {1，1，1}
> **输出:** 3 2 3

**天真方法:**解决这个问题最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于给定数组的每个数组元素，打印将给定数组的所有 **1** 移动到当前索引的成本。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the cost
// to move all 1s to each index
void costMove1s(int arr[], int N)
{
    // Traverse the array.
    for (int i = 0; i < N; i++) {

        // Stores cost to move
        // all 1s at current index
        int cost = 0;

        // Calculate cost to move
        // all 1s at current index
        for (int j = 0; j < N;
                          j++) {

            // If current element
            // of the array is 1.
            if (arr[j] == 1) {

                // Update cost
                cost += abs(i - j);
            }
        }
        cout<<cost<<" ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 0, 1};
    int N = sizeof(arr) / sizeof(arr[0]);

    costMove1s(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to print the cost
// to move all 1s to each index
static void costMove1s(int[] arr, int N)
{

    // Traverse the array.
    for(int i = 0; i < N; i++)
    {

        // Stores cost to move
        // all 1s at current index
        int cost = 0;

        // Calculate cost to move
        // all 1s at current index
        for(int j = 0; j < N; j++)
        {

            // If current element
            // of the array is 1.
            if (arr[j] == 1)
            {

                // Update cost
                cost += Math.abs(i - j);
            }
        }
        System.out.print(cost + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 0, 1, 0, 1 };
    int N = arr.length;

    costMove1s(arr, N);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Pyhton3 program to implement
# the above approach

# Function to print the cost
# to move all 1s to each index
def costMove1s(arr, N):

    # Traverse the array.
    for i in range(0, N):

        # Stores cost to move
        # all 1s at current index
        cost = 0

        # Calculate cost to move
        # all 1s at current index
        for j in range(0, N):

            # If current element
            # of the array is 1.
            if (arr[j] == 1):

                # Update cost
                cost = cost + abs(i - j)

        print(cost, end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 0, 1, 0, 1 ]
    N = len(arr)

    costMove1s(arr, N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print the cost
// to move all 1s to each index
static void costMove1s(int[] arr, int N)
{

    // Traverse the array.
    for(int i = 0; i < N; i++)
    {

        // Stores cost to move
        // all 1s at current index
        int cost = 0;

        // Calculate cost to move
        // all 1s at current index
        for(int j = 0; j < N; j++)
        {

            // If current element
            // of the array is 1.
            if (arr[j] == 1)
            {

                // Update cost
                cost += Math.Abs(i - j);
            }
        }
        Console.Write(cost + " ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 0, 1, 0, 1 };
    int N = arr.Length;

    costMove1s(arr, N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to print the cost
// to move all 1s to each index
function costMove1s(arr, N)
{
    // Traverse the array.
    for (let i = 0; i < N; i++) {

        // Stores cost to move
        // all 1s at current index
        let cost = 0;

        // Calculate cost to move
        // all 1s at current index
        for (let j = 0; j < N;
                        j++) {

            // If current element
            // of the array is 1.
            if (arr[j] == 1) {

                // Update cost
                cost += Math.abs(i - j);
            }
        }
        document.write(cost + " ");
    }
}

// Driver Code

    let arr = [ 0, 1, 0, 1];
    let N = arr.length;

    costMove1s(arr, N);

//This code is contributed by Mayank Tyagi
</script>
```

**Output:** 

```
4 2 2 2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，思路是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并找到使用[前缀求和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)从给定数组的每个索引的左侧和右侧移动所有 **1** 的成本。按照以下步骤解决问题:

*   初始化一个数组，说 **cost[]** 来存储在给定数组的每个索引处移动所有 **1** 的成本。
*   初始化两个变量，说**成本左**、**成本右**存储成本，分别从每个指标的左侧和右侧移动所有 **1** 。
*   从左到右遍历给定数组，将 **costLeft** 的值增加左侧的 **1** 的数量，将**结果【I】**的值增加 **costLeft** ..
*   从右到左遍历给定数组，将 **costRight** 的值增加右侧 **1** 的个数，将**结果【I】**的值增加 **costRight** 。
*   最后打印**成本[]** 数组。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the cost
// to move all 1s to each index
void costMove1s(int arr[], int N)
{

    // cost[i] Stores cost to move
    // all 1s at index i
    int cost[N] = { 0 };

    // Stores count of 1s on
    // the left side of index i
    int cntLeft = 0;

    // Stores cost to move all 1s
    // from the left side of index i
    // to index i
    int costLeft = 0;

    // Traverse the array from
    // left to right.
    for (int i = 0; i < N; i++) {

        // Update cost to move
        // all 1s from left side
        // of index i to index i
        costLeft += cntLeft;

        // Update cost[i] to cntLeft
        cost[i] += costLeft;

        // If current element is 1.
        if (arr[i] == 1) {
            cntLeft++;
        }
    }

    // Stores count of 1s on
    // the right side of index i
    int cntRight = 0;

    // Stores cost to move all 1s
    // from the right of index i
    // to index i
    int costRight = 0;

    // Traverse the array from
    // right to left.
    for (int i = N - 1; i >= 0;
                          i--) {

        // Update cost to move
        // all 1s from right side
        // of index i to index i
        costRight += cntRight;

        // Update cost[i]
        // to costRight
        cost[i] += costRight;

        // If current element
        // is 1.
        if (arr[i] == 1) {
            cntRight++;
        }
    }

    // Print cost to move all 1s
    for(int i = 0; i< N; i++) {
        cout<<cost[i]<<" ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 0, 1};
    int N = sizeof(arr) / sizeof(arr[0]);
    costMove1s(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to print the cost
// to move all 1s to each index
static void costMove1s(int arr[], int N)
{

    // cost[i] Stores cost to move
    // all 1s at index i
    int cost[] = new int[N];

    // Stores count of 1s on
    // the left side of index i
    int cntLeft = 0;

    // Stores cost to move all 1s
    // from the left side of index i
    // to index i
    int costLeft = 0;

    // Traverse the array from
    // left to right.
    for(int i = 0; i < N; i++)
    {

        // Update cost to move
        // all 1s from left side
        // of index i to index i
        costLeft += cntLeft;

        // Update cost[i] to cntLeft
        cost[i] += costLeft;

        // If current element is 1.
        if (arr[i] == 1)
        {
            cntLeft++;
        }
    }

    // Stores count of 1s on
    // the right side of index i
    int cntRight = 0;

    // Stores cost to move all 1s
    // from the right of index i
    // to index i
    int costRight = 0;

    // Traverse the array from
    // right to left.
    for(int i = N - 1; i >= 0; i--)
    {

        // Update cost to move
        // all 1s from right side
        // of index i to index i
        costRight += cntRight;

        // Update cost[i]
        // to costRight
        cost[i] += costRight;

        // If current element
        // is 1.
        if (arr[i] == 1)
        {
            cntRight++;
        }
    }

    // Print cost to move all 1s
    for(int i = 0; i < N; i++)
    {
        System.out.print(cost[i] + " ");
    }
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 0, 1, 0, 1 };
    int N = arr.length;

    // Function Call
    costMove1s(arr, N);
}
}

// This code is contributed by math_lover
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print the cost
# to move all 1s to each index
def costMove1s(arr, N):

    # cost[i] Stores cost to move
    # all 1s at index i
    cost = [0] * N

    # Stores count of 1s on
    # the left side of index i
    cntLeft = 0

    # Stores cost to move all 1s
    # from the left side of index i
    # to index i
    costLeft = 0

    # Traverse the array from
    # left to right.
    for i in range(N):

        # Update cost to move
        # all 1s from left side
        # of index i to index i
        costLeft += cntLeft

        # Update cost[i] to cntLeft
        cost[i] += costLeft

        # If current element is 1.
        if (arr[i] == 1):
            cntLeft += 1

    # Stores count of 1s on
    # the right side of index i
    cntRight = 0

    # Stores cost to move all 1s
    # from the right of index i
    # to index i
    costRight = 0

    # Traverse the array from
    # right to left.
    for i in range(N - 1, -1, -1):

        # Update cost to move
        # all 1s from right side
        # of index i to index i
        costRight += cntRight

        # Update cost[i]
        # to costRight
        cost[i] += costRight

        # If current element
        # is 1.
        if (arr[i] == 1):
            cntRight += 1

    # Print cost to move all 1s
    for i in range(N):
        print(cost[i], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 0, 1, 0, 1 ]
    N = len(arr)

    costMove1s(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print the cost
// to move all 1s to each index
static void costMove1s(int []arr, int N)
{

    // cost[i] Stores cost to move
    // all 1s at index i
    int []cost = new int[N];

    // Stores count of 1s on
    // the left side of index i
    int cntLeft = 0;

    // Stores cost to move all 1s
    // from the left side of index i
    // to index i
    int costLeft = 0;

    // Traverse the array from
    // left to right.
    for(int i = 0; i < N; i++)
    {

        // Update cost to move
        // all 1s from left side
        // of index i to index i
        costLeft += cntLeft;

        // Update cost[i] to cntLeft
        cost[i] += costLeft;

        // If current element is 1.
        if (arr[i] == 1)
        {
            cntLeft++;
        }
    }

    // Stores count of 1s on
    // the right side of index i
    int cntRight = 0;

    // Stores cost to move all 1s
    // from the right of index i
    // to index i
    int costRight = 0;

    // Traverse the array from
    // right to left.
    for(int i = N - 1; i >= 0; i--)
    {

        // Update cost to move
        // all 1s from right side
        // of index i to index i
        costRight += cntRight;

        // Update cost[i]
        // to costRight
        cost[i] += costRight;

        // If current element
        // is 1.
        if (arr[i] == 1)
        {
            cntRight++;
        }
    }

    // Print cost to move all 1s
    for(int i = 0; i < N; i++)
    {
        Console.Write(cost[i] + " ");
    }
}

// Driver Code
public static void Main (String[] args)
{
    int []arr = { 0, 1, 0, 1 };
    int N = arr.Length;

    // Function Call
    costMove1s(arr, N);
}
}

// This code is contributed by math_lover
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to print the cost
// to move all 1s to each index
function costMove1s(arr, N)
{

    // cost[i] Stores cost to move
    // all 1s at index i
    var cost = Array(N).fill(0);

    // Stores count of 1s on
    // the left side of index i
    var cntLeft = 0;

    // Stores cost to move all 1s
    // from the left side of index i
    // to index i
    var costLeft = 0;

    // Traverse the array from
    // left to right.
    for(var i = 0; i < N; i++)
    {

        // Update cost to move
        // all 1s from left side
        // of index i to index i
        costLeft += cntLeft;

        // Update cost[i] to cntLeft
        cost[i] += costLeft;

        // If current element is 1.
        if (arr[i] == 1)
        {
            cntLeft++;
        }
    }

    // Stores count of 1s on
    // the right side of index i
    var cntRight = 0;

    // Stores cost to move all 1s
    // from the right of index i
    // to index i
    var costRight = 0;

    // Traverse the array from
    // right to left.
    for(var i = N - 1; i >= 0; i--)
    {

        // Update cost to move
        // all 1s from right side
        // of index i to index i
        costRight += cntRight;

        // Update cost[i]
        // to costRight
        cost[i] += costRight;

        // If current element
        // is 1.
        if (arr[i] == 1)
        {
            cntRight++;
        }
    }

    // Print cost to move all 1s
    for(var i = 0; i< N; i++)
    {
        document.write(cost[i] + " ");
    }
}

// Driver Code
var arr = [ 0, 1, 0, 1 ];
var N = arr.length;

costMove1s(arr, N);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
4 2 2 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)