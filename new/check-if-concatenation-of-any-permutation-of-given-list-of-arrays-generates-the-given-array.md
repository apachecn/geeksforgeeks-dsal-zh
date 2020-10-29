# 检查给定数组列表的任何置换的串联是否生成给定数组

> 原文：[https://www.geeksforgeeks.org/check-if-concatenation-of-any-permutation-of-given-list-of-arrays-generates-the-given-array/](https://www.geeksforgeeks.org/check-if-concatenation-of-any-permutation-of-given-list-of-arrays-generates-the-given-array/)

给定 **N** 个不同整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** 以及一个不同整数的数组**个[]** 的列表， 检查给定的数组列表是否可以以任何顺序串联以获得给定的数组。 如果可能，则打印**“是”** 。 否则，打印**“否”** 。

**示例**：

> **输入**：arr [] = {1、2、4、3}，件[] [] = {{1}，{4、3}，{2}}
> **输出 **：是
> **说明**：
> 将列表重新排列为{{1}，{2}，{4、3}}。
> 现在，连接列表中的所有数组将生成与给定数组相同的序列{1,2,4,3}。
> 
> **输入**：arr [] = {1、2、4、3}，片段= {{1}，{2}，{3、4}}
> **输出**：否
> **说明**：
> 无法对给定列表进行排列，以使连接后生成的序列等于给定数组。

**天真的方法**：最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr []** ，对于每个元素， **arr [i]** 进行检查 如果列表中存在任何数组，则该数组是否从 **arr [i]** 开始。 如果发现为真，则增加 **i** ，同时发现数组中存在的元素等于 **arr [i]** 。 如果它们不相等，则打印**否**。 重复上述步骤，直到 **i < N** 为止。 遍历给定数组的元素后，打印**是**。

**时间复杂度**：O（N <sup>2</sup> ）

**辅助空间**：`O(n)`

**高效方法**：这个想法是通过使用 [Map 存储给定数组 **arr []** 中存在的元素的索引来使用](https://www.geeksforgeeks.org/map-interface-java-examples/)[散列](http://www.geeksforgeeks.org/hashing-data-structure/)的概念 数据结构。 请按照以下步骤解决问题：

1.  创建一个 [**映射**](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，以存储给定数组 **arr []** 的元素的索引。

2.  [遍历列表中存在的每个数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个数组，请执行以下步骤：

    *   从**映射**中找到数组 **arr []** 中其第一个元素的索引。

    *   检查获取的数组是否为数组 **arr []** 的子数组，或者是否不是从之前找到的索引开始。

3.  如果子数组与找到的数组不相等，则打印**否**。

4.  否则，在[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)之后，打印**是**。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to obtain array by concatenating
// the arrays in list pieces[]
bool check(vector<int>& arr, 
    vector<vector<int>>& pieces)
{

    // Stores the index of element in
    // the given array arr[]
    unordered_map<int, int> m;

    for(int i = 0; i < arr.size(); i++)
        m[arr[i]] = i + 1;

    // Traverse over the list pieces
    for(int i = 0; i < pieces.size(); i++)
    {

        // If item size is 1 and
        // exists in map
        if (pieces[i].size() == 1 && 
          m[pieces[i][0]] != 0)
        {
            continue;
        }

        // If item contains > 1 element
        // then check order of element
        else if (pieces[i].size() > 1 &&
               m[pieces[i][0]] != 0) 
        {
            int idx = m[pieces[i][0]] - 1;

            idx++;

            // If end of the array
            if (idx >= arr.size())
                return false;

            // Check the order of elements
            for(int j = 1; j < pieces[i].size(); j++)
            {

                // If order is same as
                // the array elements
                if (arr[idx] == pieces[i][j]) 
                {

                    // Increment idx
                    idx++;

                    // If order breaks
                    if (idx >= arr.size() && 
                     j < pieces[i].size() - 1)
                        return false;
                }

                // Otherwise
                else
                {
                    return false;
                }
            }
        }

        // Return false if the first
        // element doesn't exist in m
        else
        {
            return false;
        }
    }

    // Return true
    return true;
}

// Driver Code
int main()
{

    // Given target list
    vector<int> arr = { 1, 2, 4, 3 };

    // Given array of list
    vector<vector<int> > pieces{ { 1 }, { 4, 3 }, { 2 } };

    // Function call
    if (check(arr, pieces))
    {
        cout << "Yes";
    }
    else
    {
        cout << "No";
    }
    return 0;
}

// This code is contributed by akhilsaini

```

## Java

```java

// Java program for the above approach

import java.util.*;

class GFG {

    // Function to check if it is possible
    // to obtain array by concatenating
    // the arrays in list pieces[]
    static boolean check(
        List<Integer> arr,
        ArrayList<List<Integer> > pieces)
    {
        // Stores the index of element in
        // the given array arr[]
        Map<Integer, Integer> m
            = new HashMap<>();

        for (int i = 0; i < arr.size(); i++)
            m.put(arr.get(i), i);

        // Traverse over the list pieces
        for (int i = 0;
             i < pieces.size(); i++) {

            // If item size is 1 and
            // exists in map
            if (pieces.get(i).size() == 1
                && m.containsKey(
                       pieces.get(i).get(0))) {
                continue;
            }

            // If item contains > 1 element
            // then check order of element
            else if (pieces.get(i).size() > 1
                     && m.containsKey(
                            pieces.get(i).get(0))) {

                int idx = m.get(
                    pieces.get(i).get(0));

                idx++;

                // If end of the array
                if (idx >= arr.size())
                    return false;

                // Check the order of elements
                for (int j = 1;
                     j < pieces.get(i).size();
                     j++) {

                    // If order is same as
                    // the array elements
                    if (arr.get(idx).equals(
                            pieces.get(i).get(j))) {

                        // Increment idx
                        idx++;

                        // If order breaks
                        if (idx >= arr.size()
                            && j < pieces.get(i).size() - 1)
                            return false;
                    }

                    // Otherwise
                    else {
                        return false;
                    }
                }
            }

            // Return false if the first
            // element doesn't exist in m
            else {
                return false;
            }
        }

        // Return true
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given target list
        List<Integer> arr
            = Arrays.asList(1, 2, 4, 3);

        ArrayList<List<Integer> > pieces
            = new ArrayList<>();

        // Given array of list
        pieces.add(Arrays.asList(1));
        pieces.add(Arrays.asList(4, 3));
        pieces.add(Arrays.asList(2));

        // Function Call
        if (check(arr, pieces)) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }
}

```

## Python3

```py

# Python3 program for the above approach
from array import *

# Function to check if it is possible
# to obtain array by concatenating
# the arrays in list pieces[]
def check(arr, pieces):

    # Stores the index of element in
    # the given array arr[]
    m = {}

    for i in range(0, len(arr)):
        m[arr[i]] = i + 1

    # Traverse over the list pieces
    for i in range(0, len(pieces)):

        # If item size is 1 and
        # exists in map
        if (len(pieces[i]) == 1 and
              m[pieces[i][0]] != 0):
            continue

        # If item contains > 1 element
        # then check order of element
        elif (len(pieces[i]) > 1 and
                m[pieces[i][0]] != 0):
            idx = m[pieces[i][0]] - 1
            idx = idx+1

            # If end of the array
            if idx >= len(arr):
                return False

            # Check the order of elements
            for j in range(1, len(pieces[i])):

                # If order is same as
                # the array elements
                if arr[idx] == pieces[i][j]:
                    # Increment idx
                    idx = idx+1

                    # If order breaks
                    if (idx >= len(arr) and
                           j < len(pieces[i]) - 1):
                        return False

                # Otherwise
                else:
                    return False

        # Return false if the first
        # element doesn't exist in m
        else:
            return False

    # Return true
    return True

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 4, 3 ]

    # Given array of list
    pieces = [ [ 1 ], [ 4, 3 ], [ 2 ] ]

    # Function call
    if check(arr, pieces) == True:
        print("Yes")
    else:
        print("No")

# This code is contributed by akhilsaini

```

## C#

```cs

// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Function to check if it is possible
// to obtain array by concatenating
// the arrays in list pieces[]
static bool check(List<int> arr,
                  List<List<int>> pieces)
{

    // Stores the index of element in
    // the given array arr[]
    Dictionary<int, 
               int> m = new Dictionary<int, 
                                       int>();

    for(int i = 0; i < arr.Count; i++)
        m.Add(arr[i], i);

    // Traverse over the list pieces
    for(int i = 0; i < pieces.Count; i++)
    {

        // If item size is 1 and
        // exists in map
        if (pieces[i].Count == 1 && 
            m.ContainsKey(pieces[i][0]))
        {
            continue;
        }

        // If item contains > 1 element
        // then check order of element
        else if (pieces[i].Count > 1 && 
                 m.ContainsKey(pieces[i][0]))
        {
            int idx = m[pieces[i][0]];

            idx++;

            // If end of the array
            if (idx >= arr.Count)
                return false;

            // Check the order of elements
            for(int j = 1; j < pieces[i].Count; j++)
            {

                // If order is same as
                // the array elements
                if (arr[idx] == pieces[i][j])
                {

                    // Increment idx
                    idx++;

                    // If order breaks
                    if (idx >= arr.Count && 
                     j < pieces[i].Count - 1)
                        return false;
                }

                // Otherwise
                else
                {
                    return false;
                }
            }
        }

        // Return false if the first
        // element doesn't exist in m
        else
        {
            return false;
        }
    }

    // Return true
    return true;
}

// Driver Code
static public void Main()
{

    // Given target list
    List<int> arr = new List<int>(){ 1, 2, 4, 3 };

    List<List<int> > pieces = new List<List<int> >();

    // Given array of list
    pieces.Add(new List<int>(){ 1 });
    pieces.Add(new List<int>(){ 4, 3 });
    pieces.Add(new List<int>(){ 2 });

    // Function call
    if (check(arr, pieces))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by akhilsaini

```

**Output:** 

```
Yes

```

**时间复杂度**：O（N * log N）其中 N 是给定数组的长度。

**辅助空间**：`O(n)`



* * *

* * *



