# 滑动窗口最大值:设置 2

> 原文:[https://www.geeksforgeeks.org/sliding-window-maximum-set-2/](https://www.geeksforgeeks.org/sliding-window-maximum-set-2/)

**设置 1:** [滑动窗口最大值(k 大小所有子阵列的最大值)](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)。
给定一个大小为 **N** 的数组 **arr** 和一个整数 **K** ，任务是为每个大小为 **K** 的相邻子数组找到最大值。

**示例:**

> **输入:** arr[] = {1，2，3，1，4，5，2，3，6}，K = 3
> **输出:** 3 3 4 5 5 5 6
> 所有大小为 K 的相邻子阵列都是
> {1，2，3} = > 3
> {2，3，1} = > 3
> {3，1，4} = > 4
> {1，4，5} = >
> 
> **输入:** arr[] = {8，5，10，7，9，4，15，12，90，13}，K = 4
> **输出:** 10 10 10 15 15 90 90

**方法:**为了在较小的空间复杂度下解决这个问题，我们可以使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)。

*   第一个变量指针遍历子数组，找到给定大小的最大元素 **K**
*   第二个变量指针标记第一个变量指针的结束索引，即**(I+K–1)第一个索引**。
*   当第一个变量指针到达第二个变量指针的索引时，该子数组的最大值已经计算出来并将被打印出来。
*   重复该过程，直到第二个变量指针到达最后一个数组索引**(即 array _ size–1)**。

下面是上述方法的实现:

## C++

```
// C++ program to find the maximum for each
// and every contiguous subarray of size K

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum for each
// and every contiguous subarray of size k
void printKMax(int a[], int n, int k)
{
    // If k = 1, print all elements
    if (k == 1) {
        for (int i = 0; i < n; i += 1)
            cout << a[i] << " ";
        return;
    }

    // Using p and q as variable pointers
    // where p iterates through the subarray
    // and q marks end of the subarray.
    int p = 0,
        q = k - 1,
        t = p,
        max = a[k - 1];

    // Iterating through subarray.
    while (q <= n - 1) {

        // Finding max
        // from the subarray.
        if (a[p] > max)
            max = a[p];

        p += 1;

        // Printing max of subarray
        // and shifting pointers
        // to next index.
        if (q == p && p != n) {
            cout << max << " ";
            q++;
            p = ++t;

            if (q < n)
                max = a[q];
        }
    }
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 3, 4, 5,
                6, 7, 8, 9, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    int K = 3;

    printKMax(a, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum for each
// and every contiguous subarray of size K
import java.util.*;

class GFG{

// Function to find the maximum for each
// and every contiguous subarray of size k
static void printKMax(int a[], int n, int k)
{
    // If k = 1, print all elements
    if (k == 1) {
        for (int i = 0; i < n; i += 1)
            System.out.print(a[i]+ " ");
        return;
    }

    // Using p and q as variable pointers
    // where p iterates through the subarray
    // and q marks end of the subarray.
    int p = 0,
        q = k - 1,
        t = p,
        max = a[k - 1];

    // Iterating through subarray.
    while (q <= n - 1) {

        // Finding max
        // from the subarray.
        if (a[p] > max)
            max = a[p];

        p += 1;

        // Printing max of subarray
        // and shifting pointers
        // to next index.
        if (q == p && p != n) {
            System.out.print(max+ " ");
            q++;
            p = ++t;

            if (q < n)
                max = a[q];
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 1, 2, 3, 4, 5,
                6, 7, 8, 9, 10 };
    int n = a.length;
    int K = 3;

    printKMax(a, n, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the maximum for each
# and every contiguous subarray of size K

# Function to find the maximum for each
# and every contiguous subarray of size k
def printKMax(a, n, k):

    # If k = 1, prall elements
    if (k == 1):
        for i in range(n):
            print(a[i], end=" ");
        return;

    # Using p and q as variable pointers
    # where p iterates through the subarray
    # and q marks end of the subarray.
    p = 0;
    q = k - 1;
    t = p;
    max = a[k - 1];

    # Iterating through subarray.
    while (q <= n - 1):

        # Finding max
        # from the subarray.
        if (a[p] > max):
            max = a[p];
        p += 1;

        # Printing max of subarray
        # and shifting pointers
        # to next index.
        if (q == p and p != n):
            print(max, end=" ");
            q += 1;
            p = t + 1;
            t = p;

            if (q < n):
                max = a[q];

# Driver Code
if __name__ == '__main__':
    a = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
    n = len(a);
    K = 3;

    printKMax(a, n, K);

# This code is contributed by Princi Singh
```

