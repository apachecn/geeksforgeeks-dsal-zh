# 检查是否有可能对距离为 K 的元素进行条件交换的数组进行排序

> 原文:[https://www . geeksforgeeks . org/check-如果有可能用条件交换距离为 k 的元素对数组进行排序/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-sort-an-array-with-conditional-swapping-of-elements-at-distance-k/)

给定一个由 n 个元素组成的**数组 arr[]** ，我们必须**将一个索引 i** 与另一个索引 **i + k** 交换任意多次，并检查是否有可能对给定数组 arr[]。如果是，则打印“是”，否则打印“否”。
**示例:**

> **输入:** K = 2，arr = [4，3，2，6，7]
> **输出:**是
> **解释:**
> 选择索引 i = 0，用 i + k 交换索引 I，然后数组变成[2，3，4，6，7]，排序后输出为“是”。
> **输入:** K = 2，arr = [4，2，3，7，6]
> **输出:**否
> **说明:**
> 不可能得到排序数组。

**方法:**
要解决上面提到的问题，我们要从索引 0 开始取元素，加上 K 的倍数，就是 0，0 + k，0 + (2*k)等等。将这些位置交换为从 0 到 K-1 的所有索引，并检查最终数组是否已排序。如果是，则返回“是”，否则返回“否”。
以下是上述办法的实施:

## C++

```
// CPP implementation to Check if it is possible to sort an
// array with conditional swapping of elements at distance K
#include <bits/stdc++.h>
using namespace std;

// Function for finding if it possible
// to obtain sorted array or not
bool fun(int arr[], int n, int k)
{
    vector<int> v;

    // Iterate over all elements until K
    for (int i = 0; i < k; i++) {
        // Store elements as multiples of K
        for (int j = i; j < n; j += k) {
            v.push_back(arr[j]);
        }

        // Sort the elements
        sort(v.begin(), v.end());

        int x = 0;

        // Put elements in their required position
        for (int j = i; j < n; j += k) {
            arr[j] = v[x];
            x++;
        }

        v.clear();
    }

    // Check if the array becomes sorted or not
    for (int i = 0; i < n - 1; i++) {
        if (arr[i] > arr[i + 1])
            return false;
    }
    return true;
}

// Driver code
int main()
{
    int arr[] = { 4, 2, 3, 7, 6 };

    int K = 2;

    int n = sizeof(arr) / sizeof(arr[0]);

    if (fun(arr, n, K))
        cout << "yes" << endl;

    else
        cout << "no" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if it
// is possible to sort an array with
// conditional swapping of elements
// at distance K
import java.lang.*;
import java.io.*;
import java.util.*;

class GFG{

// Function for finding if it possible
// to obtain sorted array or not    
public static boolean fun(int[] arr, int n,
                                     int k)
{
    Vector<Integer> v = new Vector<Integer>();

    // Iterate over all elements until K
    for(int i = 0; i < k; i++)
    {

       // Store elements as multiples of K
       for(int j = i; j < n; j += k)
       {
          v.add(arr[j]);
       }

       // Sort the elements
       Collections.sort(v);

       int x = 0;

       // Put elements in their
       // required position
       for(int j = i; j < n; j += k)
       {
          arr[j] = v.get(x);
          x++;
       }
       v.clear();
    }

    // Check if the array becomes
    // sorted or not
    for(int i = 0; i < n - 1; i++)
    {
       if (arr[i] > arr[i + 1])
       {
           return false;
       }
    }
    return true;
}

// Driver code
public static void main (String args[])
{
    int[] arr = { 4, 2, 3, 7, 6 };
    int K = 2;
    int n = arr.length;

    if (fun(arr, n, K))
    {
        System.out.println("yes");
    }
    else
    {
        System.out.println("no");
    }
}
}

// This code is contributed by sayesha
```

## 蟒蛇 3

```
# Python3 implementation to Check if it is possible to sort an
# array with conditional swapping of elements at distance K

# Function for finding if it possible
# to obtain sorted array or not
def fun(arr, n, k):

    v = []

    # Iterate over all elements until K
    for i in range(k):

        # Store elements as multiples of K
        for j in range(i, n, k):
            v.append(arr[j]);

        # Sort the elements
        v.sort();

        x = 0

        # Put elements in their required position
        for j in range(i, n, k):
            arr[j] = v[x];
            x += 1

        v = []

    # Check if the array becomes sorted or not
    for i in range(n - 1):
        if (arr[i] > arr[i + 1]):
            return False
    return True

# Driver code
arr= [ 4, 2, 3, 7, 6 ]

K = 2;

n = len(arr)

if (fun(arr, n, K)):
    print("yes")
else:
    print("no")

# This code is contributed by apurva raj
```

## C#

```
// C# implementation to check if it
// is possible to sort an array with
// conditional swapping of elements
// at distance K
using System;
using System.Collections.Generic;
class GFG{

// Function for finding if it possible
// to obtain sorted array or not    
public static bool fun(int[] arr,
                       int n, int k)
{
    List<int> v = new List<int>();

    // Iterate over all elements until K
    for(int i = 0; i < k; i++)
    {      
       // Store elements as multiples of K
       for(int j = i; j < n; j += k)
       {
          v.Add(arr[j]);
       }

       // Sort the elements
       v.Sort();

       int x = 0;

       // Put elements in their
       // required position
       for(int j = i; j < n; j += k)
       {
          arr[j] = v[x];
          x++;
       }
       v.Clear();
    }

    // Check if the array becomes
    // sorted or not
    for(int i = 0; i < n - 1; i++)
    {
       if (arr[i] > arr[i + 1])
       {
           return false;
       }
    }
    return true;
}

// Driver code
public static void Main(String []args)
{
    int[] arr = {4, 2, 3, 7, 6};
    int K = 2;
    int n = arr.Length;
    if (fun(arr, n, K))
    {
        Console.WriteLine("yes");
    }
    else
    {
        Console.WriteLine("no");
    }
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript implementation to
// Check if it is possible to sort an
// array with conditional swapping of
// elements at distance K

// Function for finding if it possible
// to obtain sorted array or not
function fun(arr, n, k)
{
    let v = [];

    // Iterate over all elements until K
    for (let i = 0; i < k; i++) {
        // Store elements as multiples of K
        for (let j = i; j < n; j += k) {
            v.push(arr[j]);
        }

        // Sort the elements
        v.sort();

        let x = 0;

        // Put elements in their required position
        for (let j = i; j < n; j += k) {
            arr[j] = v[x];
            x++;
        }

        v = [];
    }

    // Check if the array becomes sorted or not
    for (let i = 0; i < n - 1; i++) {
        if (arr[i] > arr[i + 1])
            return false;
    }
    return true;
}

// Driver code
    let arr = [ 4, 2, 3, 7, 6 ];

    let K = 2;

    let n = arr.length;

    if (fun(arr, n, K))
        document.write("yes");

    else
        document.write("no");

</script>
```

**Output:** 

```
no
```