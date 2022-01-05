# 清空管柱所需的操作

> 原文:[https://www . geesforgeks . org/operations-要求将字符串留空/](https://www.geeksforgeeks.org/operations-required-to-make-the-string-empty/)

给定一个字符串 **str** ，任务是用给定的操作将字符串清空。在单个操作中，您可以挑选字符串中的一些字符(每个挑选的字符应该具有相同的频率)并将其从字符串中移除。打印使字符串为空所需的全部操作。
**例:**

> **输入:** str = "aabbccc"
> **输出:** 2
> 在一次操作中，字符‘a’和‘b’可以被移除，因为两者具有相同的频率。
> 第二次操作可以删除频率为 3 的字符‘c’。
> 共需要 2 次操作。
> **输入:**str = " geeks forgeeks "
> **输出:** 3

**方法:**找到字符串字符的唯一频率。唯一频率的总计数将是使字符串为空所需的操作数。
对于**str = " aaabbcccc "**，唯一的频率是 **3** 和 **4** 。唯一频率总数为 **2** 。
HashMap 可用于存储字符及其频率，然后 HashSet 可用于查找唯一频率的计数，即所需操作的数量。
以下是上述方法的实施:

## C++

```
// CPP implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of operations required
int totalOperations(string str, int len)
{
    // HashMap to store characters and their frequencies
    unordered_map<char, int> h;
    for (int i = 0; i < len; i++)

        // If already contains the character then
        // increment its frequency by 1
        h[str[i]]++;

    // HashSet to store unique frequency
    unordered_set<int> hs;

    // Insert frequencies into HashSet
    for (auto i : h)
        hs.insert(i.second);

    // Count of unique frequencies
    return hs.size();
}

// Driver Code
int main()
{
    string str = "geeksforgeeks";
    int len = str.length();

    cout << totalOperations(str, len) << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG {

    // Function to return the count of operations required
    static int totalOperations(String str, int len)
    {

        // HashMap to store characters and their frequencies
        HashMap<Character, Integer> h = new HashMap<Character, Integer>();
        for (int i = 0; i < len; i++) {

            // If already contains the character then
            // increment its frequency by 1
            if (h.containsKey(str.charAt(i)))
                h.put(str.charAt(i), h.get(str.charAt(i)) + 1);

            // Else add the character to the HashMap with frequency 1
            else
                h.put(str.charAt(i), 1);
        }

        // Set to iterate over HashMap
        Set<Map.Entry<Character, Integer> > set = h.entrySet();

        // HashSet to store unique frequency
        HashSet<Integer> hs = new HashSet<Integer>();

        // Insert frequencies into HashSet
        for (Map.Entry<Character, Integer> me : set)
            hs.add(me.getValue());

        // Count of unique frequencies
        return hs.size();
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        int len = str.length();
        System.out.println(totalOperations(str, len));
    }
}
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the count of operations required
def totalOperations(st, length):

    # Dictionary to store characters and their frequencies
    d = {}
    for i in range(length):

        # If already contains the character then
        # increment its frequency by 1
        if st[i] in d:
            d[st[i]] += 1

        # Else add the character to the HashMap with frequency 1
        else:
            d[st[i]] = 1

    # Set to Store unique frequency
    valueSet = set()

    # Insert frequencies into HashSet
    for key in d.keys():
        valueSet.add(d[key])

    # Count of unique frequencies
    return len(valueSet)

# Driver Code
st = "geeksforgeeks"
l = len(st)
print(totalOperations(st, l))

# This code is contributed by Vivekkumar Singh
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return
// the count of operations required
static int totalOperations(String str, int len)
{

    // HashMap to store characters
    // and their frequencies
    Dictionary<char,
               int> h = new Dictionary<char,
                                       int>();
    for (int i = 0; i < len; i++)
    {

        // If already contains the character then
        // increment its frequency by 1
        if (h.ContainsKey(str[i]))
            h[str[i]] = h[str[i]] + 1;

        // Else add the character
        // to the HashMap with frequency 1
        else
            h.Add(str[i], 1);
    }

    // Set to iterate over HashMap
    // HashSet to store unique frequency
    HashSet<int> hs = new HashSet<int>();

    // Insert frequencies into HashSet
    foreach(KeyValuePair<char, int> me in h)
        hs.Add(me.Value);

    // Count of unique frequencies
    return hs.Count;
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    int len = str.Length;
    Console.WriteLine(totalOperations(str, len));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of operations required
function totalOperations(str, len)
{
    // HashMap to store characters and their frequencies
    var h = new Map();
    for (var i = 0; i < len; i++)

        // If already contains the character then
        // increment its frequency by 1
        if(h.has(str[i]))
            h.set(str[i], h.get(str[i])+1)
        else
            h.set(str[i], 1)

    // HashSet to store unique frequency
    var hs = new Set();

    // Insert frequencies into HashSet
    h.forEach((value, key) => {

        hs.add(value);
    });

    // Count of unique frequencies
    return hs.size;
}

// Driver Code
var str = "geeksforgeeks";
var len = str.length;
document.write( totalOperations(str, len));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
3
```