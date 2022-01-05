# 给定数组的所有可能的非空子集的值的总和

> 原文:[https://www . geesforgeks . org/给定数组的所有可能非空子集的值之和/](https://www.geeksforgeeks.org/sum-of-values-of-all-possible-non-empty-subsets-of-the-given-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出给定数组中所有可能的非空数组子集的值之和。
**例:**

> **输入:** arr[] = {2，3}
> **输出:** 10
> 所有非空子集为{2}、{3}和{2，3}
> 总和= 2 + 3 + 2 + 3 = 10
> **输入:** arr[] = {2，1，5，6}
> **输出:** 112

**方法:**可以观察到，当从所有可能的子集添加所有元素时，原始数组的每个元素出现在**2<sup>(N–1)</sup>**次。这意味着最终答案中任何元素 **arr[i]** 的贡献将是**arr[I]* 2<sup>(N–1)</sup>**。所以，需要的答案是**(arr[0]+arr[1]+arr[2]+…+arr[N–1])* 2<sup>(N–1)</sup>**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required sum
int sum(int arr[], int n)
{

    // Find the sum of the array elements
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }

    // Every element appears 2^(n-1) times
    sum = sum * pow(2, n - 1);
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 2, 1, 5, 6 };
    int n = sizeof(arr) / sizeof(int);

    cout << sum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the required sum
    static int sum(int arr[], int n)
    {

        // Find the sum of the array elements
        int sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum += arr[i];
        }

        // Every element appears 2^(n-1) times
        sum = sum * (int)Math.pow(2, n - 1);
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 1, 5, 6 };
        int n = arr.length;
        System.out.println(sum(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required sum
def sum( arr, n):

    # Find the sum of the array elements
    sum = 0
    for i in arr :
        sum += i

    # Every element appears 2^(n-1) times
    sum = sum * pow(2, n - 1)
    return sum

# Driver code
arr = [ 2, 1, 5, 6 ]
n = len(arr)

print(sum(arr, n))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function to return the required sum
    static int sum(int[] arr, int n)
    {

        // Find the sum of the array elements
        int sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum += arr[i];
        }

        // Every element appears 2^(n-1) times
        sum = sum * (int)Math.Pow(2, n - 1);
        return sum;
    }

    // Driver code
    public static void Main ()
    {
        int[] arr = { 2, 1, 5, 6 };
        int n = arr.Length;
        Console.WriteLine(sum(arr, n));
    }
}

// This code is contributed by CodeMech
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Function to return the required sum
function sum(arr, n)
{

// Find the sum of the array elements
var sum = 0;
for (i = 0; i < n; i++)
{
sum += arr[i];
}

// Every element appears 2^(n-1) times
sum = sum * parseInt(Math.pow(2, n - 1));
return sum;
}

// Driver code

var arr = [ 2, 1, 5, 6 ];
var n = arr.length;
document.write(sum(arr, n));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
112
```