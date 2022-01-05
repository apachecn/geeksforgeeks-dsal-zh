# 最小子阵列，其元素的二进制表示的串联中的 1 的数量至少为 K

> 原文:[https://www . geeksforgeeks . org/最小子数组-这样其元素的二进制表示的 1 的串联数至少为-k/](https://www.geeksforgeeks.org/minimum-sub-array-such-that-number-of-1s-in-concatenation-of-binary-representation-of-its-elements-is-at-least-k/)

给定一个由非负整数和整数 **k** 组成的数组 **arr[]** 。任务是找到**arr【】**的任何子数组的最小长度，这样如果这个子数组的所有元素都用二进制表示法表示，并连接起来形成一个二进制字符串，那么结果字符串中的 1 的数量至少为 **k** 。如果不存在这样的子阵列，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {4，3，7，9}，k = 4
> **输出:** 2
> 一个可能的子数组是{3，7}。
> 
> **输入:** arr[] = {1，2，4，8}，k = 2
> T3】输出: 2

**方法:**想法是使用两个变量 **j** 和 **i** 并分别将其初始化为 0 和 1，以及一个数组 **count_one** ，该数组将存储数组中特定元素的二进制表示中存在的 1 的数量，以及一个变量 **sum** 存储直到索引的 1 的数量，以及 **ans** 存储最小长度。现在迭代数组，如果 **count_one** 的 ith 或 jth 元素的 1 的个数等于 k，那么将 ans 更新为 1，如果到 ith 元素的 1 的个数之和大于或等于 k，那么将 **ans** 更新为 ans 和(i-j)+1 的**最小值，否则如果小于 k，那么将 j 增加 1，以增加 **sum** 的值。**

以下是该方法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Finds the sub-array with maximum length
int FindSubarray(int arr[], int n, int k)
{
    // Array which stores number of ones
    // present in the binary representation
    // of ith element of the array
    int count_one[n];

    for (int i = 0; i < n; i++) {
        count_one[i] = __builtin_popcount(arr[i]);
    }

    // Sum variable to store sum of
    // number of ones
    // Initialize it as number of ones
    // present in the binary representation
    // of 0th element of the array
    int sum = count_one[0];

    // If there is only a single element
    if (n == 1) {
        if (count_one[0] >= k)
            return 1;
        else
            return -1;
    }

    // Stores the minimum length
    // of the required sub-array
    int ans = INT_MAX;

    int i = 1;
    int j = 0;

    while (i < n) {
        // If binary representation of jth
        // element of array has 1's equal to k
        if (k == count_one[j]) {
            ans = 1;
            break;
        }

        // If binary representation of ith
        // element of array has 1's equal to k
        else if (k == count_one[i]) {
            ans = 1;
            break;
        }

        // If sum of number of 1's of
        // binary representation of elements upto
        // ith element is less than k
        else if (sum + count_one[i] < k) {
            sum += count_one[i];
            i++;
        }

        // If sum of number of 1's of
        // binary representation of elements upto
        // ith element is greater than k
        else if (sum + count_one[i] > k) {
            ans = min(ans, (i - j) + 1);
            sum -= count_one[j];
            j++;
        }

        else if (sum + count_one[i] == k) {
            ans = min(ans, (i - j) + 1);
            sum += count_one[i];
            i++;
        }
    }

    if (ans != INT_MAX)
        return ans;

    else
        return -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 8 };
    int n = sizeof(arr) / sizeof(int);
    int k = 2;

    cout << FindSubarray(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Finds the sub-array with maximum length
static int FindSubarray(int arr[], int n, int k)
{
    // Array which stores number of ones
    // present in the binary representation
    // of ith element of the array
    int []count_one = new int[n];

    for (int i = 0; i < n; i++)
    {
        count_one[i] = Integer.bitCount(arr[i]);
    }

    // Sum variable to store sum of
    // number of ones
    // Initialize it as number of ones
    // present in the binary representation
    // of 0th element of the array
    int sum = count_one[0];

    // If there is only a single element
    if (n == 1)
    {
        if (count_one[0] >= k)
            return 1;
        else
            return -1;
    }

    // Stores the minimum length
    // of the required sub-array
    int ans = Integer.MAX_VALUE;

    int i = 1;
    int j = 0;

    while (i < n)
    {
        // If binary representation of jth
        // element of array has 1's equal to k
        if (k == count_one[j])
        {
            ans = 1;
            break;
        }

        // If binary representation of ith
        // element of array has 1's equal to k
        else if (k == count_one[i])
        {
            ans = 1;
            break;
        }

        // If sum of number of 1's of
        // binary representation of elements upto
        // ith element is less than k
        else if (sum + count_one[i] < k)
        {
            sum += count_one[i];
            i++;
        }

        // If sum of number of 1's of
        // binary representation of elements upto
        // ith element is greater than k
        else if (sum + count_one[i] > k)
        {
            ans = Math.min(ans, (i - j) + 1);
            sum -= count_one[j];
            j++;
        }

        else if (sum + count_one[i] == k)
        {
            ans = Math.min(ans, (i - j) + 1);
            sum += count_one[i];
            i++;
        }
    }

    if (ans != Integer.MAX_VALUE)
        return ans;

    else
        return -1;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 4, 8 };
    int n = arr.length;
    int k = 2;

    System.out.println(FindSubarray(arr, n, k));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys;

# Finds the sub-array with maximum length
def FindSubarray(arr, n, k) :

    # Array which stores number of ones
    # present in the binary representation
    # of ith element of the array
    count_one = [0] * n;

    for i in range(n) :
        count_one[i] = bin(arr[i]).count('1');

    # Sum variable to store sum of
    # number of ones
    # Initialize it as number of ones
    # present in the binary representation
    # of 0th element of the array
    sum = count_one[0];

    # If there is only a single element
    if (n == 1) :

        if (count_one[0] >= k) :
            return 1;
        else :
            return -1;

    # Stores the minimum length
    # of the required sub-array
    ans = sys.maxsize;

    i = 1;
    j = 0;

    while (i < n) :

        # If binary representation of jth
        # element of array has 1's equal to k
        if (k == count_one[j]) :
            ans = 1;
            break;

        # If binary representation of ith
        # element of array has 1's equal to k
        elif (k == count_one[i]) :
            ans = 1;
            break;

        # If sum of number of 1's of
        # binary representation of elements upto
        # ith element is less than k
        elif (sum + count_one[i] < k) :
            sum += count_one[i];
            i += 1;

        # If sum of number of 1's of
        # binary representation of elements upto
        # ith element is greater than k
        elif (sum + count_one[i] > k) :
            ans = min(ans, (i - j) + 1);
            sum -= count_one[j];
            j += 1;

        elif (sum + count_one[i] == k) :
            ans = min(ans, (i - j) + 1);
            sum += count_one[i];
            i += 1;

    if (ans != sys.maxsize) :
        return ans;

    else :
        return -1;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 4, 8 ];
    n = len(arr);
    k = 2;

    print(FindSubarray(arr, n, k));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Finds the sub-array with maximum length
static int FindSubarray(int []arr, int n, int k)
{
    // Array which stores number of ones
    // present in the binary representation
    // of ith element of the array
    int []count_one = new int[n];
    int i = 0;
    for (i = 0; i < n; i++)
    {
        count_one[i] = bitCount(arr[i]);
    }

    // Sum variable to store sum of
    // number of ones
    // Initialize it as number of ones
    // present in the binary representation
    // of 0th element of the array
    int sum = count_one[0];

    // If there is only a single element
    if (n == 1)
    {
        if (count_one[0] >= k)
            return 1;
        else
            return -1;
    }

    // Stores the minimum length
    // of the required sub-array
    int ans = int.MaxValue;

    i = 1;
    int j = 0;

    while (i < n)
    {
        // If binary representation of jth
        // element of array has 1's equal to k
        if (k == count_one[j])
        {
            ans = 1;
            break;
        }

        // If binary representation of ith
        // element of array has 1's equal to k
        else if (k == count_one[i])
        {
            ans = 1;
            break;
        }

        // If sum of number of 1's of
        // binary representation of elements upto
        // ith element is less than k
        else if (sum + count_one[i] < k)
        {
            sum += count_one[i];
            i++;
        }

        // If sum of number of 1's of
        // binary representation of elements upto
        // ith element is greater than k
        else if (sum + count_one[i] > k)
        {
            ans = Math.Min(ans, (i - j) + 1);
            sum -= count_one[j];
            j++;
        }

        else if (sum + count_one[i] == k)
        {
            ans = Math.Min(ans, (i - j) + 1);
            sum += count_one[i];
            i++;
        }
    }

    if (ans != int.MaxValue)
        return ans;

    else
        return -1;
}

static int bitCount(long x)
{
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 4, 8 };
    int n = arr.Length;
    int k = 2;

    Console.WriteLine(FindSubarray(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Finds the sub-array with maximum length
function FindSubarray(arr, n, k)
{

    // Array which stores number of ones
    // present in the binary representation
    // of ith element of the array
    let count_one = new Array(n);
    let i = 0;

    for(i = 0; i < n; i++)
    {
        count_one[i] = bitCount(arr[i]);
    }

    // Sum variable to store sum of
    // number of ones
    // Initialize it as number of ones
    // present in the binary representation
    // of 0th element of the array
    let sum = count_one[0];

    // If there is only a single element
    if (n == 1)
    {
        if (count_one[0] >= k)
            return 1;
        else
            return -1;
    }

    // Stores the minimum length
    // of the required sub-array
    let ans = Number.MAX_VALUE;

    i = 1;
    let j = 0;

    while (i < n)
    {

        // If binary representation of jth
        // element of array has 1's equal to k
        if (k == count_one[j])
        {
            ans = 1;
            break;
        }

        // If binary representation of ith
        // element of array has 1's equal to k
        else if (k == count_one[i])
        {
            ans = 1;
            break;
        }

        // If sum of number of 1's of
        // binary representation of elements upto
        // ith element is less than k
        else if (sum + count_one[i] < k)
        {
            sum += count_one[i];
            i++;
        }

        // If sum of number of 1's of
        // binary representation of elements upto
        // ith element is greater than k
        else if (sum + count_one[i] > k)
        {
            ans = Math.min(ans, (i - j) + 1);
            sum -= count_one[j];
            j++;
        }

        else if (sum + count_one[i] == k)
        {
            ans = Math.min(ans, (i - j) + 1);
            sum += count_one[i];
            i++;
        }
    }

    if (ans != Number.MAX_VALUE)
        return ans;
    else
        return -1;
}

function bitCount(x)
{
    let setBits = 0;

    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver code
let arr = [ 1, 2, 4, 8 ];
let n = arr.length;
let k = 2;

document.write(FindSubarray(arr, n, k));

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
2
```