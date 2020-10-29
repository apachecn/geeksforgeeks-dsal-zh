# 检查给定数组中每个元素的频率是否唯一

> 原文：[https://www.geeksforgeeks.org/check-if-frequency-of-each-element-in-given-array-is-unique-or-not/](https://www.geeksforgeeks.org/check-if-frequency-of-each-element-in-given-array-is-unique-or-not/)

给定 **N** 个正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，其中整数在 **1 到 N** 范围内。 检查数组中元素的[频率是否唯一。 如果所有频率都是唯一的，则打印**“是”** ，否则打印**“否”** 。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

**示例**：

> **输入**：N = 5，arr [] = {1，1，2，5，5}
> **输出**：否
> **说明**：
> 该数组包含 2（1's），1（2's）和 2（5's），因为 1 和 5 的频率数相同，即 2 倍。 因此，该数组不满足该条件。
> 
> **输入**：N = 10，arr [] = {2，2，5，10，1，2，10，5，10，2}
> **输出**：是
> **解释**：
> 1 的数目-> 1
> 2 的数目-> 4
> 5 的数目-> 2
> 10 的数目- > 3\.
> 由于，数组中存在的元素的出现次数是唯一的。 因此，该数组不满足该条件。

**朴素的方法**：的想法是检查从 **1 到 N** 的每个数字是否存在于数组中。 如果是，则计算该元素在阵列中的频率，并将该频率存储在阵列中。 最后，只需检查数组中是否有重复的元素，并相应地打印输出即可。

**时间复杂度**：*O（N <sup>2</sup> ）*

**辅助空间**：*`O(n)`*

**高效方法**：的想法是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)。 步骤如下：

1.  遍历给定数组 **arr []** 并将每个元素的频率存储在 [Map](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 中。

2.  现在遍历映射，检查是否有任何元素的计数多次发生。

3.  如果上述步骤中任何元素的数量大于一个，则打印“ **否”** ，否则打印**“是”** 。

下面是上述方法的实现：

## C++

```cpp

// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether the
// frequency of elements in array
// is unique or not.
bool checkUniqueFrequency(int arr[],
                          int n)
{

    // Freq map will store the frequency
    // of each element of the array
    unordered_map<int, int> freq;

    // Store the frequency of each
    // element from the array
    for (int i = 0; i < n; i++) {
        freq[arr[i]]++;
    }

    unordered_set<int> uniqueFreq;

    // Check whether frequency of any
    // two or more elements are same
    // or not. If yes, return false
    for (auto& i : freq) {
        if (uniqueFreq.count(i.second))
            return false;
        else
            uniqueFreq.insert(i.second);
    }

    // Return true if each
    // frequency is unique
    return true;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 1, 2, 5, 5 };
    int n = sizeof arr / sizeof arr[0];

    // Function Call
    bool res = checkUniqueFrequency(arr, n);

    // Print the result
    if (res)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}

```

## Java

```java

// Java code for the above approach
import java.util.*;

class GFG{

// Function to check whether the
// frequency of elements in array
// is unique or not.
static boolean checkUniqueFrequency(int arr[],
                                    int n)
{

    // Freq map will store the frequency
    // of each element of the array
    HashMap<Integer,
            Integer> freq = new HashMap<Integer,
                                        Integer>();

    // Store the frequency of each
    // element from the array
    for(int i = 0; i < n; i++)
    {
        if(freq.containsKey(arr[i]))
        {
            freq.put(arr[i], freq.get(arr[i]) + 1);
        }else
        {
            freq.put(arr[i], 1);
        }
    }

    HashSet<Integer> uniqueFreq = new HashSet<Integer>();

    // Check whether frequency of any
    // two or more elements are same
    // or not. If yes, return false
    for(Map.Entry<Integer,
                  Integer> i : freq.entrySet())
    {
        if (uniqueFreq.contains(i.getValue()))
            return false;
        else
            uniqueFreq.add(i.getValue());
    }

    // Return true if each
    // frequency is unique
    return true;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 1, 2, 5, 5 };
    int n = arr.length;

    // Function call
    boolean res = checkUniqueFrequency(arr, n);

    // Print the result
    if (res)
        System.out.print("Yes" + "\n");
    else
        System.out.print("No" + "\n");
}
}

// This code is contributed by PrinciRaj1992

```

## Python3

```py

# Python3 code for 
# the above approach
from collections import defaultdict

# Function to check whether the
# frequency of elements in array
# is unique or not.
def checkUniqueFrequency(arr, n):

    # Freq map will store the frequency
    # of each element of the array
    freq = defaultdict (int)

    # Store the frequency of each
    # element from the array
    for i in range (n):
        freq[arr[i]] += 1

    uniqueFreq = set([])

    # Check whether frequency of any
    # two or more elements are same
    # or not. If yes, return false
    for i in freq:
        if (freq[i] in uniqueFreq):
            return False
        else:
            uniqueFreq.add(freq[i])

    # Return true if each
    # frequency is unique
    return True

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [1, 1, 2, 5, 5]
    n = len(arr)

    # Function Call
    res = checkUniqueFrequency(arr, n)

    # Print the result
    if (res):
        print ("Yes")
    else:
        print ("No")

# This code is contributed by Chitranayal

```

## C#

```cs

// C# code for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to check whether the
// frequency of elements in array
// is unique or not.
static bool checkUniqueFrequency(int []arr,
                                 int n)
{

    // Freq map will store the frequency
    // of each element of the array
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();

    // Store the frequency of each
    // element from the array
    for(int i = 0; i < n; i++)
    {
        if(freq.ContainsKey(arr[i]))
        {
            freq[arr[i]] = freq[arr[i]] + 1;
        }else
        {
            freq.Add(arr[i], 1);
        }
    }

    HashSet<int> uniqueFreq = new HashSet<int>();

    // Check whether frequency of any
    // two or more elements are same
    // or not. If yes, return false
    foreach(KeyValuePair<int,
                         int> i in freq)
    {
        if (uniqueFreq.Contains(i.Value))
            return false;
        else
            uniqueFreq.Add(i.Value);
    }

    // Return true if each
    // frequency is unique
    return true;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 1, 1, 2, 5, 5 };
    int n = arr.Length;

    // Function call
    bool res = checkUniqueFrequency(arr, n);

    // Print the result
    if (res)
        Console.Write("Yes" + "\n");
    else
        Console.Write("No" + "\n");
}
}

// This code is contributed by sapnasingh4991

```

**Output:** 

```
No

```

**时间复杂度**：*`O(n)`，其中 N 是数组中元素的数量。*

**辅助空间**：*`O(n)`*



* * *

* * *



