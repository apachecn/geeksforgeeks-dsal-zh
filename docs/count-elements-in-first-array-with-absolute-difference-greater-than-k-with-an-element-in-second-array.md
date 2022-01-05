# 用第二个数组中的一个元素计数绝对差值大于 K 的第一个数组中的元素

> 原文:[https://www . geeksforgeeks . org/count-绝对差大于 k 的第一数组中的元素与第二数组中的元素/](https://www.geeksforgeeks.org/count-elements-in-first-array-with-absolute-difference-greater-than-k-with-an-element-in-second-array/)

给定两个**数组 arr1[]和 arr2[]** 以及一个**整数 K** ，我们的任务是找出第一个数组中的元素个数，对于元素 **x，在 arr1[]** 中，至少存在一个元素 **y，在 arr2[]** 中，x 和 y 的**绝对差**大于整数 **K** 。

**示例:**

> **输入:** arr1 = {3，1，4}，arr2 = {5，1，2}，K = 2
> **输出:** 2
> **说明:**
> 这样的元素是 1 和 4。
> 对于 1，arr2[]有 5，ABS(1–5)= 4，大于 2。
> 对于 4，arr2[]有 1，ABS(4–1)= 3，同样大于 2。
> 
> **输入:** arr1 = {1，2}，arr2 = {4，6}，K = 3
> **输出:** 2
> **说明:**
> 这样的元素是 1 和 2。
> 对于 1，arr2[]有 6，ABS(1–6)= 5，大于 3。
> 对于 2，arr2[]有 6，ABS(2–6)= 4，大于 3。

**天真方法:**对 arr1[]中的每个元素进行迭代，检查 arr2 中是否存在一个元素，使得它们的绝对差值大于 k 值

***时间复杂度:** **O(N * M)*** 其中 N 和 M 分别是数组 1 和 2 的大小。

**有效方法:**要优化上述方法，我们必须观察到，对于 arr1【】中的每个元素，我们只需要 arr 2【】中**最小和最大的元素来检查它是否遥远。对于 arr1 中的每个元素 x，如果最小或最大值与 x 的绝对差值大于 K，则该元素是远离的。**

下面是上述方法的实现:

## C++

```
// C++ program to count elements in first Array
// with absolute difference greater than K
// with an element in second Array

#include <bits/stdc++.h>
using namespace std;

// Function to count the such elements
void countDist(int arr1[], int n, int arr2[],
               int m, int k)
{
    // Store count of required elements in arr1
    int count = 0;

    // Initialise the smallest and the largest
    // value from the second array arr2[]
    int smallest = arr2[0];
    int largest = arr2[0];

    // Find the smallest and
    // the largest element in arr2
    for (int i = 0; i < m; i++) {
        smallest = max(smallest, arr2[i]);
        largest = min(largest, arr1[i]);
    }
    for (int i = 0; i < n; i++) {

        // Check if absolute difference of smallest
        // and arr1[i] or largest and arr1[i] is > K
        // then arr[i] is a required element
        if (abs(arr1[i] - smallest) > k
            || abs(arr1[i] - largest) > k)
            count++;
    }

    // Print the final result
    cout << count;
}

// Driver code
int main()
{
    int arr1[] = { 3, 1, 4 };
    int n = sizeof(arr1) / sizeof(arr1[0]);
    int arr2[] = { 5, 1, 2 };
    int m = sizeof(arr2) / sizeof(arr2[0]);
    int k = 2;

    countDist(arr1, n, arr2, m, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count elements in first Array
// with absolute difference greater than K
// with an element in second Array
class GFG{

// Function to count the such elements
static void countDist(int arr1[], int n,
                      int arr2[], int m,
                      int k)
{
    // Store count of required elements in arr1
    int count = 0;

    // Initialise the smallest and the largest
    // value from the second array arr2[]
    int smallest = arr2[0];
    int largest = arr2[0];

    // Find the smallest and
    // the largest element in arr2
    for(int i = 0; i < m; i++)
    {
       smallest = Math.max(smallest, arr2[i]);
       largest = Math.min(largest, arr1[i]);
    }
    for(int i = 0; i < n; i++)
    {

       // Check if absolute difference
       // of smallest and arr1[i] or
       // largest and arr1[i] is > K
       // then arr[i] is a required element
       if (Math.abs(arr1[i] - smallest) > k ||
           Math.abs(arr1[i] - largest) > k)
           count++;
    }

    // Print the final result
    System.out.print(count);
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 3, 1, 4 };
    int n = arr1.length;
    int arr2[] = { 5, 1, 2 };
    int m = arr2.length;
    int k = 2;

    countDist(arr1, n, arr2, m, k);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count elements in the first Array
# with an absolute difference greater than K
# with an element in the second Array

# Function to count the such elements
def countDist(arr1, n, arr2, m, k):

    # Store count of required elements in arr1
    count = 0

    # Initialise the smallest and the largest
    # value from the second array arr2[]
    smallest = arr2[0]
    largest = arr2[0]

    # Find the smallest and
    # the largest element in arr2
    for i in range(m):
        smallest = max(smallest, arr2[i])
        largest = min(largest, arr1[i])

    for i in range(n):

        # Check if absolute difference of smallest
        # and arr1[i] or largest and arr1[i] is > K
        # then arr[i] is a required element
        if (abs(arr1[i] - smallest) > k
            or abs(arr1[i] - largest) > k):
            count += 1

    # Print final result
    print(count)

# Driver code
if __name__ == '__main__':

    arr1= [ 3, 1, 4 ]
    n = len(arr1)
    arr2= [ 5, 1, 2 ]
    m = len(arr2)
    k = 2

    countDist(arr1, n, arr2, m, k)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count elements in first array
// with absolute difference greater than K
// with an element in second Array
using System;

class GFG{

// Function to count the such elements
static void countDist(int []arr1, int n,
                      int []arr2, int m,
                      int k)
{
    // Store count of required elements in arr1
    int count = 0;

    // Initialise the smallest and the largest
    // value from the second array arr2[]
    int smallest = arr2[0];
    int largest = arr2[0];

    // Find the smallest and
    // the largest element in arr2
    for(int i = 0; i < m; i++)
    {
       smallest = Math.Max(smallest, arr2[i]);
       largest = Math.Min(largest, arr1[i]);
    }
    for(int i = 0; i < n; i++)
    {

       // Check if absolute difference
       // of smallest and arr1[i] or
       // largest and arr1[i] is > K
       // then arr[i] is a required element
       if (Math.Abs(arr1[i] - smallest) > k ||
           Math.Abs(arr1[i] - largest) > k)
           count++;
    }

    // Print the readonly result
    Console.Write(count);
}

// Driver code
public static void Main(String[] args)
{
    int []arr1 = { 3, 1, 4 };
    int n = arr1.Length;
    int []arr2 = { 5, 1, 2 };
    int m = arr2.Length;
    int k = 2;

    countDist(arr1, n, arr2, m, k);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to count elements in
// first Array with absolute difference
// greater than K with an element in
// second Array   

// Function to count the such elements
function countDist(arr1, n, arr2, m, k)
{

    // Store count of required elements in arr1
    var count = 0;

    // Initialise the smallest and the largest
    // value from the second array arr2
    var smallest = arr2[0];
    var largest = arr2[0];

    // Find the smallest and
    // the largest element in arr2
    for(i = 0; i < m; i++)
    {
        smallest = Math.max(smallest, arr2[i]);
        largest = Math.min(largest, arr1[i]);
    }
    for(i = 0; i < n; i++)
    {

        // Check if absolute difference
        // of smallest and arr1[i] or
        // largest and arr1[i] is > K
        // then arr[i] is a required element
        if (Math.abs(arr1[i] - smallest) > k ||
            Math.abs(arr1[i] - largest) > k)
            count++;
    }

    // Print the final result
    document.write(count);
}

// Driver code
var arr1 = [ 3, 1, 4 ];
var n = arr1.length;
var arr2 = [ 5, 1, 2 ];
var m = arr2.length;
var k = 2;

countDist(arr1, n, arr2, m, k);

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N + M)，其中 N 和 M 是给定数组的大小。
**辅助空间:** O(1)。