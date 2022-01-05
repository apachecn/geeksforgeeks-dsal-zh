# 检查是否有任何子阵列可以通过替换少于一半的元素而成为回文

> 原文:[https://www . geesforgeks . org/check-if-any-subarray-可以通过替换少于一半的元素来制作回文/](https://www.geeksforgeeks.org/check-if-any-subarray-can-be-made-palindromic-by-replacing-less-than-half-of-its-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过用子数组的任何其他元素替换少于一半的元素(即**地板**【长度/2】)来检查给定数组中的任何子数组是否可以成为[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。

**示例:**

> **输入:** arr[] = {2，7，4，6，7，8}
> **输出:**是
> **说明:**在这个阵列的所有子阵中，子阵{7，4，6，7}只需要 1 次运算就可以使其成为回文，即以 4 替换 arr[3]或以 6 替换 arr[4]，这比 floor(4/2) ( = 2)要少。
> 
> **输入:** arr[] = {3，7，19，6}
> **输出:**否

**天真方法:**解决这个问题最简单的方法是[生成给定阵列的所有子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵列，检查使该子阵列成为回文所需的替换次数是否小于**地板(子阵列长度/ 2)** 。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 如果数组 **arr[]** 包含重复的元素，那么总是有可能从该元素的初始出现到下一次出现选择一个子数组。由于子阵列的第一个和最后一个元素已经相等，因此该子阵列将需要小于地板(长度/2)的操作。

按照以下步骤解决问题:

*   初始化一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，用于存储每个阵元的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [迭代所有数组元素](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[计算每个数组元素](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)和[的频率，并将其插入到地图](https://www.geeksforgeeks.org/map-insert-in-c-stl/)中。
*   检查是否发现任何数组元素的频率大于 1..如果发现是真的，打印**“是”**。否则，打印**“否”**。

下面是该方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// A Utility Function to check if a subarray
// can be palindromic by replacing less than
// half of the elements present in it
bool isConsistingSubarrayUtil(int arr[], int n)
{
    // Stores frequency of array elements
    map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < n; ++i) {

        // Update frequency of
        // each array element
        mp[arr[i]]++;
    }

    // Iterator over the Map
    map<int, int>::iterator it;

    for (it = mp.begin(); it != mp.end(); ++it) {

        // If frequency of any element exceeds 1
        if (it->second > 1) {
            return true;
        }
    }

    // If no repetition is found
    return false;
}

// Function to check and print if any subarray
// can be made palindromic by replacing less
// than half of its elements
void isConsistingSubarray(int arr[], int N)
{
    if (isConsistingSubarrayUtil(arr, N)) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5, 1 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    isConsistingSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// A Utility Function to check if a subarray
// can be palindromic by replacing less than
// half of the elements present in it
static boolean isConsistingSubarrayUtil(int arr[],
                                        int n)
{

    // Stores frequency of array elements
    TreeMap<Integer,
            Integer> mp = new TreeMap<Integer,
                                      Integer>();

    // Traverse the array
    for(int i = 0; i < n; ++i)
    {

        // Update frequency of
        // each array element
        mp.put(arr[i],
        mp.getOrDefault(arr[i], 0) + 1);
    }

    for(Map.Entry<Integer,
                  Integer> it : mp.entrySet())
    {

        // If frequency of any element exceeds 1
        if (it.getValue() > 1)
        {
            return true;
        }
    }

    // If no repetition is found
    return false;
}

// Function to check and print if any subarray
// can be made palindromic by replacing less
// than half of its elements
static void isConsistingSubarray(int arr[], int N)
{
    if (isConsistingSubarrayUtil(arr, N))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}

// Driver Code
public static void main(String args[])
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5, 1 };

    // Size of array
    int N = arr.length;

    // Function Call
    isConsistingSubarray(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# A Utility Function to check if a subarray
# can be palindromic by replacing less than
# half of the elements present in it
def isConsistingSubarrayUtil(arr, n) :

    # Stores frequency of array elements
    mp = {};

    # Traverse the array
    for i in range(n) :

        # Update frequency of
        # each array element
        if arr[i] in mp :
            mp[arr[i]] += 1;           
        else :
            mp[arr[i]] = 1;

    # Iterator over the Map
    for it in mp :

        # If frequency of any element exceeds 1
        if (mp[it] > 1) :
            return True;

    # If no repetition is found
    return False;

# Function to check and print if any subarray
# can be made palindromic by replacing less
# than half of its elements
def isConsistingSubarray(arr, N) :

    if (isConsistingSubarrayUtil(arr, N)) :
        print("Yes");
    else :
        print("No");

# Driver Code
if __name__ == "__main__" :

    # Given array arr[]
    arr = [ 1, 2, 3, 4, 5, 1 ];

    # Size of array
    N = len(arr);

    # Function Call
    isConsistingSubarray(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

// A Utility Function to check if a subarray
// can be palindromic by replacing less than
// half of the elements present in it
static bool isConsistingSubarrayUtil(int[] arr,
                                        int n)
{

    // Stores frequency of array elements
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

    var val = mp.Keys.ToList();
    foreach(var key in val)
    {
        // If frequency of any element exceeds 1
        if (mp[key] > 1)
        {
            return true;
        }
    }

    // If no repetition is found
    return false;
}

// Function to check and print if any subarray
// can be made palindromic by replacing less
// than half of its elements
static void isConsistingSubarray(int[] arr, int N)
{
    if (isConsistingSubarrayUtil(arr, N))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}

// Driver Code
public static void Main()
{
    // Given array arr[]
    int[] arr = { 1, 2, 3, 4, 5, 1 };

    // Size of array
    int N = arr.Length;

    // Function Call
    isConsistingSubarray(arr, N);
}
}

// This code is contributed by sanjoy62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// A Utility Function to check if a subarray
// can be palindromic by replacing less than
// half of the elements present in it
function isConsistingSubarrayUtil(arr, n)
{
    // Stores frequency of array elements
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < n; ++i) {

        // Update frequency of
        // each array element
        if(mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i])+1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    var ans = false;
    // Iterator over the Map
    mp.forEach((value, key) => {

        // If frequency of any element exceeds 1
        if (value > 1) {
            ans = true;
        }
    });

    if(ans)
        return true;

    // If no repetition is found
    return false;
}

// Function to check and print if any subarray
// can be made palindromic by replacing less
// than half of its elements
function isConsistingSubarray(arr, N)
{
    if (isConsistingSubarrayUtil(arr, N)) {
        document.write( "Yes");
    }
    else {
        document.write( "No" );
    }
}

// Driver Code
// Given array arr[]
var arr = [1, 2, 3, 4, 5, 1];
// Size of array
var N = arr.length;
// Function Call
isConsistingSubarray(arr, N);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)