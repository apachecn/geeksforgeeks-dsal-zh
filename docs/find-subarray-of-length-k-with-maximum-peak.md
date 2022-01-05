# 找到最大峰值长度为 K 的子阵列

> 原文:[https://www . geesforgeks . org/find-最大峰值长度为 k 的子阵列/](https://www.geeksforgeeks.org/find-subarray-of-length-k-with-maximum-peak/)

给定一个长度为 n 的**数组 arr【】**和一个**正整数 K** ，我们必须找到一个长度为 K 的子数组，其中包含最大峰值。
线段【l，r】的峰是这样的指标，即 **l < i < r** 、**a【I-1】<a【I】**和**a【I+1】<a【I】**。
***注:**线段的边界指数 l 和 r 不是峰值。如果有许多子阵列具有最大峰值，则打印具有最小左索引的子阵列。*
**例:**

> **输入:**
> arr = {3，1，4，1，5，9，2，6}，k = 7
> **输出:**
> Left = 1
> Right = 7
> Peak = 2
> **说明:**
> 有两个长度为 7 的子阵列，即【1，7】和【2，8】。两个子阵列都有 2 个峰值，即 3 和 6 指数是两个子阵列的峰值。我们必须返回具有最小 l 和最大峰值的子阵列，即 l = 1 和峰值= 2。
> **输入:**
> arr = {3，2，3，2，1}，k = 3
> **输出:**
> Left = 2
> Right = 4
> Peak = 1
> **解释:**
> 只有一个长度为 3 且内部峰数为 1 的子阵列，即 l =2，Peak 为 i = 3。

**方法:**
解决这个问题的方法是使用一个[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)，我们在 K 大小的窗口上滑动，找到每个窗口的峰值总数，哪个窗口给出的峰值数最大，哪个就是答案。当移动右索引时，我们检查添加的索引是否是峰值，我们增加计数，当移动左索引时，我们检查移除的索引是否是峰值，如果是，则减少计数。我们总是有一个 K 大小的窗户。
**下面是上述方法的实现:**

## C++

```
// C++ implementation to Find subarray
// of Length K with Maximum Peak

#include <bits/stdc++.h>
using namespace std;

// Function to find the subarray
void findSubArray(int* a, int n, int k)
{
    // Make prefix array to store
    // the prefix sum of peak count
    int pref[n];

    pref[0] = 0;

    for (int i = 1; i < n - 1; ++i) {

        // Count peak for previous index
        pref[i] = pref[i - 1];

        // Check if this element is a peak
        if (a[i] > a[i - 1] && a[i] > a[i + 1])

            // Increment the count
            pref[i]++;
    }

    int peak = 0, left = 0;

    for (int i = 0; i + k - 1 < n; ++i)

        // Check if number of peak in the sub array
        // whose l = i is greater or not
        if (pref[i + k - 2] - pref[i] > peak) {
            peak = pref[i + k - 2] - pref[i];
            left = i;
        }

    // Print the result
    cout << "Left = " << left + 1 << endl;
    cout << "Right = " << left + k << endl;
    cout << "Peak = " << peak << endl;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 3, 2, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 3;

    findSubArray(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Find subarray
// of Length K with Maximum Peak

class GFG{

// Function to find the subarray
static void findSubArray(int []a, int n, int k)
{
    // Make prefix array to store
    // the prefix sum of peak count
    int []pref = new int[n];

    pref[0] = 0;

    for (int i = 1; i < n - 1; ++i) {

        // Count peak for previous index
        pref[i] = pref[i - 1];

        // Check if this element is a peak
        if (a[i] > a[i - 1] && a[i] > a[i + 1])

            // Increment the count
            pref[i]++;
    }

    int peak = 0, left = 0;

    for (int i = 0; i + k - 1 < n; ++i)

        // Check if number of peak in the sub array
        // whose l = i is greater or not
        if (pref[i + k - 2] - pref[i] > peak) {
            peak = pref[i + k - 2] - pref[i];
            left = i;
        }

    // Print the result
    System.out.print("Left = " +  (left + 1) +"\n");
    System.out.print("Right = " +  (left + k) +"\n");
    System.out.print("Peak = " +  peak +"\n");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 3, 2, 1 };

    int n = arr.length;

    int k = 3;

    findSubArray(arr, n, k);

}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to Find subarray
# of Length K with Maximum Peak

# Function to find the subarray
def findSubArray(a, n, k):

    # Make prefix array to store
    # the prefix sum of peak count
    pref = [0 for i in range(n)]

    pref[0] = 0

    for i in range(1, n - 1, 1):
        # Count peak for previous index
        pref[i] = pref[i - 1]

        # Check if this element is a peak
        if (a[i] > a[i - 1] and a[i] > a[i + 1]):
            # Increment the count
            pref[i] += 1

    peak = 0
    left = 0

    for i in range(0, n - k + 1, 1):

        # Check if number of peak in the sub array
        # whose l = i is greater or not
        if (pref[i + k - 2] - pref[i] > peak):
            peak = pref[i + k - 2] - pref[i]
            left = i

    # Print the result
    print("Left =",left + 1)
    print("Right =",left + k)
    print("Peak =",peak)

# Driver code
if __name__ == '__main__':
    arr = [3, 2, 3, 2, 1]

    n = len(arr)
    k = 3
    findSubArray(arr, n, k)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation to Find subarray
// of Length K with Maximum Peak
using System;

class GFG{

// Function to find the subarray
static void findSubArray(int []a, int n, int k)
{

    // Make prefix array to store
    // the prefix sum of peak count
    int []pref = new int[n];

    pref[0] = 0;

    for(int i = 1; i < n - 1; ++i)
    {

       // Count peak for previous index
       pref[i] = pref[i - 1];

       // Check if this element is a peak
       if (a[i] > a[i - 1] && a[i] > a[i + 1])
       {
           // Increment the count
           pref[i]++;
       }
    }

    int peak = 0;
    int left = 0;

    for(int i = 0; i + k - 1 < n; ++i)
    {

       // Check if number of peak in the sub array
       // whose l = i is greater or not
       if (pref[i + k - 2] - pref[i] > peak)
       {
           peak = pref[i + k - 2] - pref[i];
           left = i;
       }
    }

    // Print the result
    Console.Write("Left = " + (left + 1) + "\n");
    Console.Write("Right = " + (left + k) + "\n");
    Console.Write("Peak = " + peak + "\n");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 2, 3, 2, 1 };
    int n = arr.Length;
    int k = 3;

    findSubArray(arr, n, k);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// Javascript implementation to Find subarray
// of Length K with Maximum Peak

// Function to find the subarray
function findSubArray(a, n, k)
{

    // Make prefix array to store
    // the prefix sum of peak count
    let pref = new Array(n);

    pref[0] = 0;

    for (let i = 1; i < n - 1; ++i)
    {

        // Count peak for previous index
        pref[i] = pref[i - 1];

        // Check if this element is a peak
        if (a[i] > a[i - 1] && a[i] > a[i + 1])

            // Increment the count
            pref[i]++;
    }

    let peak = 0, left = 0;

    for (let i = 0; i + k - 1 < n; ++i)

        // Check if number of peak in the sub array
        // whose l = i is greater or not
        if (pref[i + k - 2] - pref[i] > peak) {
            peak = pref[i + k - 2] - pref[i];
            left = i;
        }

    // Print the result
    document.write("Left = " + (left + 1) + "<br>");
    document.write("Right = " + (left + k) + "<br>");
    document.write("Peak = " + peak + "<br>");
}

// Driver code
let arr = [3, 2, 3, 2, 1];
let n = arr.length;
let k = 3;

findSubArray(arr, n, k);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
Left = 2
Right = 4
Peak = 1
```

**时间复杂度:** O(N)