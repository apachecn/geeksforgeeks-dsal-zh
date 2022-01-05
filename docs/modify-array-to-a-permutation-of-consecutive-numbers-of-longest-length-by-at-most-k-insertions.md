# 通过最多 K 次插入将数组修改为最长的连续数字的排列

> 原文:[https://www . geeksforgeeks . org/modify-array-to-a-置换-一个最长长度为 k 的连续插入数/](https://www.geeksforgeeks.org/modify-array-to-a-permutation-of-consecutive-numbers-of-longest-length-by-at-most-k-insertions/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是通过最多附加 **K** 个元素来找到[数组](https://www.geeksforgeeks.org/array-data-structure/)的最大长度，使得数组成为从 **1** 开始的连续数字的排列。一旦添加了 **K** 元素，就可以插入两个或多个数组元素的和。

***注意:**元素可以由数组中最初存在的元素或附加元素的总和构成。但是，作为数组中两个或更多元素的总和添加的元素不能用于生成其他元素。*

**示例:**

> **输入:** N = 3，K = 1，arr[] = {1，2，4}
> **输出:** 8
> **解释:**
> 原始数组元素= {1，2，4}
> 使用这些元素可以得到的数组元素有{3，5，6，7}。
> 在数组中插入 8。
> 现在，从 9 到 15 开始的所有数字都可以追加到数组中。
> 因此，数组成为 15 个数字的连续序列。
> 
> **输入:** N = 5，K=4，arr[N] = {1，3，10，3，1 }
> T3】输出: 223

**方法:**思路是[将](https://www.geeksforgeeks.org/quick-sort/)[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**按升序排序，然后利用这样一个事实:如果[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**元素之和为**之和**，则可以形成从 **1** 到**之和**的所有元素，如果不是，则需要将**之和+1** 元素插入按照以下步骤解决问题:

*   [排序](https://www.geeksforgeeks.org/quick-sort/)把[阵](https://www.geeksforgeeks.org/array-data-structure/)T4【arr】。
*   将变量**索引**初始化为 **0** ，将[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和 **x** 中元素的索引维护为 **0** 存储答案。
*   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/) 直到**指数**小于 **N** ，执行以下步骤:
    *   如果 **arr【指数】**大于 **x** ，如果 **K** 等于 **0** ，则[破](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   否则将 **x** 的值增加 **x** ，将 **k** 的值减去 **1。**
    *   否则，将 **arr【指数】**的值加到 **x** 的值上，并将**指数**的值增加 **1。**
*   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/) 直到 **K** 不等于 **0** ，执行以下步骤:
    *   将 **x** 的值增加 **x** ，将 **k** 的值减去 **1** 。
*   执行上述步骤后，打印 **x-1** 的值作为答案。

下面是上述方法的实现。

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length
// possible
void findMaximumLength(int n, int k, int arr[])
{
    // Sort the array
    sort(arr, arr + n);

    // Initializing the variables
    int x = 1;
    int index = 0;

    // Iterate over the range
    while (index < n) {
        if (arr[index] > x) {

            // If k is 0, then no
            // element can be inserted
            if (k == 0)
                break;

            // Insert the element
            x = x + x;
            k--;
        }
        else {
            x += arr[index++];
        }
    }

    // Insert the remaining
    // possible elements
    while (k != 0) {
        x = x + x;
        k--;
    }

    // Print the answer
    cout << x - 1 << endl;
}

// Driver Code
int main()
{
    int n = 5, k = 4;
    int arr[n] = { 1, 3, 10, 3, 1 };

    findMaximumLength(n, k, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;
import java.util.Arrays;
class GFG
{

    // Function to find the maximum length
    // possible
    static void findMaximumLength(int n, int k, int arr[])
    {

        // Sort the array
        Arrays.sort(arr);

        // Initializing the variables
        int x = 1;
        int index = 0;

        // Iterate over the range
        while (index < n) {
            if (arr[index] > x) {

                // If k is 0, then no
                // element can be inserted
                if (k == 0)
                    break;

                // Insert the element
                x = x + x;
                k--;
            }
            else {
                x += arr[index++];
            }
        }

        // Insert the remaining
        // possible elements
        while (k != 0) {
            x = x + x;
            k--;
        }

        // Print the answer
        System.out.println(x - 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5, k = 4;
        int arr[] = { 1, 3, 10, 3, 1 };

        findMaximumLength(n, k, arr);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the maximum length
# possible
def findMaximumLength(n, k, arr):

    # Sort the array
    arr.sort();

    # Initializing the variables
    x = 1;
    index = 0;

    # Iterate over the range
    while (index < n):
        if (arr[index] > x):

            # If k is 0, then no
            # element can be inserted
            if (k == 0):
                break;

            # Insert the element
            x = x + x;
            k-=1;

        else:
            x += arr[index];
            index += 1;

    # Insert the remaining
    # possible elements
    while (k != 0):
        x = x + x;
        k -= 1;

    # Print answer
    print(x - 1);

# Driver Code
if __name__ == '__main__':
    n = 5; k = 4;
    arr = [ 1, 3, 10, 3, 1 ];

    findMaximumLength(n, k, arr);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum length
// possible
static void findMaximumLength(int n, int k, int []arr)
{

    // Sort the array
    Array.Sort(arr);

    // Initializing the variables
    int x = 1;
    int index = 0;

    // Iterate over the range
    while (index < n)
    {
        if (arr[index] > x)
        {

            // If k is 0, then no
            // element can be inserted
            if (k == 0)
                break;

            // Insert the element
            x = x + x;
            k--;
        }
        else
        {
            x += arr[index++];
        }
    }

    // Insert the remaining
    // possible elements
    while (k != 0)
    {
        x = x + x;
        k--;
    }

    // Print the answer
    Console.Write(x - 1);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5, k = 4;
    int []arr = { 1, 3, 10, 3, 1 };

    findMaximumLength(n, k, arr);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum length
// possible
function findMaximumLength(n, k, arr) {
  // Sort the array
  arr.sort((a, b) => a - b);

  // Initializing the variables
  let x = 1;
  let index = 0;

  // Iterate over the range
  while (index < n) {
    if (arr[index] > x) {
      // If k is 0, then no
      // element can be inserted
      if (k == 0) break;

      // Insert the element
      x = x + x;
      k--;
    } else {
      x += arr[index++];
    }
  }

  // Insert the remaining
  // possible elements
  while (k != 0) {
    x = x + x;
    k--;
  }

  // Print the answer
  document.write(x - 1);
}

// Driver Code
let n = 5,
  k = 4;
let arr = [1, 3, 10, 3, 1];

findMaximumLength(n, k, arr);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
223
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*