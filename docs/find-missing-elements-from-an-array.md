# 从数组中查找缺少的元素

> 原文:[https://www . geesforgeks . org/find-从数组中缺失元素/](https://www.geeksforgeeks.org/find-missing-elements-from-an-array/)

给定范围**【1，N】**的整数列表，其中缺少一些元素。任务是找到丢失的元素。**注意**列表中可以有重复项。
**例:**

```
Input: arr[] = {1, 3, 3, 3, 5}
Output: 2 4

Input: arr[] = {1, 2, 3, 4, 4, 7, 7} 
Output: 5 6
```

**方法:**在给定的范围内**【1，N】**应该有一个元素对应每个指标。如果一个元素丢失了，那么它的索引将永远不会被访问。

```
Traverse the array:
For each element:
    if array[element] > 0:
          Mark the element as visited
Again, traverse the array:
     if element isNot Visited:
           add it as missing element
```

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the missing elements
vector<int> missing_elements(vector<int> vec)
{

    // Vector to store the list
    // of missing elements
    vector<int> mis;

    // For every given element
    for (int i = 0; i < vec.size(); i++) {

        // Find its index
        int temp = abs(vec[i]) - 1;

        // Update the element at the found index
        vec[temp] = vec[temp] > 0 ? -vec[temp] : vec[temp];
    }
    for (int i = 0; i < vec.size(); i++)

        // Current element was not present
        // in the original vector
        if (vec[i] > 0)
            mis.push_back(i + 1);

    return mis;
}

// Driver code
int main()
{
    vector<int> vec = { 3, 3, 3, 5, 1 };

    // Vector to store the returned
    // list of missing elements
    vector<int> miss_ele = missing_elements(vec);

    // Print the list of elements
    for (int i = 0; i < miss_ele.size(); i++)
        cout << miss_ele[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Function to find the missing elements
    static Vector missing_elements(Vector vec)
    {

        // Vector to store the list
        // of missing elements
        Vector mis = new Vector();

        // For every given element
        for (int i = 0; i < vec.size(); i++)
        {

            // Find its index
            int temp = Math.abs((int)vec.get(i)) - 1;

            // Update the element at the found index
            if ((int)vec.get(temp) > 0)
                vec.set(temp,-(int)vec.get(temp));
            else
                vec.set(temp,vec.get(temp));
        }
        for (int i = 0; i < vec.size(); i++)
        {
            // Current element was not present
            // in the original vector
            if ((int)vec.get(i) > 0)
                mis.add(i + 1);
        }
        return mis;
    }

    // Driver code
    public static void main(String args[])
    {
        Vector vec = new Vector();
        vec.add(3);
        vec.add(3);
        vec.add(3);
        vec.add(5);
        vec.add(1);

        // Vector to store the returned
        // list of missing elements
        Vector miss_ele = missing_elements(vec);

        // Print the list of elements
        for (int i = 0; i < miss_ele.size(); i++)
            System.out.print(miss_ele.get(i) + " ");
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the missing elements
def missing_elements(vec):

    # Vector to store the list
    # of missing elements
    mis = []

    # For every given element
    for i in range(len(vec)):

        # Find its index
        temp = abs(vec[i]) - 1

        # Update the element at the found index
        if vec[temp] > 0:
            vec[temp] = -vec[temp]

    for i in range(len(vec)):

        # Current element was not present
        # in the original vector
        if (vec[i] > 0):
            mis.append(i + 1)

    return mis

# Driver code
vec = [3, 3, 3, 5, 1]

# Vector to store the returned
# list of missing elements
miss_ele = missing_elements(vec)

# Print the list of elements
for i in range(len(miss_ele)):
    print(miss_ele[i], end = " ")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;            

class GFG
{

    // Function to find the missing elements
    static List<int> missing_elements(List<int> vec)
    {

        // List<int> to store the list
        // of missing elements
        List<int> mis = new List<int>();

        // For every given element
        for (int i = 0; i < vec.Count; i++)
        {

            // Find its index
            int temp = Math.Abs((int)vec[i]) - 1;

            // Update the element at the found index
            if ((int)vec[temp] > 0)
                vec[temp] = -(int)vec[temp];
            else
                vec[temp] = vec[temp];
        }
        for (int i = 0; i < vec.Count; i++)
        {
            // Current element was not present
            // in the original vector
            if ((int)vec[i] > 0)
                mis.Add(i + 1);
        }
        return mis;
    }

    // Driver code
    public static void Main(String []args)
    {
        List<int> vec = new List<int>();
        vec.Add(3);
        vec.Add(3);
        vec.Add(3);
        vec.Add(5);
        vec.Add(1);

        // List to store the returned
        // list of missing elements
        List<int> miss_ele = missing_elements(vec);

        // Print the list of elements
        for (int i = 0; i < miss_ele.Count; i++)
            Console.Write(miss_ele[i] + " ");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to find the missing elements
    function missing_elements(vec)
    {

        // Vector to store the list
        // of missing elements
        let mis = [];

        // For every given element
        for (let i = 0; i < vec.length; i++) {

            // Find its index
            let temp = Math.abs(vec[i]) - 1;

            // Update the element at the found index
            vec[temp] = vec[temp] > 0 ? -vec[temp] : vec[temp];
        }
        for (let i = 0; i < vec.length; i++)

            // Current element was not present
            // in the original vector
            if (vec[i] > 0)
                mis.push(i + 1);

        return mis;
    }

    let vec = [ 3, 3, 3, 5, 1 ];

    // Vector to store the returned
    // list of missing elements
    let miss_ele = missing_elements(vec);

    // Print the list of elements
    for (let i = 0; i < miss_ele.length; i++)
        document.write(miss_ele[i] + " ");

</script>
```

**Output:** 

```
2 4
```

***时间复杂度:** O(N)，其中 N 为*向量**向量**的*长度。*

***辅助空间:** O(N)*