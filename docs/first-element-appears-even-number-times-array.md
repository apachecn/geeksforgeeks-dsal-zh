# 数组中出现偶数次的第一个元素

> 原文:[https://www . geesforgeks . org/first-element-appears-偶数-次数-array/](https://www.geeksforgeeks.org/first-element-appears-even-number-times-array/)

给定一个数组，找到数组中出现偶数次的第一个元素。如果存在，则返回元素，否则返回 0。
**例:**

> 输入:arr[] = {1，5，4，7，4，1，5，7，1，5 }；
> 输出:4
> 说明，4 是第一个出现偶数次的元素。
> 输入:arr[] = {2，4，6，8，1，6 }；
> 输出:6
> 说明，6 是第一个出现偶数次的元素

一个**简单的解决方案**就是把每一个元素都一一考虑。对于每个元素，开始计数频率，计数为偶数的第一个元素给出结果。该解决方案的时间复杂度为 0(n![^{2}   ](img/f21bfc0260630c03cee11d3fc69eca20.png "Rendered by QuickLaTeX.com"))。
一个**高效的解决方案**可以使用具有 0(n)个时间和 0(n)个额外空间的哈希映射来解决这个问题，如:

*   如果哈希映射中不存在[i]，将其作为对插入哈希映射(a[i]，false)。
*   如果哈希映射中存在[i]，并且值为真，则将它切换为假。
*   如果散列图中有一个[i],并且值为 false，则将它切换为 true。

## C++

```
// C++ code to find the first element
// that appears even number times
#include <bits/stdc++.h>
using namespace std;
int firstEven(int arr[], int n)
{

    unordered_map<int, bool> map1;

    for (int i = 0; i < n; i++)
    {

        // first time occurred
        if (map1.find(arr[i]) == map1.end())
            map1.insert(pair <int,bool> (arr[i],false));

        // toggle for repeated occurrence
        else
        {
            bool val = map1.find(arr[i])->second;
            if (val == true)
                map1.find(arr[i])->second = false;
            else
                map1.find(arr[i])->second = true;
        }
    }

    int j = 0;
    for (j = 0; j < n; j++)
    {

        // first integer with true value
        if (map1.find(arr[j])->second == true)
            break;
    }

    return arr[j];
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6, 8, 1, 6 };
    cout << firstEven(arr, 6);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code to find the first element
// that appears even number times
import java.util.*;
class GFG {
    public static int firstEven(int arr[], int n)
    {

        HashMap<Integer, Boolean> map =
                 new HashMap<Integer, Boolean>();

        for (int i = 0; i < n; i++) {

            // first time occurred
            if (map.get(arr[i]) == null)
                map.put(arr[i], false);

            // toggle for repeated occurrence
            else {
                boolean val = map.get(arr[i]);
                if (val == true)
                    map.put(arr[i], false);
                else
                    map.put(arr[i], true);
            }
        }

        int j = 0;
        for (j = 0; j < n; j++) {

            // first integer with true value
            if (map.get(arr[j]) == true)
                break;
        }

        return arr[j];
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 4, 6, 8, 1, 6 };
        int n = arr.length;
        System.out.println(firstEven(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 code to find the first element
# that appears even number times
def firstEven(arr, n):

    map1 = {}
    for i in range(0, n):

        # first time occurred
        if arr[i] not in map1:
            map1[arr[i]] = False

        # toggle for repeated occurrence
        else:
            map1[arr[i]] = not map1[arr[i]]

    for j in range(0, n):

        # first integer with true value
        if map1[arr[j]] == True:
            break

    return arr[j]

# Driver code
if __name__ == "__main__":

    arr = [2, 4, 6, 8, 1, 6]
    print(firstEven(arr, 6))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# code to find the first element
// that appears even number times
using System;
using System.Collections.Generic;

class GFG
{
    static int firstEven(int []arr,
                         int n)
    {
        var map = new Dictionary<int,
                                 string>();

        var hash = new HashSet<int>(arr);

        foreach (int a in hash)
            map.Add(a, "null");

        for (int i = 0; i < n; i++)
        {

            // first time occurred
            if (map[arr[i]].Equals("null"))
                map[arr[i]] = "false";

            // toggle for repeated
            // occurrence
            else
            {
                string val = map[arr[i]];
                if (val.Equals("true"))
                    map[arr[i]] = "false";
                else
                    map[arr[i]] = "true";
            }
        }

        int j = 0;
        for (j = 0; j < n; j++)
        {

            // first integer with
            // true value
            if (map[arr[j]].Equals("true"))
                break;
        }
        return arr[j];
    }

    // Driver code
    static void Main()
    {
        int []arr = new int[]{ 2, 4, 6,
                               8, 1, 6 };
        int n = arr.Length;
        Console.Write(firstEven(arr, n));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>
// Javascript code to find the first element
// that appears even number times

function firstEven(arr, n)
{

    let map1 = new Map();

    for (let i = 0; i < n; i++)
    {

        // first time occurred
        if (!map1.has(arr[i]))
            map1.set(arr[i],false);

        // toggle for repeated occurrence
        else
        {
            let val = map1.get(arr[i]);
            if (val == true)
                map1.set(arr[i], false);
            else
                map1.set(arr[i], true);
        }
    }

    let j = 0;
    for (j = 0; j < n; j++)
    {

        // first integer with true value
        if (map1.get(arr[j]) == true)
            break;
    }

    return arr[j];
}

// Driver code

    let arr = [ 2, 4, 6, 8, 1, 6 ];
    document.write(firstEven(arr, 6));

    // This code is contributed by gfgking.
</script>
```

**Output:** 

```
6
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)