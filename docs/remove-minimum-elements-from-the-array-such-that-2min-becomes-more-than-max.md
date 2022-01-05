# 从数组中移除最小元素，使 2*min 大于 max

> 原文:[https://www . geeksforgeeks . org/从数组中移除最小元素，这样 2 分钟就可以超过最大值/](https://www.geeksforgeeks.org/remove-minimum-elements-from-the-array-such-that-2min-becomes-more-than-max/)

给定大小为 **N** 的数组。任务是从数组中移除最小元素，使得最小数量的两倍大于修改后数组中的最大数量。打印移除的最小元素数。
**例:**

> **输入:** arr[] = {4，5，100，9，10，11，12，15，200}
> **输出:** 4
> 移除 4 个元素(4，5，100，200)
> 使 2*min 大于 max。
> **输入:** arr[] = {4，7，5，6}
> **输出:** 0

**进场:**

*   给定数组排序
*   在数组中从左向右遍历，对于每个选择的元素(让它是 x)和索引 I，找到(2*x)的[上限](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)。让索引为 j。然后，如果(n-j+i)小于我们答案的当前值，则通过(n-j+i)更新我们所需的答案。

以下是上述方法的实现:

## C++

```
// CPP program to remove minimum elements from the
// array such that 2*min becomes more than max
#include <bits/stdc++.h>
using namespace std;

// Function to remove minimum elements from the
// array such that 2*min becomes more than max
int Removal(vector<int> v, int n)
{
    // Sort the array
    sort(v.begin(), v.end());

    // To store the required answer
    int ans = INT_MAX;

    // Traverse from left to right
    for (vector<int>::iterator i = v.begin(); i != v.end();
                                                     i++) {

        vector<int>::iterator j = upper_bound(v.begin(),
                                    v.end(), (2 * (*i)));

        // Update the answer
        ans = min(ans, n - (int)(j - i));
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    vector<int> a = { 4, 5, 100, 9, 10, 11, 12, 15, 200 };

    int n = a.size();

    // Function call
    cout << Removal(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove minimum elements from the
// array such that 2*min becomes more than max
import java.util.Arrays;

class GFG
{

    // Function to calculate upper bound
    public static int upperBound(int[] array,
                                 int value)
    {
        int low = 0;
        int high = array.length;
        while (low < high)
        {
            final int mid = (low + high) / 2;
            if (value >= array[mid])
            {
                low = mid + 1;
            }
            else
            {
                high = mid;
            }
        }
        return low;
    }

    // Function to remove minimum elements from the
    // array such that 2*min becomes more than max
    public static int Removal(int[] v, int n)
    {

        // Sort the array
        Arrays.sort(v);

        // To store the required answer
        int ans = Integer.MAX_VALUE;
        int k = 0;

        // Traverse from left to right
        for (int i : v)
        {
            int j = upperBound(v, (2 * i));

            // Update the answer
            ans = Math.min(ans, n - (j - k));
            k++;
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] a = { 4, 5, 100, 9, 10,
                    11, 12, 15, 200 };
        int n = a.length;

        // Function call
        System.out.println(Removal(a, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to remove minimum elements from the
# array such that 2*min becomes more than max
from bisect import bisect_left as upper_bound

# Function to remove minimum elements from the
# array such that 2*min becomes more than max
def Removal(v, n):

    # Sort the array
    v = sorted(v)

    # To store the required answer
    ans = 10**9

    # Traverse from left to right
    for i in range(len(v)):
        j = upper_bound(v, (2 * (a[i])))

        # Update the answer
        ans = min(ans, n - (j - i - 1))

    # Return the required answer
    return ans

# Driver code
a = [4, 5, 100, 9, 10, 11, 12, 15, 200]

n = len(a)

# Function call
print(Removal(a, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to remove minimum elements
// from the array such that 2*min becomes
// more than max
using System;

class GFG
{

    // Function to calculate upper bound
    public static int upperBound(int[] array,
                                 int value)
    {
        int low = 0;
        int high = array.Length;
        while (low < high)
        {
            int mid = (low + high) / 2;
            if (value >= array[mid])
            {
                low = mid + 1;
            }
            else
            {
                high = mid;
            }
        }
        return low;
    }

    // Function to remove minimum elements from the
    // array such that 2*min becomes more than max
    public static int Removal(int[] v, int n)
    {

        // Sort the array
        Array.Sort(v);

        // To store the required answer
        int ans = int.MaxValue;
        int k = 0;

        // Traverse from left to right
        foreach (int i in v)
        {
            int j = upperBound(v, (2 * i));

            // Update the answer
            ans = Math.Min(ans, n - (j - k));
            k++;
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] a = { 4, 5, 100, 9, 10,
                    11, 12, 15, 200 };
        int n = a.Length;

        // Function call
        Console.WriteLine(Removal(a, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript program to remove minimum elements
      // from the array such that 2*min becomes
      // more than max

      // Function to calculate upper bound
      function upperBound(array, value) {
        var low = 0;
        var high = array.length;
        while (low < high) {
          var mid = parseInt((low + high) / 2);
          if (value >= array[mid]) {
            low = mid + 1;
          } else {
            high = mid;
          }
        }
        return low;
      }

      // Function to remove minimum elements from the
      // array such that 2*min becomes more than max
      function Removal(v, n) {
        // Sort the array
        v.sort((a, b) => a - b);

        // To store the required answer
        var ans = 2147483648;
        var k = 0;

        // Traverse from left to right
        for (const i of v) {
          var j = upperBound(v, 2 * i);

          // Update the answer
          ans = Math.min(ans, n - (j - k));
          k++;
        }

        // Return the required answer
        return ans;
      }

      // Driver code
      var a = [4, 5, 100, 9, 10, 11, 12, 15, 200];
      var n = a.length;

      // Function call
      document.write(Removal(a, n));

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(NlogN)