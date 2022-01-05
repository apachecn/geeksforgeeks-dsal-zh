# 找出任意两个元素之间的最小差异|设置 2

> 原文:[https://www . geesforgeks . org/find-任意两个元素之间的最小差异-set-2/](https://www.geeksforgeeks.org/find-minimum-difference-between-any-two-elements-set-2/)

给定一个大小为 **n** 的未排序数组 **arr[]** ，任务是找出给定数组中任意一对之间的最小差异。

> **输入:** arr[] = {1，2，3，4}
> **输出:** 1
> 可能的绝对差异为:
> {1，2，3，1，2，1}
> **输入:** arr[] = {10，2，5，4}
> **输出:** 1

**进场:**

1.  遍历数组并创建一个散列数组来存储数组元素的频率。
2.  现在，遍历散列数组并计算两个最近元素之间的距离。
3.  计算频率是为了检查某个元素的频率是否大于 1，这意味着绝对距离将为 0，即| arr[I]–arr[I]|。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 100001

// Function to return the minimum
// absolute difference between any
// two elements of the array
int getMinDiff(int arr[], int n)
{
    // To store the frequency of each element
    int freq[MAX] = { 0 };

    for (int i = 0; i < n; i++) {

        // Update the frequency of current element
        freq[arr[i]]++;

        // If current element appears more than once
        // then the minimum absolute difference
        // will be 0 i.e. |arr[i] - arr[i]|
        if (freq[arr[i]] > 1)
            return 0;
    }

    int mn = INT_MAX;

    // Checking the distance between the nearest
    // two elements in the frequency array
    for (int i = 0; i < MAX; i++) {
        if (freq[i] > 0) {
            i++;
            int cnt = 1;
            while ((freq[i] == 0) && (i != MAX - 1)) {
                cnt++;
                i++;
            }
            mn = min(cnt, mn);
            i--;
        }
    }

    // Return the minimum absolute difference
    return mn;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(int);

    cout << getMinDiff(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

private static final int MAX = 100001;

// Function to return the minimum
// absolute difference between any
// two elements of the array
static int getMinDiff(int arr[], int n)
{
    // To store the frequency of each element
    int[] freq = new int[MAX];
    for(int i = 0; i < n; i++)
    {
        freq[i] = 0;
    }
    for (int i = 0; i < n; i++)
    {

        // Update the frequency of current element
        freq[arr[i]]++;

        // If current element appears more than once
        // then the minimum absolute difference
        // will be 0 i.e. |arr[i] - arr[i]|
        if (freq[arr[i]] > 1)
            return 0;
    }

    int mn = Integer.MAX_VALUE;

    // Checking the distance between the nearest
    // two elements in the frequency array
    for (int i = 0; i < MAX; i++)
    {
        if (freq[i] > 0)
        {
            i++;
            int cnt = 1;
            while ((freq[i] == 0) && (i != MAX - 1))
            {
                cnt++;
                i++;
            }
            mn = Math.min(cnt, mn);
            i--;
        }
    }

    // Return the minimum absolute difference
    return mn;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4 };
    int n = arr.length;

    System.out.println(getMinDiff(arr, n));

}
}

// This code is contributed by nidhi16bcs2007
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 100001

# Function to return the minimum
# absolute difference between any
# two elements of the array
def getMinDiff(arr, n):

    # To store the frequency of each element
    freq = [0 for i in range(MAX)]

    for i in range(n):

        # Update the frequency of current element
        freq[arr[i]] += 1

        # If current element appears more than once
        # then the minimum absolute difference
        # will be 0 i.e. |arr[i] - arr[i]|
        if (freq[arr[i]] > 1):
            return 0

    mn = 10**9

    # Checking the distance between the nearest
    # two elements in the frequency array
    for i in range(MAX):
        if (freq[i] > 0):
            i += 1
            cnt = 1
            while ((freq[i] == 0) and (i != MAX - 1)):
                cnt += 1
                i += 1
            mn = min(cnt, mn)
            i -= 1

    # Return the minimum absolute difference
    return mn

# Driver code
arr = [ 1, 2, 3, 4]
n = len(arr)

print(getMinDiff(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    private static int MAX = 100001;

    // Function to return the minimum
    // absolute difference between any
    // two elements of the array
    static int getMinDiff(int []arr, int n)
    {
        // To store the frequency of each element
        int[] freq = new int[MAX];
        for(int i = 0; i < n; i++)
        {
            freq[i] = 0;
        }
        for (int i = 0; i < n; i++)
        {

            // Update the frequency of current element
            freq[arr[i]]++;

            // If current element appears more than once
            // then the minimum absolute difference
            // will be 0 i.e. |arr[i] - arr[i]|
            if (freq[arr[i]] > 1)
                return 0;
        }

        int mn = int.MaxValue;

        // Checking the distance between the nearest
        // two elements in the frequency array
        for (int i = 0; i < MAX; i++)
        {
            if (freq[i] > 0)
            {
                i++;
                int cnt = 1;
                while ((freq[i] == 0) && (i != MAX - 1))
                {
                    cnt++;
                    i++;
                }
                mn = Math.Min(cnt, mn);
                i--;
            }
        }

        // Return the minimum absolute difference
        return mn;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 4 };
        int n = arr.Length;

        Console.WriteLine(getMinDiff(arr, n));

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

let MAX = 100001;

// Function to return the minimum
// absolute difference between any
// two elements of the array
function getMinDiff(arr,n)
{
    // To store the frequency of each element
    let freq=[];
    for(let i = 0; i < n; i++)
    {
        freq[i] = 0;
    }
    for (let i = 0; i < n; i++)
    {

        // Update the frequency of current element
        freq[arr[i]]++;

        // If current element appears more than once
        // then the minimum absolute difference
        // will be 0 i.e. |arr[i] - arr[i]|
        if (freq[arr[i]] > 1)
            return 0;
    }

    let mn = Number.MAX_VALUE;

    // Checking the distance between the nearest
    // two elements in the frequency array
    for (let i = 0; i < MAX; i++)
    {
        if (freq[i] > 0)
        {
            i++;
            let cnt = 1;
            while ((freq[i] == 0) && (i != MAX - 1))
            {
                cnt++;
                i++;
            }
            mn = Math.min(cnt, mn);
            i--;
        }
    }

    // Return the minimum absolute difference
    return mn;
}

// Driver code

    let arr = [ 1, 2, 3, 4 ];
    let n = arr.length;

    document.write(getMinDiff(arr, n));

//contributed by 171fa07058

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(MAX)

说明:在上面的例子中，我们已经取 max 等于 100001，但是我们可以取 MAX 作为数组中的最大元素

**空间复杂度:** O(MAX)

说明:我们采用了最大尺寸的频率阵列。

**备选较短实施:**

## 蟒蛇 3

```
# Python3 implementation of the approach
import itertools

arr = [1,2,3,4]
diff_list = []

# Get the combinations of numbers
for n1, n2 in list(itertools.combinations(arr, 2)):

    # Find the absolute difference
    diff_list.append(abs(n1-n2))

print(min(diff_list))   

# This code is contributed by mailprakashindia
```

**Output:** 

```
1
```

**时间复杂度:**O(r *(T2)nC<sub>r</sub>)

说明:这里 r 是 2，因为我们使用迭代器工具组合两个元素，n 是给定数组的长度，所以如果我们计算它，它将是

O (n*(n-1)将是 O (n*n)

**空间复杂度:** O ( ( <sup>n</sup> C r))(这里，r=2)

说明:我们用列表来存储数组的所有组合，我们用 diff_list 数组来存储绝对差