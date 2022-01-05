# 检查数组中是否有一个元素等于所有剩余元素的总和

> 原文:[https://www . geesforgeks . org/check-如果数组有一个等于所有剩余元素总和的元素/](https://www.geeksforgeeks.org/check-if-the-array-has-an-element-which-is-equal-to-sum-of-all-the-remaining-elements/)

给定一个由 N 个元素组成的数组，任务是检查该数组中是否有一个元素等于所有剩余元素的总和。
**例** :

```
Input: a[] = {5, 1, 2, 2}
Output: Yes
we can write 5=(1+2+2)

Input: a[] = {2, 1, 2, 4, 3}
Output: No
```

**逼近:**假设数组中的元素总数为 **N** 。现在，如果存在任何这样的元素，使得该元素等于剩余元素的和，那么可以说该数组可以被分成具有相等和的两半，使得一半只有一个具有值 sum/2 的元素。
此外，由于两半的和相等，因此数组的总和必须相等，我们知道:

*   奇数+奇数=偶数
*   偶数+偶数=偶数

**算法** :

*   遍历数组，统计所有元素的出现次数，并存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。同时对数组元素求和。
*   问题中给出的条件只有在满足以下条件时才有可能。
    1.  数组的总和是偶数
    2.  数组中出现的 sum/2 应该至少等于 1。
*   如果不满足上述条件，则不可能移除任何此类元素。

以下是上述方法的实现:

## C++

```
// C++ program to Check if the array
// has an element which is equal to sum
// of all the remaining elements

#include <bits/stdc++.h>
using namespace std;

// Function to check if such element exists or not
bool isExists(int a[], int n)
{
    // Storing frequency in map
    unordered_map<int, int> freq;

    // Stores the sum
    int sum = 0;

    // Traverse the array and count the
    // array elements
    for (int i = 0; i < n; i++) {
        freq[a[i]]++;
        sum += a[i];
    }

    // Only possible if sum is even
    if (sum % 2 == 0) {
        // If half sum is available
        if (freq[sum / 2])
            return true;
    }

    return false;
}

// Driver code
int main()
{
    int a[] = { 5, 1, 2, 2 };

    int n = sizeof(a) / sizeof(a[0]);

    if (isExists(a, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check if the array
// has an element which is equal to sum
// of all the remaining elements
import java.util.*;
class Solution{

// Function to check if such element exists or not
static boolean isExists(int a[], int n)
{
    // Storing frequency in map
    Map<Integer, Integer> freq= new HashMap<Integer, Integer>();

    // Stores the sum
    int sum = 0;

    // Traverse the array and count the
    // array elements
    for (int i = 0; i < n; i++) {
        freq.put(a[i],freq.get(a[i])==null?0:freq.get(a[i])+1);
        sum += a[i];
    }

    // Only possible if sum is even
    if (sum % 2 == 0) {
        // If half sum is available
        if (freq.get(sum / 2)!=null)
            return true;
    }

    return false;
}

// Driver code
public static void main(String args[])
{
    int a[] = { 5, 1, 2, 2 };

    int n = a.length;

    if (isExists(a, n))
        System.out.println( "Yes");
    else
        System.out.println( "No");

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 code to check if the array has
# an element which is equal to sum of all
# the remaining elements

# function to check if such element
# exists or not
def isExists(a, n):

    # storing frequency in dict
    freq = {i : 0 for i in a}

    #stores the sum
    Sum = 0

    # traverse the array and count
    # the array element
    for i in range(n):
        freq[a[i]] += 1
        Sum += a[i]

    # Only possible if sum is even
    if Sum % 2 == 0:

        #if half sum is available
        if freq[Sum // 2]:
            return True
    return False

# Driver code
a = [5, 1, 2, 2]

n = len(a)

if isExists(a, n):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to Check if the array
// has an element which is equal to sum
// of all the remaining elements
using System;
using System.Collections.Generic;

class Solution
{

// Function to check if such element exists or not
static Boolean isExists(int []arr, int n)
{
    // Storing frequency in map
    Dictionary<int, int> m = new Dictionary<int, int>();

    // Stores the sum
    int sum = 0;

    // Traverse the array and count the
    // array elements
    for (int i = 0; i < n; i++)
    {
        if(m.ContainsKey(arr[i]))
        {
            var val = m[arr[i]];
            m.Remove(arr[i]);
            m.Add(arr[i], val + 1);
        }
        else
        {
            m.Add(arr[i], 1);
        }
        sum += arr[i];
    }

    // Only possible if sum is even
    if (sum % 2 == 0)
    {
        // If half sum is available
        if (m[sum / 2] != 0)
            return true;
    }

    return false;
}

// Driver code
public static void Main()
{
    int []a = { 5, 1, 2, 2 };

    int n = a.Length;

    if (isExists(a, n))
        Console.WriteLine( "Yes");
    else
        Console.WriteLine( "No");
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to Check if the array
// has an element which is equal to sum
// of all the remaining elements

// Function to check if such element exists or not
function isExists(a, n)
{
    // Storing frequency in map
    let freq= new Map();

    // Stores the sum
    let sum = 0;

    // Traverse the array and count the
    // array elements
    for (let i = 0; i < n; i++) {
        freq.set(a[i],freq.get(a[i])==null?0:freq.get(a[i])+1);
        sum += a[i];
    }

    // Only possible if sum is even
    if (sum % 2 == 0) {
        // If half sum is available
        if (freq.get(sum / 2)!=null)
            return true;
    }

    return false;
}

// Driver Code

           let a = [ 5, 1, 2, 2 ];

    let n = a.length;

    if (isExists(a, n))
        document.write( "Yes");
    else
        document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N * log N)
**辅助空间:** O(N)
**另一种方法:**计算总计=数组中所有元素的总和。然后运行一个 FOR 循环来检查每个元素* 2 ==总数。如果找到任何这样的元素，返回真，否则在循环结束时返回假。时间复杂度= O(N)，空间复杂度= O(1)。