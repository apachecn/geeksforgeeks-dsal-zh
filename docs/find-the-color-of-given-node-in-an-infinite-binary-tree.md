# 在无限二叉树中找到给定节点的颜色

> 原文:[https://www . geesforgeks . org/find-无限二叉树中给定节点的颜色/](https://www.geeksforgeeks.org/find-the-color-of-given-node-in-an-infinite-binary-tree/)

给定一个无限长的二叉树，其模式如下:

```
                      1
                    /   \
                  2       3
                /  \     /   \ 
               4    5   6     7
             /  \  / \ / \   / \
            ......................
```

也给了一个数组 **arr** 大小 **N** 和一个数字 **K** 。任务是用颜色 i (1 < = i < = N)一个接一个地给节点 arr[i]的所有子树着色。给所有子树着色后，找到节点 **K** 的颜色。

**注意:-** 最初所有节点颜色为 0。

> **输入:** arr[] = {3，2，1，3}，K = 7
> **输出:** 4
> **解释:**
> 将颜色 1 应用到节点 3 的子树后，节点 7 包含颜色 1。
> 将颜色 2 应用到节点 2 的子树后，节点 7 包含颜色 1。
> 将颜色 3 应用到节点 1 的子树后，节点 7 包含颜色 3。
> 将颜色 4 应用到节点 3 的子树后，节点 7 包含颜色 4。
> 
> **输入:** arr[] = {3，2，1，3}，K = 4
> **输出:** 3
> **解释:**
> 将颜色 1 应用到节点 3 的子树后，节点 4 包含颜色 0。
> 将颜色 2 应用到节点 2 的子树后，节点 4 包含颜色 2。
> 将颜色 3 应用到节点 1 的子树后，节点 4 包含颜色 3。
> 将颜色 4 应用到节点 3 的子树后，节点 4 包含颜色 3。

一种**天真的方法**是对于每个索引 i (1 < = i < = N)更新子树中所有节点的颜色，直到节点的级别小于给定节点 k 的级别。在 N 次这样的操作之后，打印节点 k 的颜色

一种有效的方法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)

*   首先，在地图中插入所有具有各自颜色的节点(在这种情况下，如果一个节点有多个颜色，则保留一个具有最大颜色数的节点)。
*   找到给定节点 k 的所有祖先，并输出具有最大数量的颜色。(如果当前节点为 **x** ，则 **(x-1)/2** 或 **x/2** 为其祖先)

下面是上述方法的实现:

## C++

