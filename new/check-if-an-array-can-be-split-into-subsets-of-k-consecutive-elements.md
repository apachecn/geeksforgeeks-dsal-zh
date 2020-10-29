# 检查数组是否可以分为 K 个连续元素的子集

> 原文：[https://www.geeksforgeeks.org/check-if-an-array-can-be-split-into-subsets-of-k-consecutive-elements/](https://www.geeksforgeeks.org/check-if-an-array-can-be-split-into-subsets-of-k-consecutive-elements/)

给定一个数组 **arr []** 和整数 **K** ，任务是将该数组拆分为大小为 **K** 的子集，以使每个子集由**组成 K** 个连续元素。

**示例**：

> **输入**：arr [] = {1、2、3、6、2、3、4、7、8}，K = 3
> **输出**：true
> **解释**：
> 长度为 9 的给定数组可以分为 3 个子集{1、2、3}，{2、3、4}和{6、7、8}，这样每个子集 由 3 个连续的元素组成。
> 
> **输入**：arr [] = [1、2、3、4、5]，K = 4
> **输出**：否
> **说明**：
> 无法将长度为 5 的给定数组拆分为 4 的子集。

**方法**

请按照以下步骤解决问题：

*   将所有数组元素的频率存储在 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中

*   遍历 **HashMap** 。

*   对于 **HashMap** 中存在的每个元素，请检查是否所有出现的元素都可以用**接下来（K – 1）个连续元素**分组为一个子集。 如果是这样，请相应地降低 **HashMap** 中子集中包含的元素的频率，然后继续进行。

*   如果找到任何无法分组为 K 个连续元素的子集的元素，则输出 False。 否则打印 True。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a given array can
// be split into subsets of K consecutive
// elements
bool groupInKConsecutive(vector<int>& arr,
                         int K)
{
    // Stores the frequencies of
    // array elements
    map<int, int> count;

    for (int h : arr) {
        ++count[h];
    }

    // Traverse the map
    for (auto c : count) {
        int cur = c.first;
        int n = c.second;

        // Check if all its occurrences can
        // be grouped into K subsets
        if (n > 0) {

            // Traverse next K elements
            for (int i = 1; i < K; ++i) {

                // If the element is not
                // present in the array
                if (!count.count(cur + i)) {
                    return false;
                }

                count[cur + i] -= n;

                // If it cannot be split into
                // required number of subsets
                if (count[cur + i] < 0)
                    return false;
            }
        }
    }

    return true;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 3, 6, 2,
                        3, 4, 7, 8 };
    int k = 3;
    if (groupInKConsecutive(arr, k)) {
        cout << "True";
    }
    else {
        cout << "False";
    }
}

```

## Java

```java

// Java Program to implement the
// above approach
import java.util.*;
class GFG{

// Function to check if a given array can
// be split into subsets of K consecutive
// elements
static boolean groupInKConsecutive(int[] arr,
                                    int K)
{
    // Stores the frequencies of
    // array elements
    HashMap<Integer,
              Integer> count = new HashMap<Integer,
                                           Integer>();

    for (int h : arr) 
    {
        if(count.containsKey(h))
            count.put(h, count.get(h) + 1);
        else
            count.put(h, 1);
    }

    // Traverse the map
    for (Map.Entry<Integer,
                    Integer> c : count.entrySet())
    {
        int cur = c.getKey();
        int n = c.getValue();

        // Check if all its occurrences can
        // be grouped into K subsets
        if (n > 0)
        {

            // Traverse next K elements
            for (int i = 1; i < K; ++i)
            {

                // If the element is not
                // present in the array
                if (!count.containsKey(cur + i)) 
                {
                    return false;
                }

                count.put(cur + i, count.get(cur + i) - n);

                // If it cannot be split into
                // required number of subsets
                if (count.get(cur + i) < 0)
                    return false;
            }
        }
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 6, 2,
                     3, 4, 7, 8 };
    int k = 3;
    if (groupInKConsecutive(arr, k))
    {
        System.out.print("True");
    }
    else
    {
        System.out.print("False");
    }
}
}

// This code contributed by sapnasingh4991

```

## Python3

```py

# Python3 program to implement the
# above approach

from collections import defaultdict

# Function to check if a given array can
# be split into subsets of K consecutive
# elements
def groupInKConsecutive(arr, K):

    # Stores the frequencies of
    # array elements
    count = defaultdict(int)

    for h in arr:
        count[h] += 1

    # Traverse the map
    for key, value in count.items():
        cur = key
        n = value

        # Check if all its occurrences can
        # be grouped into K subsets
        if (n > 0):

            # Traverse next K elements
            for i in range(1, K):

                # If the element is not
                # present in the array
                if ((cur + i) not in count):
                    return False

                count[cur + i] -= n

                # If it cannot be split into
                # required number of subsets
                if (count[cur + i] < 0):
                    return False

    return True

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 6, 2,
            3, 4, 7, 8 ]
    k = 3

    if (groupInKConsecutive(arr, k)):
        print("True")
    else:
        print("False")

# This code is contributed by chitranayal

```

## C#

```cs

// C# program to implement the
// above approach
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Function to check if a given array can
// be split into subsets of K consecutive
// elements
static bool groupInKConsecutive(int[] arr,
                                int K)
{

    // Stores the frequencies of
    // array elements
    Dictionary<int,
               int> count = new Dictionary<int,
                                           int>();

    foreach(int h in arr) 
    {
        if (count.ContainsKey(h))
            count[h]++;
        else
            count[h] = 1;
    }

    // Traverse the map
    foreach(int c in count.Keys.ToList())
    {
        int cur = c;
        int n = count;

        // Check if all its occurrences can
        // be grouped into K subsets
        if (n > 0)
        {

            // Traverse next K elements
            for(int i = 1; i < K; ++i)
            {

                // If the element is not
                // present in the array
                if (!count.ContainsKey(cur + i)) 
                {
                    return false;
                }

                count[cur + i] -= n;

                // If it cannot be split into
                // required number of subsets
                if (count[cur + i] < 0)
                    return false;
            }
        }
    }
    return true;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 1, 2, 3, 6, 2,
                  3, 4, 7, 8 };
    int k = 3;
    if (groupInKConsecutive(arr, k))
    {
        Console.Write("True");
    }
    else
    {
        Console.Write("False");
    }
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
True

```

**时间复杂度**：O（N * log（N））

**辅助空间**：`O(n)`



* * *

* * *