## C#

```
// C# program to find the maximum for each
// and every contiguous subarray of size K
using System;

class GFG{

// Function to find the maximum for each
// and every contiguous subarray of size k
static void printKMax(int []a, int n, int k)
{
    // If k = 1, print all elements
    if (k == 1) {
        for (int i = 0; i < n; i += 1)
            Console.Write(a[i]+ " ");
        return;
    }

    // Using p and q as variable pointers
    // where p iterates through the subarray
    // and q marks end of the subarray.
    int p = 0,
        q = k - 1,
        t = p,
        max = a[k - 1];

    // Iterating through subarray.
    while (q <= n - 1) {

        // Finding max
        // from the subarray.
        if (a[p] > max)
            max = a[p];

        p += 1;

        // Printing max of subarray
        // and shifting pointers
        // to next index.
        if (q == p && p != n) {
            Console.Write(max+ " ");
            q++;
            p = ++t;

            if (q < n)
                max = a[q];
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 1, 2, 3, 4, 5,
                6, 7, 8, 9, 10 };
    int n = a.Length;
    int K = 3;

    printKMax(a, n, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find the maximum for each
// and every contiguous subarray of size K

// Function to find the maximum for each
// and every contiguous subarray of size k
function printKMax(a, n, k)
{
    // If k = 1, print all elements
    if (k == 1) {
        for (let i = 0; i < n; i += 1)
            document.write(a[i] + " ");
        return;
    }

    // Using p and q as variable pointers
    // where p iterates through the subarray
    // and q marks end of the subarray.
    let p = 0, q = k - 1, t = p, max = a[k - 1];

    // Iterating through subarray.
    while (q <= n - 1) {

        // Finding max
        // from the subarray.
        if (a[p] > max)
            max = a[p];

        p += 1;

        // Printing max of subarray
        // and shifting pointers
        // to next index.
        if (q == p && p != n) {
            document.write(max + " ");
            q++;
            p = ++t;

            if (q < n)
                max = a[q];
        }
    }
}

// Driver Code

let a = [ 1, 2, 3, 4, 5,
            6, 7, 8, 9, 10 ];
let n = a.length
let K = 3;

printKMax(a, n, K);
</script>
```

**Output**

```
3 4 5 6 7 8 9 10 
```

**时间复杂度:O(N*k)**
**辅助空间复杂度:O(1)**

**<u>方法 2:</u>** 使用动态规划:

*   首先，将整个数组分成 k 个元素的块，使得每个块包含数组的 k 个元素(不总是针对最后一个块)。
*   维护两个 dp 数组，即左数组和右数组。
*   **left[i]** 是当前块(存在当前元素的块)中当前元素(包括当前元素)左侧所有元素的最大值。
*   类似地， **right[i]** 是当前块(存在当前元素的块)中当前元素(包括当前元素)右侧所有元素的最大值。
*   最后，在计算任意长度为 k 的子阵中的最大元素时，我们计算右[l]和左[r]
    的最大值，其中 **l =当前子阵的起始索引，r =当前子阵的结束索引**

下面是上述方法的实现，

## C++

