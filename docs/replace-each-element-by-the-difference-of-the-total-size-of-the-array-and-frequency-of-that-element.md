# 用数组的总大小和该元素的频率之差来替换每个元素

> 原文:[https://www . geeksforgeeks . org/用数组总大小和元素频率之差替换每个元素/](https://www.geeksforgeeks.org/replace-each-element-by-the-difference-of-the-total-size-of-the-array-and-frequency-of-that-element/)

给定一个整数数组，任务是用数组的总大小和它的频率之差来替换每个元素。

**示例:**

```
Input: arr[] = { 1, 2, 5, 2, 2, 5, 4 }
Output: 6 4 5 4 4 5 6
Size of the array is 7.
The frequency of 1 is 1\. So replace it by 7-1 = 6
The frequency of 2 is 3\. So replace it by 7-3 = 4

Input: arr[] = { 4, 5, 4, 5, 6, 6, 6 }
Output: 5 5 5 5 4 4 4
```

**进场:**

1.  取一个散列图，它将存储数组中所有元素的频率。
2.  现在，再次遍历。
3.  现在，用数组的总大小和它的频率之差来替换所有的元素。
4.  打印修改后的数组。

下面是上述方法的实现:

## C++

```
// C++ program to Replace each element
// by the difference of the total size
// of the array and its frequency
#include <bits/stdc++.h>
using namespace std;

// Function to replace the elements
void ReplaceElements(int arr[], int n)
{
    // Hash map which will store the
    // frequency of the elements of the array.
    unordered_map<int, int> mp;

    for (int i = 0; i < n; ++i)

        // Increment the frequency
        // of the element by 1.
        mp[arr[i]]++;

    // Replace every element by its frequency
    for (int i = 0; i < n; ++i)
        arr[i] = n - mp[arr[i]];

}

// Driver code
int main()
{
    int arr[] = { 1, 2, 5, 2, 2, 5, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    ReplaceElements(arr, n);

    // Print the modified array.
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Replace each element
// by the difference of the total size
// of the array and its frequency
import java.util.*;

class GFG
{

    // Function to replace the elements
    static void ReplaceElements(int arr[], int n)
    {
        // Hash map which will store the
        // frequency of the elements of the array.
        HashMap<Integer, Integer> mp = new HashMap<>();

        for (int i = 0; i < n; i++)
        {

            // Increment the frequency
            // of the element by 1.
            if (!mp.containsKey(arr[i]))
            {
                mp.put(arr[i], 1);
            }
            else
            {
                mp.put(arr[i], mp.get(arr[i]) + 1);
            }
        }

        // Replace every element by its frequency
        for (int i = 0; i < n; ++i)
        {
            arr[i] = n - mp.get(arr[i]);
        }

    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 5, 2, 2, 5, 4};
        int n = arr.length;

        ReplaceElements(arr, n);

        // Print the modified array.
        for (int i = 0; i < n; ++i)
        {
            System.out.print(arr[i] + " ");
        }
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to Replace each element
# by the difference of the total size
# of the array and its frequency

# Function to replace the elements
def ReplaceElements(arr, n):

    # Hash map which will store the
    # frequency of the elements of the array.
    mp = dict()

    for i in range(n):

        # Increment the frequency
        # of the element by 1.
        mp[arr[i]] = mp.get(arr[i], 0) + 1

    # Replace every element by its frequency
    for i in range(n):
        arr[i] = n - mp[arr[i]]

# Driver code
arr = [1, 2, 5, 2, 2, 5, 4]
n = len(arr)

ReplaceElements(arr, n)

# Print the modified array.
for i in range(n):
    print(arr[i], end = " ")

# This code is contributed by mohit kumar
```

## C#

```
// C# program to Replace each element
// by the difference of the total size
// of the array and its frequency
using System;
using System.Collections.Generic;

class GFG
{

    // Function to replace the elements
    static void ReplaceElements(int []arr, int n)
    {
        // Hash map which will store the
        // frequency of the elements of the array.
        Dictionary<int,int> mp = new Dictionary<int,int>();

        for (int i = 0; i < n; i++)
        {

            // Increment the frequency
            // of the element by 1.
            if (!mp.ContainsKey(arr[i]))
            {
                mp.Add(arr[i], 1);
            }
            else
            {
                var a = mp[arr[i]] + 1;
                mp.Remove(arr[i]);
                mp.Add(arr[i], a);
            }
        }

        // Replace every element by its frequency
        for (int i = 0; i < n; ++i)
        {
            arr[i] = n - mp[arr[i]];
        }

    }

    // Driver code
    public static void Main()
    {
        int []arr = {1, 2, 5, 2, 2, 5, 4};
        int n = arr.Length;

        ReplaceElements(arr, n);

        // Print the modified array.
        for (int i = 0; i < n; ++i)
        {
            Console.Write(arr[i] + " ");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to Replace each element
// by the difference of the total size
// of the array and its frequency

// Function to replace the elements
function ReplaceElements(arr, n)
{

    // Hash map which will store the
    // frequency of the elements of the array.
    let mp = new Map();

    for(let i = 0; i < n; i++)
    {

        // Increment the frequency
        // of the element by 1.
        if (!mp.has(arr[i]))
        {
            mp.set(arr[i], 1);
        }
        else
        {
            mp.set(arr[i], mp.get(arr[i]) + 1);
        }
    }

    // Replace every element by its frequency
    for(let i = 0; i < n; ++i)
    {
        arr[i] = n - mp.get(arr[i]);
    }
}

// Driver Code
let arr = [ 1, 2, 5, 2, 2, 5, 4 ];
let n = arr.length;

ReplaceElements(arr, n);

// Print the modified array.
for(let i = 0; i < n; ++i)
{
    document.write(arr[i] + " ");
}

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
6 4 5 4 4 5 6
```

**时间复杂度–**O(N)