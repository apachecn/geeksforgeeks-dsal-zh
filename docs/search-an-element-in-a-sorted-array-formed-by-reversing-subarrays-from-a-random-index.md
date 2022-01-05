# 从随机索引中搜索通过反转子阵列形成的排序数组中的元素

> 原文:[https://www . geeksforgeeks . org/search-从随机索引中反转子数组形成的排序数组中的元素/](https://www.geeksforgeeks.org/search-an-element-in-a-sorted-array-formed-by-reversing-subarrays-from-a-random-index/)

给定一个大小为 **N** 的排序后的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数**键，**的任务是找到数组中**键**出现的索引。给定的数组是通过将子数组 **{arr[0]，arr[R]}** 和 **{arr[R + 1]，arr[N–1]}**在某个随机索引 **R.** 处反转得到的，如果数组中没有**键**，打印 **-1** 。

**示例:**

> ***输入*** **:** arr[] = {4，3，2，1，8，7，6，5}，键= 2
> **输出:** 2
> 
> ***输入:*** arr[] = {10，8，6，5，2，1，13，12}，键= 4
> ***输出:*** -1

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查数组中是否存在**键**。如果找到，则打印索引。否则，打印 **-1。**

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方式:**优化上述方式，思路是在[阵](https://www.geeksforgeeks.org/array-data-structure/)上应用修改后的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到**键**。按照以下步骤解决此问题:

*   将 **l** 初始化为 **0** ，将 **h** 初始化为**N–1、**，以存储[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的搜索空间的边界元素的索引。
*   [迭代，而](https://www.geeksforgeeks.org/loops-in-python/) **l** 小于或等于 **h:**
    *   将中间值存储在一个变量中，**中间**为 **(l+h)/2** 。
    *   如果**arr【mid】**等于**键**、**T5】，则打印 **mid** 作为答案并返回。**
    *   如果**arr【l】**大于或等于 **arr【中】**、**T5，这意味着随机指数位于**中**的右侧。**
        *   如果**键**的值在 **arr【中间】**和**arr【l】**之间，则更新 **h** 到**中间 1**
        *   否则，将 **l** 更新为**中+1。**
    *   否则，意味着随机点位于**中间**的左侧。
    *   如果**键**的值在**arr【h】**和**arr【mid】之间，**将 **l** 更新为 **mid+1。**
    *   否则，将 **h** 更新为**1 月中旬**。
*   最后，如果没有找到**键**，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to search an element in a
// sorted array formed by reversing
// subarrays from a random index
int find(vector<int> arr, int N, int key)
{

    // Set the boundaries
    // for binary search
    int l = 0;
    int h = N - 1;

    // Apply binary search
    while (l <= h)
    {

        // Initialize the middle element
        int mid = (l + h) / 2;

        // If element found
        if (arr[mid] == key)
            return mid;

        // Random point is on
        // right side of mid
        if (arr[l] >= arr[mid])
        {

            // From l to mid arr
            // is reverse sorted
            if (arr[l] >= key && key >= arr[mid])
                h = mid - 1;
            else
                l = mid + 1;
        }

        // Random point is on
        // the left side of mid
        else
        {

            // From mid to h arr
            // is reverse sorted
            if (arr[mid] >= key && key >= arr[h])
                l = mid + 1;
            else
                h = mid - 1;
        }
    }

    // Return Not Found
    return -1;
}

// Driver Code
int main()
{

    // Given Input
    vector<int> arr = { 10, 8, 6, 5, 2, 1, 13, 12 };

    int N = arr.size();
    int key = 8;

    // Function Call
    int ans = find(arr, N, key);

    cout << ans;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG {

// Function to search an element in a
// sorted array formed by reversing
// subarrays from a random index
public static int find(Vector<Integer> arr, int N, int key)
{

    // Set the boundaries
    // for binary search
    int l = 0;
    int h = N - 1;

    // Apply binary search
    while (l <= h)
    {

        // Initialize the middle element
        int mid = (l + h) / 2;

        // If element found
        if (arr.get(mid) == key)
            return mid;

        // Random point is on
        // right side of mid
        if (arr.get(l) >= arr.get(mid))
        {

            // From l to mid arr
            // is reverse sorted
            if (arr.get(l) >= key && key >= arr.get(mid))
                h = mid - 1;
            else
                l = mid + 1;
        }

        // Random point is on
        // the left side of mid
        else
        {

            // From mid to h arr
            // is reverse sorted
            if (arr.get(mid) >= key && key >= arr.get(h))
                l = mid + 1;
            else
                h = mid - 1;
        }
    }

    // Return Not Found
    return -1;
}

// Drive Code
public static void main(String args[])
{
   Vector<Integer> arr = new Vector <Integer>();
   arr.add(10);
   arr.add(8);
   arr.add(6);
   arr.add(5);
   arr.add(2);
   arr.add(1);
   arr.add(13);
   arr.add(12);
    int N = arr.size();
    int key = 8;

    // Function Call
    int ans = find(arr, N, key);

      System.out.println( ans);
}

}

//This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to search an element in a
# sorted array formed by reversing
# subarrays from a random index
def find(arr, N, key):

    # Set the boundaries
    # for binary search
    l = 0
    h = N-1

    # Apply binary search
    while l <= h:

          # Initialize the middle element
        mid = (l+h)//2

        # If element found
        if arr[mid] == key:
            return mid

        # Random point is on
        # right side of mid
        if arr[l] >= arr[mid]:

            # From l to mid arr
            # is reverse sorted
            if arr[l] >= key >= arr[mid]:
                h = mid-1
            else:
                l = mid+1

        # Random point is on
        # the left side of mid
        else:

            # From mid to h arr
            # is reverse sorted
            if arr[mid] >= key >= arr[h]:
                l = mid+1
            else:
                h = mid-1

    # Return Not Found
    return -1

# Driver Code
if __name__ == "__main__":

    # Given Input
    arr = [10, 8, 6, 5, 2, 1, 13, 12]
    N = len(arr)
    key = 8

    # Function Call
    ans = find(arr, N, key)
    print(ans)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to search an element in a
// sorted array formed by reversing
// subarrays from a random index
static int find(List<int> arr, int N, int key)
{

    // Set the boundaries
    // for binary search
    int l = 0;
    int h = N - 1;

    // Apply binary search
    while (l <= h)
    {

        // Initialize the middle element
        int mid = (l + h) / 2;

        // If element found
        if (arr[mid] == key)
            return mid;

        // Random point is on
        // right side of mid
        if (arr[l] >= arr[mid])
        {

            // From l to mid arr
            // is reverse sorted
            if (arr[l] >= key && key >= arr[mid])
                h = mid - 1;
            else
                l = mid + 1;
        }

        // Random point is on
        // the left side of mid
        else
        {

            // From mid to h arr
            // is reverse sorted
            if (arr[mid] >= key && key >= arr[h])
                l = mid + 1;
            else
                h = mid - 1;
        }
    }

    // Return Not Found
    return -1;
}

// Driver Code
public static void Main()
{

    // Given Input
    List<int> arr = new List<int>(){ 10, 8, 6, 5,
                                     2, 1, 13, 12 };

    int N = arr.Count;
    int key = 8;

    // Function Call
    int ans = find(arr, N, key);

    Console.Write(ans);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to search an element in a
// sorted array formed by reversing
// subarrays from a random index
function find(arr, N, key)
{

    // Set the boundaries
    // for binary search
    let l = 0;
    let h = N - 1;

    // Apply binary search
    while (l <= h)
    {

        // Initialize the middle element
        let mid = Math.floor((l + h) / 2);

        // If element found
        if (arr[mid] == key)
            return mid;

        // Random point is on
        // right side of mid
        if (arr[l] >= arr[mid])
        {

            // From l to mid arr
            // is reverse sorted
            if (arr[l] >= key && key >= arr[mid])
                h = mid - 1;
            else
                l = mid + 1;
        }

        // Random point is on
        // the left side of mid
        else
        {

            // From mid to h arr
            // is reverse sorted
            if (arr[mid] >= key && key >= arr[h])
                l = mid + 1;
            else
                h = mid - 1;
        }
    }

    // Return Not Found
    return -1;
}

// Driver Code

    // Given Input
    let arr = [ 10, 8, 6, 5, 2, 1, 13, 12 ];

    let N = arr.length;
    let key = 8;

    // Function Call
    let ans = find(arr, N, key);

    document.write(ans);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*