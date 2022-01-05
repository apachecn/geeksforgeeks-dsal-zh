# 在右侧找到最远的较小数字

> 原文:[https://www . geesforgeks . org/find-最右边的小数字/](https://www.geeksforgeeks.org/find-the-farthest-smaller-number-in-the-right-side/)

给定一个大小为 **N** 的数组 **arr[]** 。对于数组中的每个元素，任务是找到数组中最右边的元素的索引，它比当前元素小。如果没有这样的号码，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {3，1，5，2，4}
> **输出:** 3 -1 4 -1 -1
> arr[3]是 arr[0]右边最远的最小元素。
> arr[4]是 arr[2]右边最远的最小元素。
> 对于其余的元素，它们的右边没有更小的元素。
> 
> **输入:** arr[] = {1，2，3，4，0}
> **输出:** 4 4 4 4 -1

**方法:**一种有效的方法是创建一个**后缀 _min[]** 数组，其中**后缀 _min[i]** 存储子数组**arr[I…N–1]**中的最小元素。现在对于任何元素 **arr[i]** ，[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以在子阵列**后缀 _ min[I+1…N–1]**上使用，以找到 **arr[i]** 右侧最远的最小元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the farthest
// smaller number in the right side
void farthest_min(int a[], int n)
{
    // To store minimum element
    // in the range i to n
    int suffix_min[n];
    suffix_min[n - 1] = a[n - 1];
    for (int i = n - 2; i >= 0; i--) {
        suffix_min[i] = min(suffix_min[i + 1], a[i]);
    }

    for (int i = 0; i < n; i++) {
        int low = i + 1, high = n - 1, ans = -1;

        while (low <= high) {
            int mid = (low + high) / 2;

            // If current element in the suffix_min
            // is less than a[i] then move right
            if (suffix_min[mid] < a[i]) {
                ans = mid;
                low = mid + 1;
            }
            else
                high = mid - 1;
        }

        // Print the required answer
        cout << ans << " ";
    }
}

// Driver code
int main()
{
    int a[] = { 3, 1, 5, 2, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    farthest_min(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to find the farthest
    // smaller number in the right side
    static void farthest_min(int[] a, int n)
    {
        // To store minimum element
        // in the range i to n
        int[] suffix_min = new int[n];

        suffix_min[n - 1] = a[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            suffix_min[i]
                = Math.min(suffix_min[i + 1], a[i]);
        }

        for (int i = 0; i < n; i++) {
            int low = i + 1, high = n - 1, ans = -1;

            while (low <= high) {
                int mid = (low + high) / 2;

                // If current element in the suffix_min
                // is less than a[i] then move right
                if (suffix_min[mid] < a[i]) {
                    ans = mid;
                    low = mid + 1;
                }
                else
                    high = mid - 1;
            }

            // Print the required answer
            System.out.print(ans + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] a = { 3, 1, 5, 2, 4 };
        int n = a.length;

        farthest_min(a, n);
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the farthest
# smaller number in the right side

def farthest_min(a, n):

    # To store minimum element
    # in the range i to n
    suffix_min = [0 for i in range(n)]
    suffix_min[n - 1] = a[n - 1]
    for i in range(n - 2, -1, -1):
        suffix_min[i] = min(suffix_min[i + 1], a[i])

    for i in range(n):
        low = i + 1
        high = n - 1
        ans = -1

        while (low <= high):
            mid = (low + high) // 2

            # If current element in the suffix_min
            # is less than a[i] then move right
            if (suffix_min[mid] < a[i]):
                ans = mid
                low = mid + 1
            else:
                high = mid - 1

        # Print the required answer
        print(ans, end=" ")

# Driver code
a = [3, 1, 5, 2, 4]
n = len(a)

farthest_min(a, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to find the farthest
    // smaller number in the right side
    static void farthest_min(int[] a, int n)
    {
        // To store minimum element
        // in the range i to n
        int[] suffix_min = new int[n];

        suffix_min[n - 1] = a[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            suffix_min[i]
                = Math.Min(suffix_min[i + 1], a[i]);
        }

        for (int i = 0; i < n; i++) {
            int low = i + 1, high = n - 1, ans = -1;

            while (low <= high) {
                int mid = (low + high) / 2;

                // If current element in the suffix_min
                // is less than a[i] then move right
                if (suffix_min[mid] < a[i]) {
                    ans = mid;
                    low = mid + 1;
                }
                else
                    high = mid - 1;
            }

            // Print the required answer
            Console.Write(ans + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int[] a = { 3, 1, 5, 2, 4 };
        int n = a.Length;

        farthest_min(a, n);
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
Javascript<script>

// Javascript implementation of the approach

// Function to find the farthest
// smaller number in the right side
function farthest_min(a, n)
{
    // To store minimum element
    // in the range i to n
    let suffix_min = new Array(n);
    suffix_min[n - 1] = a[n - 1];
    for (let i = n - 2; i >= 0; i--) {
        suffix_min[i] = Math.min(suffix_min[i + 1], a[i]);
    }

    for (let i = 0; i < n; i++) {
        let low = i + 1, high = n - 1, ans = -1;

        while (low <= high) {
            let mid = Math.floor((low + high) / 2);

            // If current element in the suffix_min
            // is less than a[i] then move right
            if (suffix_min[mid] < a[i]) {
                ans = mid;
                low = mid + 1;
            }
            else
                high = mid - 1;
        }

        // Print the required answer
        document.write(ans + " ");
    }
}

// Driver code

    let a = [ 3, 1, 5, 2, 4 ];
    let n = a.length;

    farthest_min(a, n);

//This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
3 -1 4 -1 -1 
```

**时间复杂度:** O(N* log(N) )
**辅助空间:** O(N)