```
// CPP program to find color of the node
#include <bits/stdc++.h>
using namespace std;

// Function to find color of the node
int findColor(map<int, int> mapWithColor, int query)
{
    // Maximum is to store maximum color
    int maximum = 0;

    // Loop to check all the parent
    // values to get maximum color
    while (query >= 1) {

        // Find the number into map and get maximum color
        if (mapWithColor.find(query) != mapWithColor.end())
        {
            // Take the maximum color and
            // assign into maximum variable
            maximum = max(maximum, mapWithColor[query]);
        }

        // Find parent index
        if (query % 2 == 1)
            query = (query - 1) / 2;
        else
            query = query / 2;
    }

    // Return maximum color
    return maximum;
}

// Function to build hash map with color
map<int, int> buildMapWithColor(int arr[], int n)
{
    // To store color of each node
    map<int, int> mapWithColor;

    // For each number add a color number
    for (int i = 0; i < n; i++) {
        // Assigning color
        mapWithColor[arr[i]] = i + 1;
    }

    // Return hash map
    return mapWithColor;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 1, 3 };

    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 7;

    // Build mapWithColor
    map<int, int> mapWithColor = buildMapWithColor(arr, n);

    // Print the maximum color
    cout << findColor(mapWithColor, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find color of the node
import java.util.*;

class GFG
{

    // Function to find color of the node
    static int findColor(HashMap<Integer, Integer> mapWithColor, int query)
    {
        // Maximum is to store maximum color
        int maximum = 0;

        // Loop to check all the parent
        // values to get maximum color
        while (query >= 1)
        {

            // Find the number into map and get maximum color
            if (mapWithColor.containsKey(query))
            {
                // Take the maximum color and
                // assign into maximum variable
                maximum = Math.max(maximum, mapWithColor.get(query));
            }

            // Find parent index
            if (query % 2 == 1)
                query = (query - 1) / 2;
            else
                query = query / 2;
        }

        // Return maximum color
        return maximum;
    }

    // Function to build hash map with color
    static HashMap<Integer, Integer> buildMapWithColor(int arr[], int n)
    {
        // To store color of each node
        HashMap<Integer, Integer> mapWithColor = new HashMap<Integer, Integer>();

        // For each number add a color number
        for (int i = 0; i < n; i++)
        {
            // Assigning color
            mapWithColor.put(arr[i], i + 1);
        }

        // Return hash map
        return mapWithColor;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 3, 2, 1, 3 };

        int n = arr.length;

        int k = 7;

        // Build mapWithColor
        HashMap<Integer, Integer> mapWithColor = buildMapWithColor(arr, n);

        // Print the maximum color
        System.out.print(findColor(mapWithColor, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 code program to find color of the node

# Function to find color of the node
def findColor(mapWithColor, query):

    # Maximum is to store maximum color
    maximum = 0

    # Loop to check all the parent
    # values to get maximum color
    while (query >= 1):

        # Find the number into map and get maximum color
        if (query) in mapWithColor.keys():
            # Take the maximum color and
            # assign into maximum variable
            maximum = max(maximum, mapWithColor[query])

        # Find parent index
        if (query % 2 == 1):
            query = (query - 1) // 2
        else:
            query = query // 2

    # Return maximum color
    return maximum

# Function to build hash map with color
def buildMapWithColor(arr, n):
    # To store color of each node
    mapWithColor={}

    # For each number add a color number
    for i in range(n):
        # Assigning color
        mapWithColor[arr[i]] = i + 1

    # Return hash map
    return mapWithColor

# Driver code

arr = [3, 2, 1, 3]

n = len(arr)

k = 7

# Build mapWithColor
mapWithColor = buildMapWithColor(arr, n)

# Print the maximum color
print(findColor(mapWithColor, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find color of the node
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find color of the node
    static int findColor(Dictionary<int, int> mapWithColor, int query)
    {
        // Maximum is to store maximum color
        int maximum = 0;

        // Loop to check all the parent
        // values to get maximum color
        while (query >= 1)
        {

            // Find the number into map and get maximum color
            if (mapWithColor.ContainsKey(query))
            {
                // Take the maximum color and
                // assign into maximum variable
                maximum = Math.Max(maximum, mapWithColor[query]);
            }

            // Find parent index
            if (query % 2 == 1)
                query = (query - 1) / 2;
            else
                query = query / 2;
        }

        // Return maximum color
        return maximum;
    }

    // Function to build hash map with color
    static Dictionary<int, int> buildMapWithColor(int []arr, int n)
    {
        // To store color of each node
        Dictionary<int, int> mapWithColor = new Dictionary<int, int>();

        // For each number add a color number
        for (int i = 0; i < n; i++)
        {
            // Assigning color
            if(mapWithColor.ContainsKey(arr[i]))
                mapWithColor[arr[i]] = i + 1;
            else
                mapWithColor.Add(arr[i], i + 1);
        }

        // Return hash map
        return mapWithColor;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 3, 2, 1, 3 };

        int n = arr.Length;

        int k = 7;

        // Build mapWithColor
        Dictionary<int, int> mapWithColor = buildMapWithColor(arr, n);

        // Print the maximum color
        Console.Write(findColor(mapWithColor, k));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // Javascript program to find color of the node

// Function to find color of the node
    function findColor(mapWithColor, query)
    {
        // Maximum is to store maximum color
        let maximum = 0;

        // Loop to check all the parent
        // values to get maximum color
        while (query >= 1)
        {

            // Find the number into map and get maximum color
            if (mapWithColor.has(query))
            {
                // Take the maximum color and
                // assign into maximum variable
                maximum = Math.max(maximum, mapWithColor.get(query));
            }

            // Find parent index
            if (query % 2 == 1)
                query = (query - 1) / 2;
            else
                query = query / 2;
        }

        // Return maximum color
        return maximum;
    }

    // Function to build hash map with color
    function buildMapWithColor(arr, n)
    {
        // To store color of each node
        let mapWithColor = new Map();

        // For each number add a color number
        for (let i = 0; i < n; i++)
        {
            // Assigning color
            mapWithColor.set(arr[i], i + 1);
        }

        // Return hash map
        return mapWithColor;
    }

    // Driver code   
        let arr = [ 3, 2, 1, 3 ];

        let n = arr.length;

        let k = 7;

        // Build mapWithColor
        let mapWithColor = buildMapWithColor(arr, n);

        // Print the maximum color
        document.write(findColor(mapWithColor, k));

      // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
4
```