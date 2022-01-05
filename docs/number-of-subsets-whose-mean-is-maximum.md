# 平均值最大的子集数量

> 原文:[https://www . geesforgeks . org/子集数量-其平均值为最大值/](https://www.geeksforgeeks.org/number-of-subsets-whose-mean-is-maximum/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是计算平均值最大的 **arr[]** 的子集数量。

**示例:**

> **输入:** arr[] = {1，2，1，2}
> **输出:** 3
> 最大均值的子集为{2}、{2}和{2，2}。
> 
> **输入:**arr[]= { 1 }
> T3】输出: 1

**方法:**任何子集平均值的最大值将是该子集仅由数组中的最大元素组成时的值。因此，为了计数所有可能的子集，从数组中找到最大元素的频率，比如 **cnt** ，并且可能的子集的计数将是**2<sup>CNT</sup>–1**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// subsets with the maximum mean
int cntSubSets(int arr[], int n)
{

    // Maximum value from the array
    int maxVal = *max_element(arr, arr + n);

    // To store the number of times maximum
    // element appears in the array
    int cnt = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] == maxVal)
            cnt++;
    }

    // Return the count of valid subsets
    return (pow(2, cnt) - 1);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 2 };
    int n = sizeof(arr) / sizeof(int);

    cout << cntSubSets(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of
// subsets with the maximum mean
static int cntSubSets(int arr[], int n)
{

    // Maximum value from the array
    int maxVal = Arrays.stream(arr).max().getAsInt();

    // To store the number of times maximum
    // element appears in the array
    int cnt = 0;
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == maxVal)
            cnt++;
    }

    // Return the count of valid subsets
    return (int) (Math.pow(2, cnt) - 1);
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 1, 2, 1, 2 };
    int n = arr.length;

    System.out.println(cntSubSets(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# subsets with the maximum mean
def cntSubSets(arr, n) :

    # Maximum value from the array
    maxVal = max(arr);

    # To store the number of times maximum
    # element appears in the array
    cnt = 0;
    for i in range(n) :
        if (arr[i] == maxVal) :
            cnt += 1;

    # Return the count of valid subsets
    return ((2 ** cnt) - 1);

# Driver code
if __name__ == "__main__" :

    arr= [ 1, 2, 1, 2 ];
    n = len(arr);

    print(cntSubSets(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

// Function to return the count of
// subsets with the maximum mean
static int cntSubSets(int []arr, int n)
{

    // Maximum value from the array
    int maxVal = arr.Max();

    // To store the number of times maximum
    // element appears in the array
    int cnt = 0;
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == maxVal)
            cnt++;
    }

    // Return the count of valid subsets
    return (int) (Math.Pow(2, cnt) - 1);
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 2, 1, 2 };
    int n = arr.Length;

    Console.WriteLine(cntSubSets(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// subsets with the maximum mean
function cntSubSets(arr, n)
{

    // Maximum value from the array
    var maxVal =  arr.reduce(function(a, b)
    {
    return Math.max(a, b);
    });

    // To store the number of times maximum
    // element appears in the array
    var cnt = 0;
    for (var i = 0; i < n; i++) {
        if (arr[i] == maxVal)
            cnt++;
    }

    // Return the count of valid subsets
    return (Math.pow(2, cnt) - 1);
}

// Driver code
var arr = [ 1, 2, 1, 2 ]
var n = arr.length;
document.write(cntSubSets(arr, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n)