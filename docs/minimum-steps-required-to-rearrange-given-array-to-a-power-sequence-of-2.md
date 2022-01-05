# 将给定数组重新排列为 2 的幂序列所需的最小步数

> 原文:[https://www . geesforgeks . org/重新排列给定数组到 2 的幂序列所需的最少步骤/](https://www.geeksforgeeks.org/minimum-steps-required-to-rearrange-given-array-to-a-power-sequence-of-2/)

给定一个由 **N** 正整数**组成的数组**arr【】**，任务是通过以下操作找到将给定的整数数组变成 **2** 的[次幂序列所需的最小步骤:](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)**

*   **给定数组重新排序。不算一步。**
*   **对于每一步，从数组中选择任意索引 **i** ，并将**arr【I】**更改为**arr【I】1**或**arr【I】+1**。**

> **一个序列被称为 **2、** if 的幂序列，对于每个 i <sup>第</sup>索引(0≤I≤N-1)**、**
> **arr【I】= 2<sup>I</sup>**，其中 **N** 是给定数组的长度。**

****示例:****

> ****输入:** arr[] = { 1，8，2，10，6 }
> **输出:** 8
> **解释:**
> 将数组 arr[]重新排序为{ 1，2，6，8，10 }
> 步骤 1:将 arr[2]递减为 5
> 步骤 2:将 arr[2]递减为 4
> 步骤 3–8:将 arr[4]递增 1。arr[4]的最终值变为 16。
> 因此，arr[] = {1，2，4，8，16}
> 因此，获得 2 的幂序列所需的最小步数是 8。**
> 
>  ****输入:** arr[] = { 1，3，4 }
> T3】输出: 1**

****方法:**为了解决给定的问题，思路是[按照升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组进行排序，对于排序后的数组的每个 i <sup>第</sup>个索引，计算**arr【I】**<sub>和 **2 <sup>i</sup>** 之间的绝对差值。绝对差异的总和给了我们所需的答案。</sub>**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// steps required to convert given
// array into a power sequence of 2
int minsteps(int arr[], int n)
{

    // Sort the array in
    // ascending order
    sort(arr, arr + n);

    int ans = 0;

    // Calculate the absolute difference
    // between arr[i] and 2^i for each index
    for (int i = 0; i < n; i++) {
        ans += abs(arr[i] - pow(2, i));
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 8, 2, 10, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minsteps(arr, n) << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to implement
// the above approach

import java.util.*;
import java.lang.Math;

class GFG {

    // Function to calculate the minimum
    // steps required to convert given
    // array into a power sequence of 2
    static int minsteps(int arr[], int n)
    {
        // Sort the array in ascending order
        Arrays.sort(arr);
        int ans = 0;

        // Calculate the absolute difference
        // between arr[i] and 2^i for each index
        for (int i = 0; i < n; i++) {
            ans += Math.abs(arr[i] - Math.pow(2, i));
        }
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 8, 2, 10, 6 };
        int n = arr.length;
        System.out.println(minsteps(arr, n));
    }
}
```

## **蟒蛇 3**

```
# Python 3 program for the above approach

# Function to calculate the minimum
# steps required to convert given
# array into a power sequence of 2
def minsteps(arr, n):

    # Sort the array in ascending order
    arr.sort()
    ans = 0
    for i in range(n):
        ans += abs(arr[i]-pow(2, i))
    return ans

# Driver Code
arr = [1, 8, 2, 10, 6]
n = len(arr)
print(minsteps(arr, n))
```

## **C#**

```
// C# Program to the above approach

using System;

class GFG {

    // Function to calculate the minimum
    // steps required to convert given
    // array into a power sequence of 2
    static int minsteps(int[] arr, int n)
    {

        // Sort the array in ascending order
        Array.Sort(arr);
        int ans = 0;

        // Calculate the absolute difference
        // between arr[i] and 2^i for each index
        for (int i = 0; i < n; i++) {
            ans += Math.Abs(arr[i]
                            - (int)(Math.Pow(2, i)));
        }
        return ans;
    }

    // Driver Code
    public static void Main()
    {

        int[] arr = { 1, 8, 2, 10, 6 };
        int n = arr.Length;
        Console.WriteLine(minsteps(arr, n));
    }
}
```

## **java 描述语言**

```
<script>
// Javascript program to implement
// the above approach

// Function to calculate the minimum
// steps required to convert given
// array into a power sequence of 2
function minsteps(arr, n)
{

    // Sort the array in
    // ascending order
    arr.sort((a,b)=>a-b)

    var ans = 0;

    // Calculate the absolute difference
    // between arr[i] and 2^i for each index
    for (var i = 0; i < n; i++) {
        ans += Math.abs(arr[i] - Math.pow(2, i));
    }

    // Return the answer
    return ans;
}

// Driver Code
var arr = [ 1, 8, 2, 10, 6 ];
var n = arr.length;
document.write( minsteps(arr, n));

// This code is contributed by noob2000.
</script>
```

****Output:** 

```
8
```** 

*****时间复杂度:** O(NlogN)*
***辅助空间:** O(1)***