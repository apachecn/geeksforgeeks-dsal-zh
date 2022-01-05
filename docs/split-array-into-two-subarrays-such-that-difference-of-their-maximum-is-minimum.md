# 将阵列分成两个子阵列，使它们的最大值之差最小

> 原文:[https://www . geeksforgeeks . org/将数组拆分为两个子数组，这样它们的最大值之差就是最小值/](https://www.geeksforgeeks.org/split-array-into-two-subarrays-such-that-difference-of-their-maximum-is-minimum/)

给定一个由整数组成的数组 **arr[]** ，任务是将给定的数组分成两个子数组，使得它们的最大元素之间的差异最小。

**示例:**

> **输入:** arr[] = {7，9，5，10}
> **输出:** 1
> **解释:**
> 子阵是{5，10}和{7，9}，它们的最大值之差= 10–9 = 1。
> **输入:** arr[] = {6，6，6}
> **输出:** 0

**方法:**
我们可以观察到，我们需要将阵列分成两个子阵列，这样:

*   如果最大元素在数组中出现不止一次，它需要在两个子数组中至少出现一次。
*   否则，最大和第二大元素应该出现在不同的子阵列中。

这确保了两个子阵列的最大元素之间的差异最大化。
因此，我们需要[对数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序，然后最大的 2 个元素，即 arr[n–1]和 arr[n–2]之间的差就是需要的答案。
以下是上述办法的实施:

## C++

```
// C++ Program to split a given
// array such that the difference
// between their maximums is minimized.

#include <bits/stdc++.h>
using namespace std;

int findMinDif(int arr[], int N)
{
    // Sort the array
    sort(arr, arr + N);

    // Return the difference
    // between two highest
    // elements
    return (arr[N - 1] - arr[N - 2]);
}

// Driver Program
int main()
{

    int arr[] = { 7, 9, 5, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findMinDif(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to split a given array
// such that the difference between
// their maximums is minimized.
import java.util.*;

class GFG{

static int findMinDif(int arr[], int N)
{

    // Sort the array
    Arrays.sort(arr);

    // Return the difference between
    // two highest elements
    return (arr[N - 1] - arr[N - 2]);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 7, 9, 5, 10 };
    int N = arr.length;

    System.out.println(findMinDif(arr, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 Program to split a given
# array such that the difference
# between their maximums is minimized.
def findMinDif(arr, N):

    # Sort the array
    arr.sort()

    # Return the difference
    # between two highest
    # elements
    return (arr[N - 1] - arr[N - 2])

# Driver Program
arr = [ 7, 9, 5, 10 ]
N = len(arr)
print(findMinDif(arr, N))

# This code is contributed by yatinagg
```

## C#

```
// C# Program to split a given array
// such that the difference between
// their maximums is minimized.
using System;
class GFG{

static int findMinDif(int []arr, int N)
{

    // Sort the array
    Array.Sort(arr);

    // Return the difference between
    // two highest elements
    return (arr[N - 1] - arr[N - 2]);
}

// Driver code
public static void Main()
{
    int []arr = { 7, 9, 5, 10 };
    int N = arr.Length;

    Console.Write(findMinDif(arr, N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// javascript Program to split a given array
// such that the difference between
// their maximums is minimized.

    function findMinDif(arr , N) {

        // Sort the array
        arr.sort((a,b)=>a-b);

        // Return the difference between
        // two highest elements
        return (arr[N - 1] - arr[N - 2]);
    }

    // Driver code

        var arr = [ 7, 9, 5, 10 ];
        var N = arr.length;

        document.write(findMinDif(arr, N));

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N*log(N))，N 是数组的元素个数。*