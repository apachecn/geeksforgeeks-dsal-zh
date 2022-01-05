# 在 C

中实现上界()和下界()

> 原文:[https://www . geeksforgeeks . org/implementing-upper _ bound-and-lower _ bound-in-c/](https://www.geeksforgeeks.org/implementing-upper_bound-and-lower_bound-in-c/)

给定一个排序后的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】****N**整数和一个数字 **K** ，任务是编写 [C](https://www.geeksforgeeks.org/c/) 程序，在给定数组中找到 **K** 的[上界()](https://www.geeksforgeeks.org/stdupper_bound-in-cpp/)和[下界()](https://www.geeksforgeeks.org/lower_bound-in-cpp/)。
**举例:**

> **输入:** arr[] = {4，6，10，12，18，20}，K = 6
> **输出:**
> 6 的下限在索引 1 处为 6
> 6 的上限在索引 2 处为 10
> **输入:** arr[] = {4，6，10，12，18，20}，K = 20
> **输出:**
> 20 的下限为 20

**进场:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。以下是步骤:

*   **对于下界():**
    1.  将**开始索引**初始化为 **0** ，将**结束索引**初始化为**N–1**。
    2.  将 **K** 与数组的中间元素(比如 **arr【中】**)进行比较。
    3.  如果中间元素大于等于 **K** ，则更新 endIndex 作为中间索引(**中间**)。
    4.  否则将开始索引更新为中间+ 1。
    5.  重复以上步骤，直到**起始索引**小于**结束索引**。
    6.  经过以上所有步骤后，**起始索引**就是给定数组中 **K** 的**下界**。
*   **对于上限():**
    1.  将**开始索引**初始化为 **0** ，将**结束索引**初始化为**N–1**。
    2.  将 **K** 与数组的中间元素(比如 **arr【中】**)进行比较。
    3.  如果中间元素小于或等于 **K** ，则将开始索引更新为中间索引+ 1( **中间** + 1)。
    4.  否则将 endIndex 更新为 mid。
    5.  重复以上步骤，直到**起始索引**小于**结束索引**。
    6.  经过以上所有步骤后，**开始索引**就是给定数组中 **K** 的**上限**。

下面是上述方法的迭代和递归实现:

## 迭代解

```
// C program for iterative implementation
// of the above approach

#include <stdio.h>

// Function to implement lower_bound
int lower_bound(int arr[], int N, int X)
{
    int mid;

    // Initialise starting index and
    // ending index
    int low = 0;
    int high = N;

    // Till low is less than high
    while (low < high) {
        mid = low + (high - low) / 2;

        // If X is less than or equal
        // to arr[mid], then find in
        // left subarray
        if (X <= arr[mid]) {
            high = mid;
        }

        // If X is greater arr[mid]
        // then find in right subarray
        else {
            low = mid + 1;
        }
    }

    // if X is greater than arr[n-1]
    if(low < N && arr[low] < X) {
       low++;
    }

    // Return the lower_bound index
    return low;
}

// Function to implement upper_bound
int upper_bound(int arr[], int N, int X)
{
    int mid;

    // Initialise starting index and
    // ending index
    int low = 0;
    int high = N;

    // Till low is less than high
    while (low < high) {
        // Find the middle index
        mid = low + (high - low) / 2;

        // If X is greater than or equal
        // to arr[mid] then find
        // in right subarray
        if (X >= arr[mid]) {
            low = mid + 1;
        }

        // If X is less than arr[mid]
        // then find in left subarray
        else {
            high = mid;
        }
    }

    // if X is greater than arr[n-1]
    if(low < N && arr[low] <= X) {
       low++;
    }

    // Return the upper_bound index
    return low;
}

// Function to implement lower_bound
// and upper_bound of X
void printBound(int arr[], int N, int X)
{
    int idx;

    // If lower_bound doesn't exists
    if (lower_bound(arr, N, X) == N) {
        printf("Lower bound doesn't exist");
    }
    else {

        // Find lower_bound
        idx = lower_bound(arr, N, X);
        printf("Lower bound of %d is"
               "% d at index % d\n ",
               X,
               arr[idx], idx);
    }

    // If upper_bound doesn't exists
    if (upper_bound(arr, N, X) == N) {
        printf("Upper bound doesn't exist");
    }
    else {

        // Find upper_bound
        idx = upper_bound(arr, N, X);
        printf("Upper bound of %d is"
               "% d at index % d\n ",
               X,
               arr[idx], idx);
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 4, 6, 10, 12, 18, 20 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Element whose lower bound and
    // upper bound to be found
    int X = 6;

    // Function Call
    printBound(arr, N, X);
    return 0;
}
```

## 递归解

```
// C program for recursive implementation
// of the above approach

#include <stdio.h>

// Recursive implementation of
// lower_bound
int lower_bound(int arr[], int low,
                int high, int X)
{

    // Base Case
    if (low > high) {
        return low;
    }

    // Find the middle index
    int mid = low + (high - low) / 2;

    // If arr[mid] is greater than
    // or equal to X then search
    // in left subarray
    if (arr[mid] >= X) {
        return lower_bound(arr, low,
                           mid - 1, X);
    }

    // If arr[mid] is less than X
    // then search in right subarray
    return lower_bound(arr, mid + 1,
                       high, X);
}

// Recursive implementation of
// upper_bound
int upper_bound(int arr[], int low,
                int high, int X)
{

    // Base Case
    if (low > high)
        return low;

    // Find the middle index
    int mid = low + (high - low) / 2;

    // If arr[mid] is less than
    // or equal to X search in
    // right subarray
    if (arr[mid] <= X) {
        return upper_bound(arr, mid + 1,
                           high, X);
    }

    // If arr[mid] is greater than X
    // then search in left subarray
    return upper_bound(arr, low,
                       mid - 1, X);
}

// Function to implement lower_bound
// and upper_bound of X
void printBound(int arr[], int N, int X)
{
    int idx;

    // If lower_bound doesn't exists
    if (lower_bound(arr, 0, N, X) == N) {
        printf("Lower bound doesn't exist");
    }
    else {

        // Find lower_bound
        idx = lower_bound(arr, 0, N, X);
        printf("Lower bound of %d "
               "is %d at index %d\n",
               X, arr[idx], idx);
    }

    // If upper_bound doesn't exists
    if (upper_bound(arr, 0, N, X) == N) {
        printf("Upper bound doesn't exist");
    }
    else {

        // Find upper_bound
        idx = upper_bound(arr, 0, N, X);
        printf("Upper bound of %d is"
               "% d at index % d\n ",
               X,
               arr[idx], idx);
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 4, 6, 10, 12, 18, 20 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Element whose lower bound and
    // upper bound to be found
    int X = 6;

    // Function Call
    printBound(arr, N, X);
    return 0;
}
```

**Output:** 

```
Lower bound of 6 is 6 at index  1
 Upper bound of 6 is 10 at index  2
```

**时间复杂度:** O(log <sub>2</sub> N)，其中 N 为数组中元素的个数。
**辅助空间:** O(1)。