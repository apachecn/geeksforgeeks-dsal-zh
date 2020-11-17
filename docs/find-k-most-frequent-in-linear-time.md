# 在线性时间中查找最频繁的`k`个元素

> 原文：[https://www.geeksforgeeks.org/find-k-most-frequent-in-linear-time/](https://www.geeksforgeeks.org/find-k-most-frequent-in-linear-time/)

给定一个整数数组，我们需要打印`k`个最频繁的元素。 如果存在多个，我们需要优先考虑首次出现的元素。

**示例**：

> **输入**：`arr[] = {10, 5, 20, 5, 10, 10, 30}, k = 2`
>
> **输出**：`10 5`
> 
> **输入**：`arr[] = {7, 7, 6, 6, 6, 7, 5, 4, 4, 10, 5}, k = 3`
>
> **输出**：`7 6 5`
>
> **说明**：
>
> 在此示例中，7 和 6 具有相同的频率。 因为首先出现 7 是第一个，所以我们先打印 7。 同样，5 和 4 具有相同的频率。 我们更喜欢 5，因为 5 的首次出现是第一。

我们在下面的文章中讨论了两种方法。

[**查找给定数组中出现次数最多的`k`个数**](https://www.geeksforgeeks.org/find-k-numbers-occurrences-given-array/)

让我们首先讨论一个可以按任意顺序打印的简单解决方案，以防止有多个。 然后，我们将讨论采用顺序的解决方案。

这个想法是将哈希与频率索引一起使用。 我们首先将计数存储在哈希中。 然后，我们遍历哈希并使用频率作为索引来存储具有给定频率的元素。 此处的重要因素是最大频率可以为`n`。 因此，大小为`n + 1`的数组会很好。

## C++

```cpp

// C++ implementation to find k numbers with most
// occurrences in the given array
#include <bits/stdc++.h>
using namespace std;

// funnction to print the k numbers with most occurrences
void print_N_mostFrequentNumber(int arr[], int n, int k)
{
    // unordered_map 'um' implemented as frequency
    // hash table
    unordered_map<int, int> um;
    for (int i = 0; i < n; i++)
        um[arr[i]]++;

    // Use frequencies as indexes and put
    // elements with given frequency in a
    // vector (related to a frequency)
    vector<int> freq[n + 1];
    for (auto x : um)
        freq[x.second].push_back(x.first);

    // Initialize count of items printed
    int count = 0;

    // Traverse the frequency array from
    // right side as we need the most
    // frequent items.
    for (int i = n; i >= 0; i--) {

        // Print items of current frequency
        for (int x : freq[i]) {
            cout << x << " ";
            count++;
            if (count == k)
                return;
        }
    }
}

// Driver program to test above
int main()
{
    int arr[] = { 3, 1, 4, 4, 5, 2, 6, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    print_N_mostFrequentNumber(arr, n, k);
    return 0;
}

```

## Java

```java

// Java implementation to find k elements with max occurence.
import java.util.*;
public class KFrequentNumbers {
    static void print_N_mostFrequentNumber(int[] arr, int n, int k)
    {
        Map<Integer, Integer> mp = new HashMap<Integer, Integer>();

        // Put count of all the distinct elements in Map
        // with element as the key & count as the value.
        for (int i = 0; i < n; i++) {

            // Get the count for the element if already
            // present in the Map or get the default value
            // which is 0.
            mp.put(arr[i], mp.getOrDefault(arr[i], 0) + 1);
        }

        // Initialize an array list of array lists
        List<List<Integer> > freq = new ArrayList<List<Integer> >();
        for (int i = 0; i <= n; i++)
            freq.add(new ArrayList<Integer>());

        // Use frequencies as indexes and add corresponding
        // values to the list
        for (Map.Entry<Integer, Integer> x : mp.entrySet())
            freq.get(x.getValue()).add(x.getKey());

        // Traverse freq[] from right side.
        int count = 0;
        for (int i = n; i >= 0; i--) {
            for (int x : freq.get(i)) {
                System.out.println(x);
                count++;
                if (count == k)
                    return;
            }
        }
    }

    // Driver Code to test the code.
    public static void main(String[] args)
    {
        int arr[] = { 3, 1, 4, 4, 5, 2, 6, 1 };
        int n = arr.length;
        int k = 2;
        print_N_mostFrequentNumber(arr, n, k);
    }
}

```

## C#

```cs

// C# implementation to find 
// k elements with max occurence.
using System;
using System.Collections.Generic;
class KFrequentNumbers{

static void print_N_mostFrequentNumber(int[] arr, 
                                       int n, int k)
{
  Dictionary<int, 
             int> mp = new Dictionary<int, 
                                      int>();

  // Put count of all the 
  // distinct elements in Map
  // with element as the key 
  // & count as the value.
  for (int i = 0; i < n; i++)
  {
    // Get the count for the 
    // element if already
    // present in the Map 
    // or get the default value
    // which is 0.
    if(mp.ContainsKey(arr[i]))
    {
      mp[arr[i]] = mp[arr[i]] + 1;
    }
    else
    {
      mp.Add(arr[i], 1);
    }
  }

  // Initialize an array 
  // list of array lists
  List<List<int> > freq = 
            new List<List<int> >();

  for (int i = 0; i <= n; i++)
    freq.Add(new List<int>());

  // Use frequencies as indexes
  // and add corresponding
  // values to the list
  foreach (KeyValuePair<int, 
                        int> x in mp)
    freq[x.Value].Add(x.Key);

  // Traverse []freq from 
  // right side.
  int count = 0;
  for (int i = n; i >= 0; i--) 
  {
    foreach (int x in freq[i]) 
    {
      Console.WriteLine(x);
      count++;
      if (count == k)
        return;
    }
  }
}

// Driver Code to test the code.
public static void Main(String[] args)
{
  int []arr = {3, 1, 4, 4, 
               5, 2, 6, 1};
  int n = arr.Length;
  int k = 2;
  print_N_mostFrequentNumber(arr, n, k);
}
}

// This code is contributed by Princi Singh

```

**输出**： 

```
4 1

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。

**根据第一种出现方式进行打印。** 为了保持所需的顺序，我们遍历了原始数组而不是映射。 为避免重复，我们需要在映射中将已处理条目标记为 -1。

## C++

```cpp

// C++ implementation to find k numbers with most
// occurrences in the given array
#include <bits/stdc++.h>
using namespace std;

// function to print the k numbers with most occurrences
void print_N_mostFrequentNumber(int arr[], int n, int k)
{
    // unordered_map 'um' implemented as frequency
    // hash table
    unordered_map<int, int> um;
    for (int i = 0; i < n; i++)
        um[arr[i]]++;

    // Use frequencies as indexes and put
    // elements with given frequency in a
    // vector (related to a frequency)
    vector<int> freq[n + 1];
    for (int i = 0; i < n; i++) {
        int f = um[arr[i]];
        if (f != -1) {
            freq[f].push_back(arr[i]);
            um[arr[i]] = -1;
        }
    }

    // Initialize count of items printed
    int count = 0;

    // Traverse the frequency array from
    // right side as we need the most
    // frequent items.
    for (int i = n; i >= 0; i--) {

        // Print items of current frequency
        for (int x : freq[i]) {
            cout << x << " ";
            count++;
            if (count == k)
                return;
        }
    }
}

// Driver program to test above
int main()
{
    int arr[] = { 3, 1, 4, 4, 5, 2, 6, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    print_N_mostFrequentNumber(arr, n, k);
    return 0;
}

```

## Java

```java

// Java implementation to find k elements with max occurence.
import java.util.*;
public class KFrequentNumbers {
    static void print_N_mostFrequentNumber(int[] arr, int n, int k)
    {
        Map<Integer, Integer> mp = new HashMap<Integer, Integer>();

        // Put count of all the distinct elements in Map
        // with element as the key & count as the value.
        for (int i = 0; i < n; i++) {

            // Get the count for the element if already
            // present in the Map or get the default value
            // which is 0.
            mp.put(arr[i], mp.getOrDefault(arr[i], 0) + 1);
        }

        // Initialize an array list of array lists
        List<List<Integer> > freq = new ArrayList<List<Integer> >();
        for (int i = 0; i <= n; i++)
            freq.add(new ArrayList<Integer>());

        // Use frequencies as indexes and add corresponding
        // values to the list
        for (int i = 0; i < n; i++) {
            int f = mp.get(arr[i]);
            if (f != -1) {
                freq.get(f).add(arr[i]);
                mp.put(arr[i], -1);
            }
        }

        // Traverse freq[] from right side.
        int count = 0;
        for (int i = n; i >= 0; i--) {
            for (int x : freq.get(i)) {
                System.out.println(x);
                count++;
                if (count == k)
                    return;
            }
        }
    }

    // Driver Code to test the code.
    public static void main(String[] args)
    {
        int arr[] = { 3, 1, 4, 4, 5, 2, 6, 1 };
        int n = arr.length;
        int k = 3;
        print_N_mostFrequentNumber(arr, n, k);
    }
}

```

## C#

```cs

// C# implementation to find k elements
// with max occurence.
using System;
using System.Collections.Generic;

class GFG{

static void print_N_mostFrequentNumber(int[] arr, 
                                       int n, int k)
{
    Dictionary<int, 
               int> mp = new Dictionary<int, 
                                        int>();

    // Put count of all the distinct 
    // elements in Map with element 
    // as the key & count as the value.
    for(int i = 0; i < n; i++) 
    {

        // Get the count for the element
        // if already present in the Map
        // or get the default value which is 0.
        if (mp.ContainsKey(arr[i]))
            mp[arr[i]]++;
        else
            mp.Add(arr[i], 0);
    }

    // Initialize an array list of array lists
    List<List<int>> freq = new List<List<int>>();
    for(int i = 0; i <= n; i++)
        freq.Add(new List<int>());

    // Use frequencies as indexes and 
    // add corresponding values to 
    // the list
    for(int i = 0; i < n; i++) 
    {
        int f = mp[arr[i]];
        if (f != -1)
        {
            freq[f].Add(arr[i]);

            if (mp.ContainsKey(arr[i]))
                mp[arr[i]] = -1;
            else
                mp.Add(arr[i], 0);
        }
    }

    // Traverse []freq from right side.
    int count = 0;
    for(int i = n; i >= 0; i--) 
    {
        foreach(int x in freq[i]) 
        {
            Console.Write(x);
            Console.Write(" ");
            count++;

            if (count == k)
                return;
        }
    }
}

// Driver Code 
public static void Main(String[] args)
{
    int []arr = { 3, 1, 4, 4, 5, 2, 6, 1 };
    int n = arr.Length;
    int k = 3;

    print_N_mostFrequentNumber(arr, n, k);
}
}

// This code is contributed by Amit Katiyar

```

**输出**： 

```
1 4 3

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。



* * *

* * *



