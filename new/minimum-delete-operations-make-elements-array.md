# 最小删除操作，以使数组的所有元素相同

给定 n 个元素的数组，以便元素可以重复。 我们可以从数组中删除任意数量的元素。 任务是找到要从数组中删除的元素的最小数量，以使其相等。
**范例**：

```
Input: arr[] = {4, 3, 4, 4, 2, 4}
Output: 2
After deleting 2 and 3 from array, array becomes 
arr[] = {4, 4, 4, 4} 

Input: arr[] = {1, 2, 3, 4, 5}
Output: 4
We can delete any four elements from array.

```

在这个问题上，我们需要最小化删除操作。 该方法很简单，我们计算数组中每个元素的频率，然后在**计数数组**中找到最频繁的元素的频率。 将此频率设为 max_freq。 要获取要从数组中删除的最小元素数，请计算 **n – max_freq** ，其中 n 是给定数组中的元素数。

## C++

```cpp

// C++ program to find minimum
// number of deletes required
// to make all elements same.
#include <bits/stdc++.h>
using namespace std;

// Function to get minimum number of elements to be deleted
// from array to make array elements equal
int minDelete(int arr[], int n)
{
    // Create an hash map and store frequencies of all
    // array elements in it using element as key and
    // frequency as value
    unordered_map<int, int> freq;
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Find maximum frequency among all frequencies.
    int max_freq = INT_MIN;
    for (auto itr = freq.begin(); itr != freq.end(); itr++)
        max_freq = max(max_freq, itr->second);

    // To minimize delete operations, we remove all
    // elements but the most frequent element.
    return n - max_freq;
}

// Driver program to run the case
int main()
{
    int arr[] = { 4, 3, 4, 4, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minDelete(arr, n);
    return 0;
}

```

## Java

```java

// Java program to find minimum number
// of deletes required to make all
// elements same.
import java.util.*;

class GFG{

// Function to get minimum number of 
// elements to be deleted from array
// to make array elements equal
static int minDelete(int arr[], int n)
{

    // Create an hash map and store 
    // frequencies of all array elements
    // in it using element as key and
    // frequency as value
    HashMap<Integer, Integer> freq = new HashMap<>();
    for(int i = 0; i < n; i++)
        freq.put(arr[i], freq.getOrDefault(arr[i], 0) + 1);

    // Find maximum frequency among all frequencies.
    int max_freq = Integer.MIN_VALUE;
    for(Map.Entry<Integer, 
                  Integer> entry : freq.entrySet())
        max_freq = Math.max(max_freq, 
                            entry.getValue());

    // To minimize delete operations, 
    // we remove all elements but the
    // most frequent element.
    return n - max_freq ;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 3, 4, 4, 2, 4 };
    int n = arr.length;

    System.out.print(minDelete(arr, n));
}
}

// This code is contributed by amal kumar choubey and corrected by Leela Kotte

```

## Python3

```py

# Python3 program to find minimum 
# number of deletes required to 
# make all elements same. 

# Function to get minimum number 
# of elements to be deleted from 
# array to make array elements equal 
def minDelete(arr, n): 

    # Create an dictionary and store 
    # frequencies of all array 
    # elements in it using 
    # element as key and 
    # frequency as value 
    freq = {} 
    for i in range(n): 
        if arr[i] in freq: 
            freq[arr[i]] += 1
        else: 
            freq[arr[i]] = 1; 

    # Find maximum frequency 
    # among all frequencies. 
    max_freq = 0; 
    for i, j in freq.items(): 
        max_freq = max(max_freq, j); 

    # To minimize delete operations, 
    # we remove all elements but the 
    # most frequent element. 
    return n - max_freq; 

# Driver code 
arr = [ 4, 3, 4, 4, 2, 4 ]; 
n = len(arr) 

print(minDelete(arr, n)); 

# This code is contributed by grand_master 

```

## C#

```cs

// C# program to find minimum number
// of deletes required to make all
// elements same.
using System;
using System.Collections.Generic;
class GFG {

    // Function to get minimum number of
    // elements to be deleted from array
    // to make array elements equal
    static int minDelete(int[] arr, int n)
    {

        // Create an hash map and store
        // frequencies of all array elements
        // in it using element as key and
        // frequency as value
        Dictionary<int, int> freq
            = new Dictionary<int, int>();
        for (int i = 0; i < n; i++)
            if (freq.ContainsKey(arr[i])) 
            {
                freq[arr[i]] = freq[arr[i]] + 1;
            }
            else
            {
                freq.Add(arr[i], 1);
            }

        // Find maximum frequency among all frequencies.
        int max_freq = int.MinValue;
        foreach(KeyValuePair<int, int> entry in freq)
            max_freq = Math.Max(max_freq, entry.Value);

        // To minimize delete operations,
        // we remove all elements but the
        // most frequent element.
        return n - max_freq + 1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = {4, 3, 4, 4, 2, 4};
        int n = arr.Length;
          Console.Write(minDelete(arr, n));
    }
}

// This code is contributed by Amit Katiyar

```

**输出**：

```
2

```

**时间复杂度**：O（n）

**<u>注意：</u>** 在这里，我们可以优化多余的空间以将每个元素的频率计数为 O（1），但是为此，我们必须修改原始数组。 请参阅[此](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)文章。

本文由 [**Shashank Mishra（Gullu）**](https://www.facebook.com/shashank.mishra.92167) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

