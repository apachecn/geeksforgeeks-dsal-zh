# 找出一个数组中包含 k 个不同元素所需的最小变化

> 原文:[https://www . geeksforgeeks . org/find-最小化-更改-要求在数组中包含 k 个不同的元素/](https://www.geeksforgeeks.org/find-minimum-changes-required-in-an-array-for-it-to-contain-k-distinct-elements/)

给定一个大小为 **N** 的数组**和一个数量为 **K** 的数组**。任务是找到数组中要替换的任意数量的最小元素，使数组由 **K** 个不同的元素组成。
**注意:**数组可能由重复元素组成。
**举例:**

> **输入:** arr[]={1，2，2，8}，k = 1
> **输出:** 2
> 需要更改的元素为 1，8
> **输入:** arr[]={1，2，7，8，2，3，2，3}，k = 2
> **输出:** 3
> 需要更改的元素为 1，7，8

**方法:**由于任务是替换数组中的最小元素，所以我们不会替换数组中频率更高的元素。所以定义一个数组**freq【】**存储数组 **arr** 中每个数字的频率，然后按降序排序 **freq** 。所以，首先 **freq** 阵列的 **k** 元素不需要更换。
以下是上述方法的实施:

## C++

```
// CPP program to minimum changes required
// in an array for k distinct elements.
#include <bits/stdc++.h>
using namespace std;

#define MAX 100005

// Function to minimum changes required
// in an array for k distinct elements.
int Min_Replace(int arr[], int n, int k)
{
    sort(arr, arr + n);

    // Store the frequency of each element
    int freq[MAX];

    memset(freq, 0, sizeof freq);

    int p = 0;
    freq[p] = 1;

    // Store the frequency of elements
    for (int i = 1; i < n; i++) {
        if (arr[i] == arr[i - 1])
            ++freq[p];
        else
            ++freq[++p];
    }

    // Sort frequencies in descending order
    sort(freq, freq + n, greater<int>());

    // To store the required answer
    int ans = 0;
    for (int i = k; i <= p; i++)
        ans += freq[i];

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 7, 8, 2, 3, 2, 3 };

    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 2;

    cout << Min_Replace(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// C# program to minimum changes required
// in an array for k distinct elements.
import java.util.*;

class GFG
{
    static int MAX = 100005;

    // Function to minimum changes required
    // in an array for k distinct elements.
    static int Min_Replace(int [] arr,
                           int n, int k)
    {
        Arrays.sort(arr);

        // Store the frequency of each element
        Integer [] freq = new Integer[MAX];
        Arrays.fill(freq, 0);
        int p = 0;
        freq[p] = 1;

        // Store the frequency of elements
        for (int i = 1; i < n; i++)
        {
            if (arr[i] == arr[i - 1])
                ++freq[p];
            else
                ++freq[++p];
        }

        // Sort frequencies in descending order
        Arrays.sort(freq, Collections.reverseOrder());

        // To store the required answer
        int ans = 0;
        for (int i = k; i <= p; i++)
            ans += freq[i];

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void main (String []args)
    {
        int [] arr = { 1, 2, 7, 8, 2, 3, 2, 3 };

        int n = arr.length;

        int k = 2;

        System.out.println(Min_Replace(arr, n, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to minimum changes required
# in an array for k distinct elements.
MAX = 100005

# Function to minimum changes required
# in an array for k distinct elements.
def Min_Replace(arr, n, k):
    arr.sort(reverse = False)

    # Store the frequency of each element
    freq = [0 for i in range(MAX)]

    p = 0
    freq[p] = 1

    # Store the frequency of elements
    for i in range(1, n, 1):
        if (arr[i] == arr[i - 1]):
            freq[p] += 1
        else:
            p += 1
            freq[p] += 1

    # Sort frequencies in descending order
    freq.sort(reverse = True)

    # To store the required answer
    ans = 0
    for i in range(k, p + 1, 1):
        ans += freq[i]

    # Return the required answer
    return ans

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 7, 8, 2, 3, 2, 3]

    n = len(arr)

    k = 2

    print(Min_Replace(arr, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to minimum changes required
// in an array for k distinct elements.
using System;

class GFG
{
    static int MAX = 100005;

    // Function to minimum changes required
    // in an array for k distinct elements.
    static int Min_Replace(int [] arr,
                           int n, int k)
    {
        Array.Sort(arr);

        // Store the frequency of each element
        int [] freq = new int[MAX];

        int p = 0;
        freq[p] = 1;

        // Store the frequency of elements
        for (int i = 1; i < n; i++)
        {
            if (arr[i] == arr[i - 1])
                ++freq[p];
            else
                ++freq[++p];
        }

        // Sort frequencies in descending order
        Array.Sort(freq);
        Array.Reverse(freq);

        // To store the required answer
        int ans = 0;
        for (int i = k; i <= p; i++)
            ans += freq[i];

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int [] arr = { 1, 2, 7, 8, 2, 3, 2, 3 };

        int n = arr.Length;

        int k = 2;

        Console.WriteLine(Min_Replace(arr, n, k));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript program to minimum changes required
// in an array for k distinct elements.

var MAX = 100005;

// Function to minimum changes required
// in an array for k distinct elements.
function Min_Replace(arr, n, k)
{
    arr.sort((a,b)=>a-b)

    // Store the frequency of each element
    var freq = Array(MAX).fill(0);

    var p = 0;
    freq[p] = 1;

    // Store the frequency of elements
    for (var i = 1; i < n; i++) {
        if (arr[i] == arr[i - 1])
            ++freq[p];
        else
            ++freq[++p];
    }

    // Sort frequencies in descending order
    freq.sort((a,b)=>b-a);

    // To store the required answer
    var ans = 0;
    for (var i = k; i <= p; i++)
        ans += freq[i];

    // Return the required answer
    return ans;
}

// Driver code
var arr = [1, 2, 7, 8, 2, 3, 2, 3];
var n = arr.length;
var k = 2;
document.write( Min_Replace(arr, n, k));

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(NlogN)