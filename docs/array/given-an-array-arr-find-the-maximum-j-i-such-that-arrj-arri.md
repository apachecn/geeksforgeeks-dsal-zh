# 给定数组`arr[]`，找到最大`j – i`，使得`arr[j] > arr[i]`

> 原文： [https://www.geeksforgeeks.org/given-an-array-arr-find-the-maximum-j-i-such-that-arrj-arri/](https://www.geeksforgeeks.org/given-an-array-arr-find-the-maximum-j-i-such-that-arrj-arri/)

给定数组`arr[]`，找到最大`j – i`，使得`arr[j] > arr[i]`。

**示例**：

```
  Input: {34, 8, 10, 3, 2, 80, 30, 33, 1}
  Output: 6  (j = 7, i = 1)

  Input: {9, 2, 3, 4, 5, 6, 7, 8, 18, 0}
  Output: 8 ( j = 8, i = 0)

  Input:  {1, 2, 3, 4, 5, 6}
  Output: 5  (j = 5, i = 0)

  Input:  {6, 5, 4, 3, 2, 1}
  Output: -1 
```



**方法 1（简单但效率低下）**：

运行两个循环。 在外循环中，从左开始一个接一个地选择元素。 在内部循环中，将拾取的元素与从右侧开始的元素进行比较。 当您看到一个大于选取的元素的元素时，请停止内部循环，并保持当前的最大`j-i`更新。

## C++ 

```cpp

#include <bits/stdc++.h> 

using namespace std; 
/* For a given array arr[], returns the maximum j – i such that 
    arr[j] > arr[i] */
int maxIndexDiff(int arr[], int n) 
{ 
    int maxDiff = -1; 
    int i, j; 

    for (i = 0; i < n; ++i) 
    { 
        for (j = n-1; j > i; --j) 
        { 
            if(arr[j] > arr[i] && maxDiff < (j - i)) 
                maxDiff = j - i; 
        } 
    } 

    return maxDiff; 
} 

int main() 
{ 
    int arr[] = {9, 2, 3, 4, 5, 6, 7, 8, 18, 0}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int maxDiff = maxIndexDiff(arr, n); 
    cout<< "\n" << maxDiff; 
    return 0; 
} 

// This code is contributed 
// by Akanksha Rai(Abby_akku) 

```

## C

```c
#include <stdio.h>
/* For a given array arr[], returns the maximum j – i such that
    arr[j] > arr[i] */
int maxIndexDiff(int arr[], int n)
{
    int maxDiff = -1;
    int i, j;
 
    for (i = 0; i < n; ++i) {
        for (j = n - 1; j > i; --j) {
            if (arr[j] > arr[i] && maxDiff < (j - i))
                maxDiff = j - i;
        }
    }
 
    return maxDiff;
}
 
int main()
{
    int arr[] = { 9, 2, 3, 4, 5, 6, 7, 8, 18, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int maxDiff = maxIndexDiff(arr, n);
    printf("\n %d", maxDiff);
    getchar();
    return 0;
}
Java
filter_none
edit
play_arrow

brightness_4
class FindMaximum {
    /* For a given array arr[], returns the maximum j-i such that
       arr[j] > arr[i] */
    int maxIndexDiff(int arr[], int n)
    {
        int maxDiff = -1;
        int i, j;
 
        for (i = 0; i < n; ++i) {
            for (j = n - 1; j > i; --j) {
                if (arr[j] > arr[i] && maxDiff < (j - i))
                    maxDiff = j - i;
            }
        }
 
        return maxDiff;
    }
 
    /* Driver program to test above functions */
    public static void main(String[] args)
    {
        FindMaximum max = new FindMaximum();
        int arr[] = { 9, 2, 3, 4, 5, 6, 7, 8, 18, 0 };
        int n = arr.length;
        int maxDiff = max.maxIndexDiff(arr, n);
        System.out.println(maxDiff);
    }
}
```

## Python3

```py
# Python3 program to find the maximum
# j – i such that arr[j] > arr[i]
  
# For a given array arr[], returns
# the maximum j – i such that
# arr[j] > arr[i] 
def maxIndexDiff(arr, n):
    maxDiff = -1
    for i in range(0, n):
        j = n - 1
        while(j > i):
            if arr[j] > arr[i] and maxDiff < (j - i):
                maxDiff = j - i;
            j -= 1
     
    return maxDiff
 
# driver code
arr = [9, 2, 3, 4, 5, 6, 7, 8, 18, 0]
n = len(arr)
maxDiff = maxIndexDiff(arr, n)
print(maxDiff)
 
# This article is contributed by Smitha Dinesh Semwal
```

## C#

```cs
// C# program to find the maximum
// j – i such that arr[j] > arr[i]
using System;
class GFG {
    // For a given array arr[], returns
    // the maximum j-i such that arr[j] > arr[i]
    static int maxIndexDiff(int[] arr, int n)
    {
        int maxDiff = -1;
        int i, j;
 
        for (i = 0; i < n; ++i) {
            for (j = n - 1; j > i; --j) {
                if (arr[j] > arr[i] && maxDiff < (j - i))
                    maxDiff = j - i;
            }
        }
 
        return maxDiff;
    }
 
    // Driver program
    public static void Main()
    {
 
        int[] arr = { 9, 2, 3, 4, 5, 6, 7, 8, 18, 0 };
        int n = arr.Length;
        int maxDiff = maxIndexDiff(arr, n);
        Console.Write(maxDiff);
    }
}
// This Code is Contributed by Sam007
```

## PHP

```php
<?php
// PHP program to find the maximum
// j – i such that arr[j] > arr[i]
 
// For a given array arr[], returns 
// the maximum j – i such that 
// arr[j] > arr[i] 
function maxIndexDiff($arr, $n)
{
    $maxDiff = -1;
     
    for ($i = 0; $i < $n; ++$i)
    {
        for ($j = $n - 1; $j > $i; --$j)
        {
            if($arr[$j] > $arr[$i] && 
               $maxDiff < ($j - $i))
                $maxDiff = $j - $i;
        }
    }
 
    return $maxDiff;
}
 
// Driver Code
$arr = array(9, 2, 3, 4, 5, 
             6, 7, 8, 18, 0);
$n = count($arr);
$maxDiff = maxIndexDiff($arr, $n);
echo $maxDiff ;
 
// This code is contributed by Sam007
?>
```

时间复杂度：O（n ^ 2）

方法 2：

改进蛮力算法并查找 BUD，即瓶颈，不必要和重复的作品。快速观察实际上表明，我们一直在寻找从数组末尾到当前索引的第一个最大元素。我们可以看到，我们试图一次又一次地为数组中的每个元素找到最大的元素。假设我们有一个数组，例如`[1, 5, 12, 4, 9]`，现在我们知道 9 是大于 1、5 和 4 的元素，但是为什么我们需要一次又一次地找到它。实际上，我们可以跟踪从数组结尾到开头的最大数量。这种方法将帮助我们更好地理解，并且即兴采访也很容易。

方法：

+   从末尾遍历数组，并跟踪当前索引右边的最大数字，包括自身。
+   现在我们有了一个单调的递减数组，并且我们知道可以使用二进制搜索找到最右边的较大元素的索引。
+   现在，我们将仅对数组中的每个元素使用二进制搜索，并存储索引的最大差异，就这样，我们就完成了。

## C++

```cpp
/* For a given array arr[], calculates the maximum j – i such that
    arr[j] > arr[i] */
#include <bits/stdc++.h>
using namespace std;
 
int main()
{
    vector<long long int> v{ 34, 8, 10, 3, 2, 80, 30, 33, 1 };
    int n = v.size();
    vector<long long int> maxFromEnd(n + 1, INT_MIN);
 
    // create an array maxfromEnd
    for (int i = v.size() - 1; i >= 0; i--) {
        maxFromEnd[i] = max(maxFromEnd[i + 1], v[i]);
    }
 
    int result = 0;
 
    for (int i = 0; i < v.size(); i++) {
        int low = i + 1, high = v.size() - 1, ans = i;
 
        while (low <= high) {
            int mid = (low + high) / 2;
 
            if (v[i] <= maxFromEnd[mid]) {
                // we store this as current answer and look
                // for further larger number to the right side
                ans = max(ans, mid);
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }
        // keeping a track of the
        // maximum difference in indices
        result = max(result, ans - i);
    }
    cout << result << endl;
}
```

## Java

```java
// Java program to implement
// the above approach
 
// For a given array arr[], 
// calculates the maximum j – i 
// such that arr[j] > arr[i] 
import java.util.*;
class GFG{
 
public static void main(String[] args)
{
  int []v = {34, 8, 10, 3, 2, 
             80, 30, 33, 1};
  int n = v.length;
  int []maxFromEnd = new int[n + 1];
  Arrays.fill(maxFromEnd, Integer.MIN_VALUE);
 
  // Create an array maxfromEnd
  for (int i = v.length - 1; i >= 0; i--) 
  {
    maxFromEnd[i] = Math.max(maxFromEnd[i + 1], 
                             v[i]);
  }
 
  int result = 0;
 
  for (int i = 0; i < v.length; i++) 
  {
    int low = i + 1, high = v.length - 1, 
        ans = i;
 
    while (low <= high) 
    {
      int mid = (low + high) / 2;
 
      if (v[i] <= maxFromEnd[mid]) 
      {
        // We store this as current 
        // answer and look for further 
        // larger number to the right side
        ans = Math.max(ans, mid);
        low = mid + 1;
      }
      else
      {
        high = mid - 1;
      }
    }
     
    // Keeping a track of the
    // maximum difference in indices
    result = Math.max(result, ans - i);
  }
  System.out.print(result + "\n");
}
}
 
// This code is contributed by shikhasingrajput
```

## C#

```cs
// C# program to implement
// the above approach
 
// For a given array []arr, 
// calculates the maximum j – i 
// such that arr[j] > arr[i] 
using System;
class GFG{
 
public static void Main(String[] args)
{
  int []v = {34, 8, 10, 3, 2, 
             80, 30, 33, 1};
  int n = v.Length;
  int []maxFromEnd = new int[n + 1];
   
  for (int i = 0; 
           i < maxFromEnd.Length; i++) 
    maxFromEnd[i] = int.MinValue;
 
  // Create an array maxfromEnd
  for (int i = v.Length - 1; 
           i >= 0; i--) 
  {
    maxFromEnd[i] = Math.Max(maxFromEnd[i + 1], 
                             v[i]);
  }
 
  int result = 0;
 
  for (int i = 0; i < v.Length; i++) 
  {
    int low = i + 1, 
        high = v.Length - 1, 
    ans = i;
 
    while (low <= high) 
    {
      int mid = (low + high) / 2;
 
      if (v[i] <= maxFromEnd[mid]) 
      {
        // We store this as current 
        // answer and look for further 
        // larger number to the right side
        ans = Math.Max(ans, mid);
        low = mid + 1;
      }
      else
      {
        high = mid - 1;
      }
    }
 
    // Keeping a track of the
    // maximum difference in indices
    result = Math.Max(result, ans - i);
  }
  Console.Write(result + "\n");
}
}
 
// This code is contributed by shikhasingrajput
```

输出：

```
6
```

时间复杂度：`O(N * log(N))`。

空间复杂度：`O(N)`。

方法 3 `O(nLgn)`：

在特别注意重复项之后，使用哈希和排序以小于二次复杂度的方式解决此问题。

方法：

+   遍历数组并将每个元素的索引存储在列表中（以处理重复项）。
+   对数组进行排序。
+   现在遍历数组，并跟踪i和j的最大差。
+   对于`j`，请考虑该元素可能的索引列表中的最后一个索引，而对于我，请考虑该列表中的第一个索引。 （因为索引是按升序附加的）。
+   不断更新最大差值，直到数组末尾。

## Python3

```py
# Python3 implementation of the above approach
n = 9
a = [34, 8, 10, 3, 2, 80, 30, 33, 1]
 
# To store the index of an element.
index = dict() 
for i in range(n):
    if a[i] in index:
 
        # append to list (for duplicates)
        index[a[i]].append(i)  
    else:
 
        # if first occurrence
        index[a[i]] = [i]   
 
# sort the input array
a.sort()     
maxDiff = 0
 
# Temporary variable to keep track of minimum i
temp = n     
for i in range(n):
    if temp > index[a[i]][0]:
        temp = index[a[i]][0]
    maxDiff = max(maxDiff, index[a[i]][-1]-temp)
 
print(maxDiff)
```

输出：

```
6
```

时间复杂度：`O(N * log(N))`

方法 4（有效）：

为了解决这个问题，我们需要获得`arr[]`的两个最佳索引：左索引`i`和右索引`j`。对于元素`arr[i]`，如果`arr[i]`左侧的元素小于`arr[i]`，则无需为左索引考虑`arr[i]`。类似地，如果`arr[j]`的右侧有一个更大的元素，那么对于正确的索引，我们不需要考虑这个`j`。因此，我们构造了两个辅助数组`LMin[]`和`RMax[]`，使得`LMin[i]`在包含`arr[i]`的`arr[i]`左侧保留最小的元素，而`RMax[j]`在`arr[i]`右侧保留最大的元素`arr[j]`包括`arr[j]`。构建完这两个辅助数组后，我们从左到右遍历这两个数组。在遍历`LMin[]`和`RMa[]`时，如果我们看到`LMin[i]`大于`RMax[j]`，则必须向前移动`LMin[]`（或执行`i++`），因为`LMin[i]`左侧的所有元素都是大于或等于`LMin[i]`。否则，我们必须继续前进`RMax[j]`，以寻找更大的`j – i`值。

感谢 celicom 为这种方法建议算法。

## C++

```cpp
#include <bits/stdc++.h>
using namespace std;
 
/* For a given array arr[],  
   returns the maximum j – i such that
   arr[j] > arr[i] */
int maxIndexDiff(int arr[], int n)
{
    int maxDiff;
    int i, j;
 
    int* LMin = new int[(sizeof(int) * n)];
    int* RMax = new int[(sizeof(int) * n)];
 
    /* Construct LMin[] such that 
    LMin[i] stores the minimum value 
    from (arr[0], arr[1], ... arr[i]) */
    LMin[0] = arr[0];
    for (i = 1; i < n; ++i)
        LMin[i] = min(arr[i], LMin[i - 1]);
 
    /* Construct RMax[] such that 
    RMax[j] stores the maximum value from 
    (arr[j], arr[j+1], ..arr[n-1]) */
    RMax[n - 1] = arr[n - 1];
    for (j = n - 2; j >= 0; --j)
        RMax[j] = max(arr[j], RMax[j + 1]);
 
    /* Traverse both arrays from left to right
    to find optimum j - i. This process is similar to 
    merge() of MergeSort */
    i = 0, j = 0, maxDiff = -1;
    while (j < n && i < n) {
        if (LMin[i] < RMax[j]) {
            maxDiff = max(maxDiff, j - i);
            j = j + 1;
        }
        else
            i = i + 1;
    }
 
    return maxDiff;
}
 
// Driver Code
int main()
{
    int arr[] = { 9, 2, 3, 4, 5,
                  6, 7, 8, 18, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int maxDiff = maxIndexDiff(arr, n);
    cout << maxDiff;
    return 0;
}
 
// This code is contributed by rathbhupendra
```

## C

```c
#include <stdio.h>
 
/* Utility Functions to get max and minimum of two integers */
int max(int x, int y)
{
    return x > y ? x : y;
}
 
int min(int x, int y)
{
    return x < y ? x : y;
}
 
/* For a given array arr[], returns the maximum j – i such that
    arr[j] > arr[i] */
int maxIndexDiff(int arr[], int n)
{
    int maxDiff;
    int i, j;
 
    int* LMin = (int*)malloc(sizeof(int) * n);
    int* RMax = (int*)malloc(sizeof(int) * n);
 
    /* Construct LMin[] such that LMin[i] stores the minimum value
       from (arr[0], arr[1], ... arr[i]) */
    LMin[0] = arr[0];
    for (i = 1; i < n; ++i)
        LMin[i] = min(arr[i], LMin[i - 1]);
 
    /* Construct RMax[] such that RMax[j] stores the maximum value
       from (arr[j], arr[j+1], ..arr[n-1]) */
    RMax[n - 1] = arr[n - 1];
    for (j = n - 2; j >= 0; --j)
        RMax[j] = max(arr[j], RMax[j + 1]);
 
    /* Traverse both arrays from left to right to find optimum j - i
        This process is similar to merge() of MergeSort */
    i = 0, j = 0, maxDiff = -1;
    while (j < n && i < n) {
        if (LMin[i] < RMax[j]) {
            maxDiff = max(maxDiff, j - i);
            j = j + 1;
        }
        else
            i = i + 1;
    }
 
    return maxDiff;
}
 
/* Driver program to test above functions */
int main()
{
    int arr[] = { 9, 2, 3, 4, 5, 6, 7, 8, 18, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int maxDiff = maxIndexDiff(arr, n);
    printf("\n %d", maxDiff);
    getchar();
    return 0;
}
```

## Java

```java
class FindMaximum {
    /* Utility Functions to get max and minimum of two integers */
    int max(int x, int y)
    {
        return x > y ? x : y;
    }
 
    int min(int x, int y)
    {
        return x < y ? x : y;
    }
 
    /* For a given array arr[], returns the maximum j-i such that
       arr[j] > arr[i] */
    int maxIndexDiff(int arr[], int n)
    {
        int maxDiff;
        int i, j;
 
        int RMax[] = new int[n];
        int LMin[] = new int[n];
 
        /* Construct LMin[] such that LMin[i] stores the minimum value
           from (arr[0], arr[1], ... arr[i]) */
        LMin[0] = arr[0];
        for (i = 1; i < n; ++i)
            LMin[i] = min(arr[i], LMin[i - 1]);
 
        /* Construct RMax[] such that RMax[j] stores the maximum value
           from (arr[j], arr[j+1], ..arr[n-1]) */
        RMax[n - 1] = arr[n - 1];
        for (j = n - 2; j >= 0; --j)
            RMax[j] = max(arr[j], RMax[j + 1]);
 
        /* Traverse both arrays from left to right to find optimum j - i
           This process is similar to merge() of MergeSort */
        i = 0;
        j = 0;
        maxDiff = -1;
        while (j < n && i < n) {
            if (LMin[i] < RMax[j]) {
                maxDiff = max(maxDiff, j - i);
                j = j + 1;
            }
            else
                i = i + 1;
        }
 
        return maxDiff;
    }
 
    /* Driver program to test the above functions */
    public static void main(String[] args)
    {
        FindMaximum max = new FindMaximum();
        int arr[] = { 9, 2, 3, 4, 5, 6, 7, 8, 18, 0 };
        int n = arr.length;
        int maxDiff = max.maxIndexDiff(arr, n);
        System.out.println(maxDiff);
    }
}
```

## Python3

```py
# Utility Functions to get max
# and minimum of two integers 
def max(a, b):
    if(a > b):
        return a
    else:
        return b
 
def min(a, b):
    if(a < b):
        return a
    else:
        return b
 
# For a given array arr[], 
# returns the maximum j - i
# such that arr[j] > arr[i]
def maxIndexDiff(arr, n):
    maxDiff = 0;
    LMin = [0] * n
    RMax = [0] * n
 
    # Construct LMin[] such that 
    # LMin[i] stores the minimum 
    # value from (arr[0], arr[1], 
    # ... arr[i]) 
    LMin[0] = arr[0]
    for i in range(1, n):
        LMin[i] = min(arr[i], LMin[i - 1])
 
    # Construct RMax[] such that 
    # RMax[j] stores the maximum 
    # value from (arr[j], arr[j + 1],
    # ..arr[n-1]) 
    RMax[n - 1] = arr[n - 1]
    for j in range(n - 2, -1, -1):
        RMax[j] = max(arr[j], RMax[j + 1]);
 
    # Traverse both arrays from left
    # to right to find optimum j - i
    # This process is similar to
    # merge() of MergeSort
    i, j = 0, 0
    maxDiff = -1
    while (j < n and i < n):
        if (LMin[i] < RMax[j]):
            maxDiff = max(maxDiff, j - i)
            j = j + 1
        else:
            i = i + 1
 
    return maxDiff
 
# Driver Code
if(__name__ == '__main__'):
    arr = [9, 2, 3, 4, 5, 
           6, 7, 8, 18, 0]
    n = len(arr)
    maxDiff = maxIndexDiff(arr, n)
    print (maxDiff)
 
# This code is contributed 
# by gautam karakoti
```

## C#

```cs
// C# program to find the maximum
// j – i such that arr[j] > arr[i]
using System;
 
class GFG {
    // Utility Functions to get max
    // and minimum of two integers
    static int max(int x, int y)
    {
        return x > y ? x : y;
    }
 
    static int min(int x, int y)
    {
        return x < y ? x : y;
    }
 
    // For a given array arr[], returns
    // the maximum j-i such thatarr[j] > arr[i]
    static int maxIndexDiff(int[] arr, int n)
    {
        int maxDiff;
        int i, j;
 
        int[] RMax = new int[n];
        int[] LMin = new int[n];
 
        // Construct LMin[] such that LMin[i]
        // stores the minimum value
        // from (arr[0], arr[1], ... arr[i])
        LMin[0] = arr[0];
        for (i = 1; i < n; ++i)
            LMin[i] = min(arr[i], LMin[i - 1]);
 
        // Construct RMax[] such that
        // RMax[j] stores the maximum value
        // from (arr[j], arr[j+1], ..arr[n-1])
        RMax[n - 1] = arr[n - 1];
        for (j = n - 2; j >= 0; --j)
            RMax[j] = max(arr[j], RMax[j + 1]);
 
        // Traverse both arrays from left
        // to right to find optimum j - i
        // This process is similar to merge()
        // of MergeSort
        i = 0;
        j = 0;
        maxDiff = -1;
        while (j < n && i < n) {
            if (LMin[i] < RMax[j]) {
                maxDiff = max(maxDiff, j - i);
                j = j + 1;
            }
            else
                i = i + 1;
        }
 
        return maxDiff;
    }
 
    // Driver program
    public static void Main()
    {
 
        int[] arr = { 9, 2, 3, 4, 5, 6, 7, 8, 18, 0 };
        int n = arr.Length;
        int maxDiff = maxIndexDiff(arr, n);
        Console.Write(maxDiff);
    }
}
// This Code is Contributed by Sam007
```

## PHP

```php
<?php 
// PHP program to find the maximum
// j – i such that arr[j] > arr[i]
 
// For a given array arr[], 
// returns the maximum j - i
// such that arr[j] > arr[i]
function maxIndexDiff($arr, $n)
{
    $maxDiff = 0;
    $LMin = array_fill(0, $n, NULL);
    $RMax = array_fill(0, $n, NULL);
 
    // Construct LMin[] such that 
    // LMin[i] stores the minimum 
    // value from (arr[0], arr[1], 
    // ... arr[i]) 
    $LMin[0] = $arr[0];
    for($i = 1; $i < $n; $i++)
        $LMin[$i] = min($arr[$i], 
                        $LMin[$i - 1]);
 
    // Construct RMax[] such that 
    // RMax[j] stores the maximum 
    // value from (arr[j], arr[j+1],
    // ..arr[n-1]) 
    $RMax[$n - 1] = $arr[$n - 1];
    for($j = $n - 2; $j >= 0; $j--)
        $RMax[$j] = max($arr[$j], 
                        $RMax[$j + 1]);
 
    // Traverse both arrays from left
    // to right to find optimum j - i
    // This process is similar to
    // merge() of MergeSort
    $i = 0;
    $j = 0;
    $maxDiff = -1;
    while ($j < $n && $i < $n)
        if ($LMin[$i] < $RMax[$j])
        {
            $maxDiff = max($maxDiff, $j - $i);
            $j = $j + 1;
        }
        else
            $i = $i + 1;
 
    return $maxDiff;
} 
 
// Driver Code
$arr = array(9, 2, 3, 4, 5, 
             6, 7, 8, 18, 0);
$n = sizeof($arr);
$maxDiff = maxIndexDiff($arr, $n);
echo $maxDiff;
 
// This code is contributed 
// by ChitraNayal
?>
```

输出：

```
8
```

时间复杂度：`O(n)`。

辅助空间：`O(n)`。