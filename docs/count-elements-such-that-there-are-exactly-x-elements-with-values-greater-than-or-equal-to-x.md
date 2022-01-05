# 对元素进行计数，以使正好有 X 个元素的值大于或等于 X

> 原文:[https://www . geeksforgeeks . org/count-elements-这样-有-恰好-x-elements-values-大于或等于-x/](https://www.geeksforgeeks.org/count-elements-such-that-there-are-exactly-x-elements-with-values-greater-than-or-equal-to-x/)

给定一个由 *N* 个整数组成的数组 *arr* ，任务是找出满足以下条件的元素个数:
如果元素是 *X* ，那么数组中必须有恰好 *X* 个大于或等于 *X*
**的元素个数(不包括 *X* 的个数)【示例:**

```
Input: arr[] = {1, 2, 3, 4}
Output: 1
Only element 2 satisfies the condition as 
there are exactly 2 elements which are greater
than or equal to 2 (3, 4) except 2 itself.

Input: arr[] = {5, 5, 5, 5, 5}
Output: 0
```

**方法:**该问题涉及有效搜索每个 arr[i]元素 arr[j]的数量(I！= j)大于或等于 arr[i]。

*   按升序对数组进行排序。
*   对于每个元素 arr[i]，使用二分搜索法得到除 arr[i]本身之外所有大于或等于 arr[i]的元素的计数。
*   如果计数等于 arr[i]，则递增结果。
*   最后打印结果的值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

ll int getCount(vector<ll int> v, int n)
{
    // Sorting the vector
    sort((v).begin(), (v).end());
    ll int cnt = 0;
    for (ll int i = 0; i < n; i++) {

        // Count of numbers which
        // are greater than v[i]
        ll int tmp = v.end() - 1
                     - upper_bound((v).begin(), (v).end(), v[i] - 1);

        if (tmp == v[i])
            cnt++;
    }
    return cnt;
}

// Driver code
int main()
{
    ll int n;
    n = 4;
    vector<ll int> v;
    v.push_back(1);
    v.push_back(2);
    v.push_back(3);
    v.push_back(4);

    cout << getCount(v, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    static int getCount(int[] v, int n)
    {

        // Sorting the vector
        Arrays.sort(v);
        int cnt = 0;
        for (int i = 0; i < n; i++)
        {

            // Count of numbers which
            // are greater than v[i]
            int tmp = n - 1 - upperBound(v, n, v[i] - 1);
            if (tmp == v[i])
                cnt++;
        }
        return cnt;
    }

    // Function to implement upper_bound()
    static int upperBound(int[] array, 
                          int length, int value)
    {
        int low = 0;
        int high = length;
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

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;
        int[] v = { 1, 2, 3, 4 };
        System.out.println(getCount(v, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from bisect import bisect as upper_bound

def getCount(v, n):

    # Sorting the vector
    v = sorted(v)
    cnt = 0
    for i in range(n):

        # Count of numbers which
        # are greater than v[i]
        tmp = n - 1 - upper_bound(v, v[i] - 1)

        if (tmp == v[i]):
            cnt += 1
    return cnt

# Driver codemain()
n = 4
v = []
v.append(1)
v.append(2)
v.append(3)
v.append(4)

print(getCount(v, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int getCount(int[] v, int n)
    {

        // Sorting the vector
        Array.Sort(v);
        int cnt = 0;
        for (int i = 0; i < n; i++)
        {

            // Count of numbers which
            // are greater than v[i]
            int tmp = n - 1 - upperBound(v, n, v[i] - 1);
            if (tmp == v[i])
                cnt++;
        }
        return cnt;
    }

    // Function to implement upper_bound()
    static int upperBound(int[] array,
                          int length, int value)
    {
        int low = 0;
        int high = length;
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

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 4;
        int[] v = { 1, 2, 3, 4 };
        Console.WriteLine(getCount(v, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    function getCount(v,n)
    {
        // Sorting the vector
        v.sort(function(a,b){return a-b;});
        let cnt = 0;
        for (let i = 0; i < n; i++)
        {

            // Count of numbers which
            // are greater than v[i]
            let tmp = n - 1 - upperBound(v, n, v[i] - 1);
            if (tmp == v[i])
                cnt++;
        }
        return cnt;
    }

    // Function to implement upper_bound()
    function upperBound(array,length,value)
    {
        let low = 0;
        let high = length;
        while (low < high)
        {
            let mid = Math.floor((low + high) / 2);
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

    // Driver Code
    let n = 4;
    let v=[1, 2, 3, 4];
    document.write(getCount(v, n));

// This code is contributed by unknown2108

</script>
```

**Output**

```
1
```

**时间复杂度:** O(N*logN)

**辅助空间:** O(1)