```
// C++ program to find the maximum for each
// and every contiguous subarray of size K

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum for each
// and every contiguous subarray of size k
void printKMax(int a[], int n, int k)
{
    // If k = 1, print all elements
    if (k == 1) {
        for (int i = 0; i < n; i += 1)
            cout << a[i] << " ";
        return;
    }

      //left[i] stores the maximum value to left of i in the current block
      //right[i] stores the maximum value to the right of i in the current block
    int left[n],right[n];

      for(int i=0;i<n;i++){
          //if the element is starting element of that block
        if(i%k == 0) left[i] = a[i];
          else left[i] = max(left[i-1],a[i]);

          //if the element is ending element of that block
          if((n-i)%k == 0 || i==0) right[n-1-i] = a[n-1-i];
          else right[n-1-i] = max(right[n-i],a[n-1-i]);
    }

      for(int i=0,j=k-1; j<n; i++,j++)
         cout << max(left[j],right[i]) << ' ';
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 3, 4, 5,
                6, 7, 8, 9, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    int K = 3;

    printKMax(a, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum for each
// and every contiguous subarray of size K
import java.util.*;

class GFG
{

  // Function to find the maximum for each
  // and every contiguous subarray of size k
  static void printKMax(int a[], int n, int k)
  {

    // If k = 1, print all elements
    if (k == 1) {
      for (int i = 0; i < n; i += 1)
        System.out.print(a[i] + " ");
      return;
    }

    // left[i] stores the maximum value to left of i in the current block
    // right[i] stores the maximum value to the right of i in the current block
    int left[] = new int[n];
    int right[] = new int[n];

    for (int i = 0; i < n; i++)
    {

      // if the element is starting element of that block
      if (i % k == 0)
        left[i] = a[i];
      else
        left[i] = Math.max(left[i - 1], a[i]);

      // if the element is ending element of that block
      if ((n - i) % k == 0 || i == 0)
        right[n - 1 - i] = a[n - 1 - i];
      else
        right[n - 1 - i] = Math.max(right[n - i], a[n - 1 - i]);
    }

    for (int i = 0, j = k - 1; j < n; i++, j++)
      System.out.print(Math.max(left[j], right[i]) + " ");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int a[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int n = a.length;
    int K = 3;

    printKMax(a, n, K);

  }
}

// This code is contributed by gauravrajput1
```

## C#

```
// C# program to find the maximum for each
// and every contiguous subarray of size K
using System;

class GFG
{

  // Function to find the maximum for each
  // and every contiguous subarray of size k
  static void printKMax(int []a, int n, int k)
  {

    // If k = 1, print all elements
    if (k == 1) {
      for (int i = 0; i < n; i += 1)
        Console.Write(a[i] + " ");
      return;
    }

    // left[i] stores the maximum value to left of i in the current block
    // right[i] stores the maximum value to the right of i in the current block
    int []left = new int[n];
    int []right = new int[n];

    for (int i = 0; i < n; i++)
    {

      // if the element is starting element of that block
      if (i % k == 0)
        left[i] = a[i];
      else
        left[i] = Math.Max(left[i - 1], a[i]);

      // if the element is ending element of that block
      if ((n - i) % k == 0 || i == 0)
        right[n - 1 - i] = a[n - 1 - i];
      else
        right[n - 1 - i] = Math.Max(right[n - i], a[n - 1 - i]);
    }

    for (int i = 0, j = k - 1; j < n; i++, j++)
      Console.Write(Math.Max(left[j], right[i]) + " ");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []a = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int n = a.Length;
    int K = 3;

    printKMax(a, n, K);

  }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum for each
// and every contiguous subarray of size K
// Function to find the maximum for each
// and every contiguous subarray of size k
function printKMax(a, n, k)
  {

    // If k = 1, print all elements
    if (k == 1) {
      for (var i = 0; i < n; i += 1)
        document.write(a[i] + " ");
      return;
    }

    // left[i] stores the maximum value to left of i in the current block
    // right[i] stores the maximum value to the right of i in the current block
    var left = [n];
    var right = [n];

    for (var i = 0; i < n; i++)
    {

      // if the element is starting element of that block
      if (i % k == 0)
        left[i] = a[i];
      else
        left[i] = Math.max(left[i - 1], a[i]);

      // if the element is ending element of that block
      if ((n - i) % k == 0 || i == 0)
        right[n - 1 - i] = a[n - 1 - i];
      else
        right[n - 1 - i] = Math.max(right[n - i], a[n - 1 - i]);
    }

    for (var i = 0, j = k - 1; j < n; i++, j++)
      document.write(Math.max(left[j], right[i]) + " ");
  }

  // Driver Code
    var a = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
    var n = a.length;
    var K = 3;

    printKMax(a, n, K);

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
3 4 5 6 7 8 9 10 
```

**时间复杂度:O(n)**
**辅助空间:O(n)**