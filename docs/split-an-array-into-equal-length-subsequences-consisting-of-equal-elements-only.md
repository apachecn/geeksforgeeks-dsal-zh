# 将一个数组分割成仅由相等元素组成的等长子序列

> 原文:[https://www . geeksforgeeks . org/将数组拆分为长度相等的子序列-仅由相等的元素组成/](https://www.geeksforgeeks.org/split-an-array-into-equal-length-subsequences-consisting-of-equal-elements-only/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是检查是否有可能将数组 **arr[]** 分割成大小相等的不同子序列，使得子序列的每个元素相等。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {1，2，3，4，4，3，2，1}
> **输出:** YES
> **解释:**可能的分区:{1，1}、{2，2}、{3，3}、{4，4}。
> 
> **输入:** arr[] = {1，1，1，2，2，2，3，3}
> **输出:**否

**方法:**思路基于以下观察:让**arr【I】**的频率为 **C <sub>i</sub>** ，那么这些元素必须分解为 **X** 的子序列，使得 **C <sub>i</sub> % X = 0** 。对于每个索引 **i** ，该值必须为是。为此， **X** 的值应等于所有 **C <sub>i</sub> (1≤i≤N)** 的[最大公约数(GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) )。如果 **X** 大于 1，则打印是，否则打印否

按照以下步骤解决问题:

*   创建一个[散列表](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)、 **mp** ，以[存储数组所有元素的频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)、 **arr[]** 。
*   将**MP**T3 中所有频率的[最大公约数存储在变量 **X** 中。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)
*   如果 **X** 大于 1，那么答案是肯定的。
*   否则，答案是否定的。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the GCD
// of two numbers a and b
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to check if it is possible to
// split the array into equal length subsequences
// such that all elements in the subsequence are equal
void splitArray(int arr[], int N)
{

    // Store frequencies of
    // array elements
    map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency of arr[i]
        mp[arr[i]]++;
    }

    // Store the GCD of frequencies
    // of all array elements
    int G = 0;

    // Traverse the map
    for (auto i : mp) {

        // Update GCD
        G = gcd(G, i.second);
    }

    // If the GCD is greater than 1,
    // print YES otherwise print NO
    if (G > 1)
        cout << "YES";
    else
        cout << "NO";
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 2, 3, 4, 4, 3, 2, 1 };

    // Store the size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    splitArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG
{

    // Function to find the GCD
    // of two numbers a and b
    int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to check if it is possible to
    // split the array into equal length subsequences
    // such that all elements in the subsequence are equal
    void splitArray(int arr[], int N)
    {

        // Store frequencies of
        // array elements
        TreeMap<Integer, Integer> mp
            = new TreeMap<Integer, Integer>();

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // Update frequency of arr[i]
            if (mp.containsKey(arr[i]))
            {
                mp.put(arr[i], mp.get(arr[i]) + 1);
            }
            else
            {
                mp.put(arr[i], 1);
            }
        }

        // Store the GCD of frequencies
        // of all array elements
        int G = 0;

        // Traverse the map
        for (Map.Entry<Integer, Integer> m :
             mp.entrySet())
        {

            // update gcd
            Integer i = m.getValue();
            G = gcd(G, i.intValue());
        }

        // If the GCD is greater than 1,
        // print YES otherwise print NO
        if (G > 1)
            System.out.print("YES");
        else
            System.out.print("NO");
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array
        int[] arr = new int[] { 1, 2, 3, 4, 4, 3, 2, 1 };

        // Store the size of the array
        int n = arr.length;
        new GFG().splitArray(arr, n);
    }
}

// This code is contributed by abhishekgiri1
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to find the GCD
# of two numbers a and b
def gcd(a, b):

    if (b == 0):
        return a

    return gcd(b, a % b)

# Function to check if it is possible
# to split the array into equal length
# subsequences such that all elements
# in the subsequence are equal
def splitArray(arr, N):

    # Store frequencies of
    # array elements
    mp = defaultdict(int)

    # Traverse the array
    for i in range(N):

        # Update frequency of arr[i]
        mp[arr[i]] += 1

    # Store the GCD of frequencies
    # of all array elements
    G = 0

    # Traverse the map
    for i in mp:

        # Update GCD
        G = gcd(G, mp[i])

    # If the GCD is greater than 1,
    # print YES otherwise print NO
    if (G > 1):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [ 1, 2, 3, 4, 4, 3, 2, 1 ]

    # Store the size of the array
    n = len(arr)

    splitArray(arr, n)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;
class GFG{

// Function to find the GCD
// of two numbers a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to check if it is possible to
// split the array into equal length subsequences
// such that all elements in the subsequence are equal
static void splitArray(int[] arr, int n)
{

    // Store frequencies of
    // array elements
    Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>();

    // Traverse the array
    for(int i = 0; i < n; ++i)
    {

        // Update frequency of
        // each array element
        if (mp.ContainsKey(arr[i]) == true)
        mp[arr[i]] += 1;
      else
        mp[arr[i]] = 1;
    }

    // Store the GCD of frequencies
    // of all array elements
    int G = 0;

    // Traverse the map
    foreach (KeyValuePair<int, int> i in mp)
    {

        // Update GCD
        G = gcd(G, i.Value);
    }

    // If the GCD is greater than 1,
    // print YES otherwise print NO
    if (G > 1)
        Console.Write("YES");
    else
        Console.Write("NO");
}

// Driver Code
public static void Main()
{

    // Given array
    int[] arr = { 1, 2, 3, 4, 4, 3, 2, 1 };

    // Store the size of the array
    int n = arr.Length;
    splitArray(arr, n);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the GCD
// of two numbers a and b
function gcd(a, b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to check if it is
// possible to split the array
// into equal length subsequences
// such that all elements in the
// subsequence are equal
function splitArray(arr, N)
{

    // Store frequencies of
    // array elements
    var mp = new Map();

    // Traverse the array
    for(var i = 0; i < N; i++)
    {

        // Update frequency of arr[i]
        if (mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    // Store the GCD of frequencies
    // of all array elements
    var G = 0;

    // Traverse the map
    mp.forEach((value, key) => {

        // Update GCD
        G = gcd(G, value);
    });

    // If the GCD is greater than 1,
    // print YES otherwise print NO
    if (G > 1)
        document.write("YES");
    else
        document.write("NO");
}

// Driver Code

// Given array
var arr = [ 1, 2, 3, 4, 4, 3, 2, 1 ];

// Store the size of the array
var n = arr.length;
splitArray(arr, n);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*