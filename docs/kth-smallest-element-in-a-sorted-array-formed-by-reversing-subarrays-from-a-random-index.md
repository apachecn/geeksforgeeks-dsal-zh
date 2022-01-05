# 通过从随机索引反转子阵列形成的排序数组中的第 k 个最小元素

> 原文:[https://www . geeksforgeeks . org/kth-排序数组中的最小元素-通过从随机索引中反转子数组形成/](https://www.geeksforgeeks.org/kth-smallest-element-in-a-sorted-array-formed-by-reversing-subarrays-from-a-random-index/)

给定一个大小为 **N** 的排序后的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **K** ，任务是找到数组中第 K 个<sup>最小元素。给定的数组是通过将子数组 **{arr[0]，arr[R]}** 和 **{arr[R + 1]，arr[N–1]}**在某个随机索引 **R.** 处反转得到的，如果数组中没有**键**，打印 **-1** 。</sup>

**示例:**

> **输入:** arr[] = { 4，3，2，1，8，7，6，5 }，K = 2
> **输出:** 2
> **说明:**数组 arr[]的排序形式为{ 1，2，3，4，5，6，7，8 }。因此，arr[]数组中的第二个最小元素是 2。
> 
> **输入:** arr[] = { 10，8，6，5，2，1，13，12 }，K = 3
> **输出:** 5

**天真方法:**解决问题最简单的方法是[按照递增顺序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对给定数组**arr【】**排序，并打印数组中第**K**T8 个最小元素。

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*

**上述解决方案的替代方法:**我们可以在不使用任何排序技术的情况下对数组进行排序，这肯定会降低时间复杂度。我们可以使用二分搜索法找到阵列中的枢轴点 **P** (旋转围绕该点发生)，并使用 C++中的 **std::reverse()** 函数反转两个子阵列**【0，P+1】**和**【P+1，N】**。

**反转子阵:**找到枢轴点 **P** 后，如下找到两个子阵的反转即可:

**std::reverse(arr，arr+P+1)；**

**std::reverse(arr + P + 1，arr+N)；**

这样我们就得到排序后的数组，我们可以将第 **Kth** 个最小元素打印为**arr【K-1】**。

## C++

```
// C++ program for the above approach.
#include <bits/stdc++.h>
using namespace std;

/* Function to get pivot. For array 4, 3, 2, 1, 6, 5
   it returns 3 (index of 1) */
int findPivot(int arr[], int low, int high)
{
    // base cases
    if (high < low)
        return -1;
    if (high == low)
        return low;

    int mid = (low + high) / 2; /*low + (high - low)/2;*/
    if (mid < high && arr[mid] < arr[mid + 1])
        return mid;

    if (mid > low && arr[mid] > arr[mid - 1])
        return (mid - 1);

    if (arr[low] <= arr[mid])
        return findPivot(arr, low, mid - 1);

    return findPivot(arr, mid + 1, high);
}

// Driver Code
int main()
{

    // Given Input
    int arr[] = { 10, 8, 6, 5, 2, 1, 13, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    // Function Call
    int P = findPivot(arr, 0, N - 1);

    // reversing first subarray
    reverse(arr, arr + P + 1);

    // reversing second subarray
    reverse(arr + P + 1, arr + N);
    // printing output
    cout << arr[K - 1];
    return 0;
}

// This code is contributed by Pranjay Vats
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach.
import java.util.*;

class GFG{

// Function to get pivot. For array 4, 3, 2, 1, 6, 5
// it returns 3 (index of 1)
static int findPivot(int arr[], int low, int high)
{

    // Base cases
    if (high < low)
        return -1;
    if (high == low)
        return low;

    int mid = (low + high) / 2; /*low + (high - low)/2;*/
    if (mid < high && arr[mid] < arr[mid + 1])
        return mid;

    if (mid > low && arr[mid] > arr[mid - 1])
        return (mid - 1);

    if (arr[low] <= arr[mid])
        return findPivot(arr, low, mid - 1);

    return findPivot(arr, mid + 1, high);
}

static void reverse(int str[], int start, int end)
{

    // Temporary variable to store character
    int temp;

    while (start <= end)
    {

        // Swapping the first and last character
        temp = str[start];
        str[start] = str[end];
        str[end] = temp;
        start++;
        end--;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int arr[] = { 10, 8, 6, 5, 2, 1, 13, 12 };
    int N = arr.length;
    int K = 3;

    // Function Call
    int P = findPivot(arr, 0, N - 1);

    // Reversing first subarray
    reverse(arr, 0, P);

    // Reversing second subarray
    reverse(arr, P, N - 1);

    // Printing output
    System.out.print(arr[K - 1]);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach.

# Function to get pivot. For array 4, 3, 2, 1, 6, 5
# it returns 3 (index of 1)
def findPivot(arr, low, high):

    # Base cases
    if (high < low):
        return -1
    if (high == low):
        return low

    mid = int((low + high) / 2) #low + (high - low)/2;
    if (mid < high and arr[mid] < arr[mid + 1]):
        return mid

    if (mid > low and arr[mid] > arr[mid - 1]):
        return (mid - 1)

    if (arr[low] <= arr[mid]):
        return findPivot(arr, low, mid - 1)

    return findPivot(arr, mid + 1, high)

def reverse(Str, start, end):
    while (start <= end):
        # Swapping the first and last character
        temp = Str[start]
        Str[start] = Str[end]
        Str[end] = temp
        start+=1
        end-=1

# Given Input
arr = [ 10, 8, 6, 5, 2, 1, 13, 12 ]
N = len(arr)
K = 3

# Function Call
P = findPivot(arr, 0, N - 1)

# Reversing first subarray
reverse(arr, 0, P)

# Reversing second subarray
reverse(arr, P, N - 1)

# Printing output
print(arr[K - 1])

# This code is contributed by decode2207.
```

## C#

```
// C# program for the above approach.
using System;
class GFG {

    // Function to get pivot. For array 4, 3, 2, 1, 6, 5
    // it returns 3 (index of 1)
    static int findPivot(int[] arr, int low, int high)
    {

        // Base cases
        if (high < low)
            return -1;
        if (high == low)
            return low;

        int mid = (low + high) / 2; /*low + (high - low)/2;*/
        if (mid < high && arr[mid] < arr[mid + 1])
            return mid;

        if (mid > low && arr[mid] > arr[mid - 1])
            return (mid - 1);

        if (arr[low] <= arr[mid])
            return findPivot(arr, low, mid - 1);

        return findPivot(arr, mid + 1, high);
    }

    static void reverse(int[] str, int start, int end)
    {

        // Temporary variable to store character
        int temp;

        while (start <= end)
        {

            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }

  static void Main() {
    // Given Input
    int[] arr = { 10, 8, 6, 5, 2, 1, 13, 12 };
    int N = arr.Length;
    int K = 3;

    // Function Call
    int P = findPivot(arr, 0, N - 1);

    // Reversing first subarray
    reverse(arr, 0, P);

    // Reversing second subarray
    reverse(arr, P, N - 1);

    // Printing output
    Console.Write(arr[K - 1]);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach.

    /* Function to get pivot. For array 4, 3, 2, 1, 6, 5
   it returns 3 (index of 1) */
  function findPivot(arr, low, high)
  {

      // base cases
      if (high < low)
          return -1;
      if (high == low)
          return low;

      let mid = parseInt((low + high) / 2, 10); /*low + (high - low)/2;*/
      if (mid < high && arr[mid] < arr[mid + 1])
          return mid;

      if (mid > low && arr[mid] > arr[mid - 1])
          return (mid - 1);

      if (arr[low] <= arr[mid])
          return findPivot(arr, low, mid - 1);

      return findPivot(arr, mid + 1, high);
  }

  function reverse(i, j, arr)
  {
    let y = j - 1;
      for(let x = i; x < j; x++)
    {
        arr[x] = arr[y];
        y--;
    }
  }

  // Given Input
  let arr = [ 10, 8, 6, 5, 2, 1, 13, 12 ];
  let N = arr.length;
  let K = 3;

  // Function Call
  let P = findPivot(arr, 0, N - 1);

  // reversing first subarray
  reverse(0, P + 1, arr);

  // reversing second subarray
  reverse(P + 1, N, arr);

  // printing output
  document.write(arr[K - 1]);

  // This code is contributed by divyeshrabadiya07.
</script>
```

**Output**

```
5
```

***时间复杂度:** O(N)*

***辅助空间:** O(1)*

**高效方法:**最优思想是基于这样的观察，即 **Rth** 元素是最小的元素，因为范围**【1】****R】**中的元素是相反的。现在，如果随机索引为 **R** ，则表示子数组**【1，R】**和**【R+1，N】**是按[降序排列的](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。因此，任务简化为寻找 **R** 的值，该值可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)获得。最后，打印**K**T22【第 T23】个最小元素。

按照以下步骤解决问题:

*   将 **l** 初始化为 **1** ，将 **h** 初始化为 **N** ，存储[二分搜索法](https://www.geeksforgeeks.org/binary-search/)搜索空间的边界元素索引。
*   [循环同时](https://www.geeksforgeeks.org/loops-in-python/)的值 **l+1 < h**
    *   将中间元素存储在变量中，**中间**为 **(l+h)/2** 。
    *   如果 **arr[l] ≥ arr[mid]。**如果是真的，那么通过更新 **l** 到**中间**来检查**中间**右侧。
    *   否则，将 **r** 更新为**中**。
*   现在找到 **R** 后，如果 **K ≤ R** ，那么答案就是**arr【R-K+1】。**否则，**arr【N-(K-R)+1】**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Kth element in a
// sorted and rotated array at random point
int findkthElement(vector<int> arr, int n, int K)
{

    // Set the boundaries for binary search
    int l = 0;
    int h = n - 1, r;

    // Apply binary search to find R
    while (l + 1 < h)
    {

        // Initialize the middle element
        int mid = (l + h) / 2;

        // Check in the right side of mid
        if (arr[l] >= arr[mid])
            l = mid;

        // Else check in the left side
        else
            h = mid;
    }

    // Random point either l or h
    if (arr[l] < arr[h])
        r = l;
    else
        r = h;

    // Return the kth smallest element
    if (K <= r + 1)
        return arr[r + 1 - K];
    else
        return arr[n - (K - (r + 1))];
}

// Driver Code
int main()
{

    // Given Input
    vector<int> arr = { 10, 8, 6, 5, 2, 1, 13, 12 };
    int n = arr.size();
    int K = 3;

    // Function Call
    cout << findkthElement(arr, n, K);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the Kth element in a
// sorted and rotated array at random point
public static int findkthElement(int arr[], int n, int K)
{

    // Set the boundaries for binary search
    int l = 0;
    int h = n - 1, r;

    // Apply binary search to find R
    while (l + 1 < h)
    {

        // Initialize the middle element
        int mid = (l + h) / 2;

        // Check in the right side of mid
        if (arr[l] >= arr[mid])
            l = mid;

        // Else check in the left side
        else
            h = mid;
    }

    // Random point either l or h
    if (arr[l] < arr[h])
        r = l;
    else
        r = h;

    // Return the kth smallest element
    if (K <= r + 1)
        return arr[r + 1 - K];
    else
        return arr[n - (K - (r + 1))];
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int []arr = { 10, 8, 6, 5, 2, 1, 13, 12 };
    int n = arr.length;
    int K = 3;

    // Function Call
    System.out.println(findkthElement(arr, n, K));
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the Kth element in a
# sorted and rotated array at random point
def findkthElement(arr, n, K):

      # Set the boundaries for binary search
    l = 0
    h = n-1

    # Apply binary search to find R
    while l+1 < h:

          # Initialize the middle element
        mid = (l+h)//2

        # Check in the right side of mid
        if arr[l] >= arr[mid]:
            l = mid

        # Else check in the left side
        else:
            h = mid

    # Random point either l or h
    if arr[l] < arr[h]:
        r = l
    else:
        r = h

    # Return the kth smallest element
    if K <= r+1:
        return arr[r+1-K]
    else:
        return arr[n-(K-(r+1))]

# Driver Code
if __name__ == "__main__":

      # Given Input
    arr = [10, 8, 6, 5, 2, 1, 13, 12]
    n = len(arr)
    K = 3

    # Function Call
    print(findkthElement(arr, n, K) )
```

## C#

```
using System.IO;
using System;

class GFG {

    // Function to find the Kth element in a
    // sorted and rotated array at random point
    public static int findkthElement(int[] arr, int n,
                                     int K)
    {

        // Set the boundaries for binary search
        int l = 0;
        int h = n - 1, r;

        // Apply binary search to find R
        while (l + 1 < h) {

            // Initialize the middle element
            int mid = (l + h) / 2;

            // Check in the right side of mid
            if (arr[l] >= arr[mid])
                l = mid;

            // Else check in the left side
            else
                h = mid;
        }

        // Random point either l or h
        if (arr[l] < arr[h])
            r = l;
        else
            r = h;

        // Return the kth smallest element
        if (K <= r + 1)
            return arr[r + 1 - K];
        else
            return arr[n - (K - (r + 1))];
    }

    static void Main()
    {
        // Given Input
        int[] arr = { 10, 8, 6, 5, 2, 1, 13, 12 };
        int n = arr.Length;
        int K = 3;

        // Function Call
        Console.WriteLine(findkthElement(arr, n, K));
    }
}

// This code is contributed by abhinavjain194.
```

## java 描述语言

```
<script>

      // Function to find the Kth element in a
      // sorted and rotated array at random point
      function findkthElement(arr, n, K) {
        // Set the boundaries for binary search
        var l = 0;
        var h = n - 1,
          r;

        // Apply binary search to find R
        while (l + 1 < h) {
          // Initialize the middle element
          var mid = parseInt((l + h) / 2);

          // Check in the right side of mid
          if (arr[l] >= arr[mid]) l = mid;
          // Else check in the left side
          else h = mid;
        }

        // Random point either l or h
        if (arr[l] < arr[h]) r = l;
        else r = h;

        // Return the kth smallest element
        if (K <= r + 1) return arr[r + 1 - K];
        else return arr[n - (K - (r + 1))];
      }

      // Given Input
      var arr = [10, 8, 6, 5, 2, 1, 13, 12];
      var n = arr.length;
      var K = 3;

      // Function Call
      document.write(findkthElement(arr, n, K));

</script>
```

**Output**

```
5
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*