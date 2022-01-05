# 检查给定数组的元素是否可能有对称加号

> 原文:[https://www . geesforgeks . org/check-if-a-symmetric-plus-is-on-the-elements-of-the-the-给定数组/](https://www.geeksforgeeks.org/check-if-a-symmetric-plus-is-possible-from-the-elements-of-the-given-array/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是检查给定数组的元素是否可能不对称加号。
正方形对称加号的形式是:

```
    Z
    Y
Z Y X Y Z
    Y
    Z
```

**注意**阵列的所有元素都必须用于形成正方形。

**示例:**

```
Input: arr[] = {1, 2, 1, 1, 1}
Output: Yes
   1
1  2  1
   1

Input: arr[] = {1, 1, 1, 1, 2, 2, 2, 3, 2}
Output: Yes
    1
    2
1 2 3 2 1
    2
    1

Input: arr[] = {1, 1, 1, 4, 2, 2, 2, 3, 2}
Output: No 
```

**方法:**为了形成非对称加号，数组中所有元素的频率必须是 4 的倍数，并且必须有一个元素在与 4 取模时其频率为 1。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that return true if
// a symmetric is possible with
// the elements of the array
bool isPlusPossible(int arr[], int n)
{

    // Map to store the frequency
    // of the array elements
    unordered_map<int, int> mp;

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    bool foundModOne = false;

    // For every unique element
    for (auto x : mp) {
        int element = x.first;
        int frequency = x.second;

        if (frequency % 4 == 0)
            continue;
        if (frequency % 4 == 1) {

            // Element has already been found
            if (foundModOne)
                return false;
            foundModOne = true;
        }

        // The frequency of the element
        // something other than 0 and 1
        else
            return false;
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 1, 1, 2, 2, 2, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (isPlusPossible(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that return true if
// a symmetric is possible with
// the elements of the array
static boolean isPlusPossible(int arr[], int n)
{

    // Map to store the frequency
    // of the array elements
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++)
    {
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }

    boolean foundModOne = false;

    // For every unique element
    for (Map.Entry<Integer,Integer> x : mp.entrySet())
    {
        int element = x.getKey();
        int frequency = x.getValue();

        if (frequency % 4 == 0)
            continue;
        if (frequency % 4 == 1)
        {

            // Element has already been found
            if (foundModOne)
                return false;
            foundModOne = true;
        }

        // The frequency of the element
        // something other than 0 and 1
        else
            return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 1, 1, 2, 2, 2, 3, 2 };
    int n = arr.length;

    if (isPlusPossible(arr, n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that return true if
# a symmetric is possible with
# the elements of the array
def isPlusPossible(arr, n):

    # Map to store the frequency
    # of the array elements
    mp = dict()

    # Traverse through array elements and
    # count frequencies
    for i in range(n):
        mp[arr[i]] = mp.get(arr[i], 0) + 1

    foundModOne = False

    # For every unique element
    for x in mp:
        element = x
        frequency = mp[x]

        if (frequency % 4 == 0):
            continue
        if (frequency % 4 == 1):

            # Element has already been found
            if (foundModOne == True):
                return False
            foundModOne = True

        # The frequency of the element
        # something other than 0 and 1
        else:
            return False
    return True   

# Driver code
arr = [1, 1, 1, 1, 2, 2, 2, 3, 2]
n = len(arr)

if (isPlusPossible(arr, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that return true if
// a symmetric is possible with
// the elements of the array
static bool isPlusPossible(int []arr,
                           int n)
{

    // Map to store the frequency
    // of the array elements
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse through array elements and
    // count frequencies
    for (int i = 0; i < n; i++)
    {
        if(mp.ContainsKey(arr[i]))
        {
            mp[arr[i]] = mp[arr[i]] + 1;
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    bool foundModOne = false;

    // For every unique element
    foreach(KeyValuePair<int, int> x in mp)
    {
        int element = x.Key;
        int frequency = x.Value;

        if (frequency % 4 == 0)
            continue;
        if (frequency % 4 == 1)
        {

            // Element has already been found
            if (foundModOne)
                return false;
            foundModOne = true;
        }

        // The frequency of the element
        // something other than 0 and 1
        else
            return false;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 1, 1, 2, 2, 2, 3, 2 };
    int n = arr.Length;

    if (isPlusPossible(arr, n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that return true if
// a symmetric is possible with
// the elements of the array
function isPlusPossible(arr, n)
{

    // Map to store the frequency
    // of the array elements
    var mp = new Map();

    // Traverse through array elements and
    // count frequencies
    for (var i = 0; i < n; i++)
    {
        if(mp.has(arr[i]))
            mp.set(arr[i], mp.get(arr[i])+1)
        else
            mp.set(arr[i], 1)
    }

    var foundModOne = false;
    var ans = true;

    // For every unique element
    mp.forEach((value, key) => {

        var element = key;
        var frequency = value;

        if (frequency % 4 != 0)
        {
        if (frequency % 4 == 1) {

            // Element has already been found
            if (foundModOne)
                ans = false
            foundModOne = true;
        }

        // The frequency of the element
        // something other than 0 and 1
        else
            ans = false
        }
    });
    return ans;
}

// Driver code
var arr = [1, 1, 1, 1, 2, 2, 2, 3, 2];
var n = arr.length;
if (isPlusPossible(arr, n))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```