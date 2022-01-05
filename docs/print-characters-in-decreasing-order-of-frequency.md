# 按频率递减顺序打印字符

> 原文:[https://www . geeksforgeeks . org/print-按频率降序排列的字符/](https://www.geeksforgeeks.org/print-characters-in-decreasing-order-of-frequency/)

给定字符串 **str** ，任务是按照字符出现频率的降序打印字符。如果两个字符的频率相同，那么就按字母顺序降序排列。
**例:**

> **输入:**str = " geeks forgeeks "
> T3】输出:T5】e–4
> s–2
> k–2
> g–2
> r–1
> o–1
> f–1
> T13】输入:str = " bbcc "
> T16】输出:T18】c–2
> b–2

**进场 1:**

*   使用一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)来存储给定字符串所有元素的频率。
*   从地图中找到最大频率元素，用它的频率打印它，然后从地图中删除它。
*   当地图不为空时，重复上一步。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the characters
// of the given string in decreasing
// order of their frequencies
void printChar(string str, int len)
{

    // To store the
    unordered_map<char, int> occ;
    for (int i = 0; i < len; i++)
        occ[str[i]]++;

    // Map's size
    int size = occ.size();
    unordered_map<char, int>::iterator it;

    // While there are elements in the map
    while (size--) {

        // Finding the maximum value
        // from the map
        unsigned currentMax = 0;
        char arg_max;
        for (it = occ.begin(); it != occ.end(); ++it) {
            if (it->second > currentMax
                || (it->second == currentMax
                    && it->first > arg_max)) {
                arg_max = it->first;
                currentMax = it->second;
            }
        }

        // Print the character
        // alongwith its frequency
        cout << arg_max << " - " << currentMax << endl;

        // Delete the maximum value
        occ.erase(arg_max);
    }
}

// Driver code
int main()
{

    string str = "geeksforgeeks";
    int len = str.length();

    printChar(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG{

// Function to print the characters
// of the given String in decreasing
// order of their frequencies
static void printChar(char []arr, int len)
{

    // To store the
    HashMap<Character,
              Integer> occ = new HashMap<Character,
                                         Integer>();
    for (int i = 0; i < len; i++)
        if(occ.containsKey(arr[i]))
        {
            occ.put(arr[i], occ.get(arr[i]) + 1);
        }
          else
        {
            occ.put(arr[i], 1);
        }

    // Map's size
    int size = occ.size();

    // While there are elements in the map
    while (size-- > 0)
    {

        // Finding the maximum value
        // from the map
        int currentMax = 0;
        char arg_max = 0;
        for (Map.Entry<Character,
                        Integer> it : occ.entrySet())
        {
            if (it.getValue() > currentMax ||
               (it.getValue() == currentMax &&
                it.getKey() > arg_max))
            {
                arg_max = it.getKey();
                currentMax = it.getValue();
            }
        }

        // Print the character
        // alongwith its frequency
        System.out.print(arg_max + " - " +
                         currentMax + "\n");

        // Delete the maximum value
        occ.remove(arg_max);
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    int len = str.length();

    printChar(str.toCharArray(), len);
}
}

// This code is contributed by gauravrajput1
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the characters
// of the given String in decreasing
// order of their frequencies
static void printChar(char []arr, int len)
{

    // To store the
    Dictionary<char,
               int> occ = new Dictionary<char,
                                         int>();
    for (int i = 0; i < len; i++)
        if(occ.ContainsKey(arr[i]))
        {
            occ[arr[i]]  = occ[arr[i]] + 1;
        }
          else
        {
            occ.Add(arr[i], 1);
        }

    // Map's size
    int size = occ.Count;

    // While there are elements in the map
    while (size-- > 0)
    {

        // Finding the maximum value
        // from the map
        int currentMax = 0;
        char arg_max = (char)0;
        foreach (KeyValuePair<char, int> it in occ)
        {
            if (it.Value > currentMax ||
               (it.Value == currentMax &&
                it.Key > arg_max))
            {
                arg_max = it.Key;
                currentMax = it.Value;
            }
        }

        // Print the character
        // alongwith its frequency
        Console.Write(arg_max + " - " +
                      currentMax + "\n");

        // Delete the maximum value
        occ.Remove(arg_max);
    }
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int len = str.Length;

    printChar(str.ToCharArray(), len);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to print the characters
// of the given String in decreasing
// order of their frequencies
function printChar(arr, len)
{

    // To store the
    let  occ = new Map();
    for (let i = 0; i < len; i++)
        if(occ.has(arr[i]))
        {
            occ.set(arr[i], occ.get(arr[i]) + 1);
        }
          else
        {
            occ.set(arr[i], 1);
        }

    // Map's size
    let size = occ.size;

    // While there are elements in the map
    while (size-- > 0)
    {

        // Finding the maximum value
        // from the map
        let currentMax = 0;
        let arg_max = 0;
        for (let [key, value] of occ.entries())
        {
            if (value > currentMax ||
               (value == currentMax &&
                key > arg_max))
            {
                arg_max = key;
                currentMax = value;
            }
        }

        // Print the character
        // alongwith its frequency
        document.write(arg_max + " - " +
                         currentMax + "<br>");

        // Delete the maximum value
        occ.delete(arg_max);
    }
}

// Driver code
let str = "geeksforgeeks";
let len = str.length;

printChar(str.split(""), len);

// This code is contributed by patel2127
</script>
```

**Output**

```
e - 4
s - 2
k - 2
g - 2
r - 1
o - 1
f - 1

```

**方法 2 :** 我们将制作一个数组 **arr** ，其大小比给定字符串长度的大小大一，我们将在其中存储频率等于 **arr** 索引的字符列表，并遵循以下步骤:

*   使用给定字符串中的字符数组制作频率图。
*   遍历频率数组，如果它的值大于零就说 **k.**
*   在 **arr** 的第 k 个索引上，将其字符值存储在索引 0 处的列表中(因为如果频率相同，我们需要字母的降序)。
*   遍历**从后开始排列**，因为如果索引处列表不是空的，我们首先需要更高的频率，而不是打印它的频率和字符。

上述方法的实施:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG {
    // Driver Code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        printChar(str);
    }
    @SuppressWarnings("unchecked")
    // Function to print the characters
    // of the given string in decreasing
    // order of their frequencies
    public static void printChar(String str)
    {
        // Initializing array of List type.
        List<Character>[] arr = new List[str.length() + 1];
        for (int i = 0; i <= str.length(); i++) {
            // Initializing List of type Character.
            arr[i] = new ArrayList<>();
        }
        int[] freq = new int[256];
        // Mapking frequency map
        for (int i = 0; i < str.length(); i++) {
            freq[(char)str.charAt(i)]++;
        }
        // Traversing frequency array
        for (int i = 0; i < 256; i++) {
            if (freq[i] > 0) {
                // If frequency array is greater than zero
                // then storing its character on
                // i-th(frequency of that character) index
                // of arr
                arr[freq[i]].add(0, (char)(i));
            }
        }
        // Traversing arr from backwards as we need greater
        // frequency character first
        for (int i = arr.length - 1; i >= 0; i--) {
            if (!arr[i].isEmpty()) {
                for (char ch : arr[i]) {
                    System.out.println(ch + "-" + i);
                }
            }
        }
    }
}
```

**Output**

```
e-4
s-2
k-2
g-2
r-1
o-1
f-1

```

**时间复杂度:** O(n)，n 为给定字符串的长度

**辅助空间:** O(n)