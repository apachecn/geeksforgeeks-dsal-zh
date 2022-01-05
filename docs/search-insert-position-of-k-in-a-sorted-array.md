# 搜索排序数组中 K 的插入位置

> 原文:[https://www . geeksforgeeks . org/search-insert-k 在排序数组中的位置/](https://www.geeksforgeeks.org/search-insert-position-of-k-in-a-sorted-array/)

给定一个由 **N** 个不同整数和一个整数 **K** 组成的[排序数组](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/) **arr[]** ，任务是找到 K 的索引，如果它存在于数组 **arr[]** 。否则，找到必须插入 **K** 的索引，以保持数组排序。

**示例:**

> **输入:** arr[] = {1，3，5，6}，K = 5
> **输出:** 2
> **解释:**由于在索引 2 中发现 5 为 arr[2] = 5，因此输出为 2。
> 
> **输入:** arr[] = {1，3，5，6}，K = 2
> **输出:** 1
> **解释:**因为数组中不存在 2，但可以在索引 1 处插入 2，使数组排序。

**天真方法:**按照以下步骤解决问题:

*   [迭代数组的每个元素](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr[]** 并搜索整数 **K** 。
*   如果发现任何数组元素等于 **K** ，则打印 K 的索引
*   否则，如果发现任何数组元素大于 **K** ，则打印该索引作为 **K** 的插入位置。如果没有发现元素超过 **K** ， **K** 必须插入到最后一个数组元素之后。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find insert position of K
int find_index(int arr[], int n, int K)
{
    // Traverse the array
    for (int i = 0; i < n; i++)

        // If K is found
        if (arr[i] == K)
            return i;

        // If current array element
        // exceeds K
        else if (arr[i] > K)
            return i;

    // If all elements are smaller
    // than K
    return n;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 2;
    cout << find_index(arr, n, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find insert position of K
static int find_index(int[] arr, int n, int K)
{

    // Traverse the array
    for(int i = 0; i < n; i++)

        // If K is found
        if (arr[i] == K)
            return i;

        // If current array element
        // exceeds K
        else if (arr[i] > K)
            return i;

    // If all elements are smaller
    // than K
    return n;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 3, 5, 6 };
    int n = arr.length;
    int K = 2;

    System.out.println(find_index(arr, n, K));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find insert position of K
def find_index(arr, n, K):

    # Traverse the array
    for i in range(n):

        # If K is found
        if arr[i] == K:
            return i

        # If arr[i] exceeds K
        elif arr[i] > K:
            return i

    # If all array elements are smaller
    return n

# Driver Code
arr = [1, 3, 5, 6]
n = len(arr)
K = 2
print(find_index(arr, n, K))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find insert position of K
static int find_index(int[] arr, int n, int K)
{

    // Traverse the array
    for(int i = 0; i < n; i++)

        // If K is found
        if (arr[i] == K)
            return i;

        // If current array element
        // exceeds K
        else if (arr[i] > K)
            return i;

    // If all elements are smaller
    // than K
    return n;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 3, 5, 6 };
    int n = arr.Length;
    int K = 2;

    Console.WriteLine(find_index(arr, n, K));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find insert position of K
function find_index(arr, n, K)
{

    // Traverse the array
    for(let i = 0; i < n; i++)

        // If K is found
        if (arr[i] == K)
            return i;

        // If current array element
        // exceeds K
        else if (arr[i] > K)
            return i;

    // If all elements are smaller
    // than K
    return n;
}

// Driver code
let arr = [ 1, 3, 5, 6 ];
let n = arr.length;
let K = 2;

document.write(find_index(arr, n, K));

// This code is contributed by splevel62  

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效途径:**优化上述途径，思路是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。按照以下步骤解决问题:

*   将**开始**和**结束**设置为 **0** 和**N–1**，其中**开始**和**结束**变量分别表示搜索空间的下限和上限。
*   计算**中间=(开始+结束)/ 2** 。
*   如果发现**arr【mid】**等于 **K** ，则打印 **mid** 作为所需答案。
*   如果 **arr【中】**超过 **K** ，将**设为低=中+ 1** 。否则，将**设置为高=中-1**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find insert position of K
int find_index(int arr[], int n, int K)
{
    // Lower and upper bounds
    int start = 0;
    int end = n - 1;

    // Traverse the search space
    while (start <= end) {
        int mid = (start + end) / 2;

        // If K is found
        if (arr[mid] == K)
            return mid;

        else if (arr[mid] < K)
            start = mid + 1;

        else
            end = mid - 1;
    }

    // Return insert position
    return end + 1;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 2;
    cout << find_index(arr, n, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find insert position of K
static int find_index(int[] arr, int n, int K)
{

    // Lower and upper bounds
    int start = 0;
    int end = n - 1;

    // Traverse the search space
    while (start <= end)
    {
        int mid = (start + end) / 2;

        // If K is found
        if (arr[mid] == K)
            return mid;

        else if (arr[mid] < K)
            start = mid + 1;

        else
            end = mid - 1;
    }

    // Return insert position
    return end + 1;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 3, 5, 6 };
    int n = arr.length;
    int K = 2;

    System.out.println(find_index(arr, n, K));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find insert position of K
def find_index(arr, n, B):

    # Lower and upper bounds
    start = 0
    end = n - 1

    # Traverse the search space
    while start<= end:

        mid =(start + end)//2

        if arr[mid] == K:
            return mid

        elif arr[mid] < K:
            start = mid + 1
        else:
            end = mid-1

    # Return the insert position
    return end + 1

# Driver Code
arr = [1, 3, 5, 6]
n = len(arr)
K = 2
print(find_index(arr, n, K))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find insert position of K
static int find_index(int[] arr, int n, int K)
{

    // Lower and upper bounds
    int start = 0;
    int end = n - 1;

    // Traverse the search space
    while (start <= end)
    {
        int mid = (start + end) / 2;

        // If K is found
        if (arr[mid] == K)
            return mid;

        else if (arr[mid] < K)
            start = mid + 1;

        else
            end = mid - 1;
    }

    // Return insert position
    return end + 1;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 3, 5, 6 };
    int n = arr.Length;
    int K = 2;

    Console.WriteLine(find_index(arr, n, K));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find insert position of K
function find_index(arr, n, K)
{
    // Lower and upper bounds
    let start = 0;
    let end = n - 1;

    // Traverse the search space
    while (start <= end) {
        let mid = Math.floor((start + end) / 2);

        // If K is found
        if (arr[mid] == K)
            return mid;

        else if (arr[mid] < K)
            start = mid + 1;

        else
            end = mid - 1;
    }

    // Return insert position
    return end + 1;
}

// Driver Code
    let arr = [ 1, 3, 5, 6 ];
    let n = arr.length;
    let K = 2;
    document.write(find_index(arr, n, K) + "<br>");

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*