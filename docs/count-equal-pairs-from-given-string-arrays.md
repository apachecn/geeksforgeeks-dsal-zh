# 从给定的字符串数组中计数相等的对

> 原文:[https://www . geesforgeks . org/count-equal-pairs-from-given-string-arrays/](https://www.geeksforgeeks.org/count-equal-pairs-from-given-string-arrays/)

给定两个字符串数组 **s1[]** 和 **s2[]** 。任务是找到配对数 **(s1[i]，s2[j])** 使得 **s1[i] = s2[j]** 。**注意**一个元素 **s1[i]** 只能参与一个单对。

**示例:**

> **输入:**s1[]= {“abc”、“def”}，s2[]= {“abc”、“ABC”}
> **输出:** 1
> 唯一有效的对是(s1[0]、s2[0])或(s1[0]、s2[1])
> 注意，即使“ABC”在
> 数组 S2[]中出现两次，但它只能组成一个单对
> 因为“ABC”在数组 S1[]中只出现一次
> 
> **输入:**S1[]= {“AAA”、“AAA”}，S2[]= {“AAA”、“AAA”}
> T3】输出: 2

**进场:**

*   创建一个[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)来存储数组所有字符串的频率 **s1[]** 。
*   现在，对于数组中的每个字符串，检查映射中是否存在与当前字符串相等的字符串。
*   如果是，则增加**计数**并减少地图中字符串的频率。这是因为一个字符串只能配对一次。
*   最后打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of required pairs
int count_pairs(string s1[], string s2[], int n1, int n2)
{

    // Map to store the frequencies of
    // all the strings of array s1[]
    unordered_map<string, int> mp;

    // Update the frequencies
    for (int i = 0; i < n1; i++)
        mp[s1[i]]++;

    // To store the count of pairs
    int cnt = 0;

    // For every string of array s2[]
    for (int i = 0; i < n2; i++) {

        // If current string can make a pair
        if (mp[s2[i]] > 0) {

            // Increment the count of pairs
            cnt++;

            // Decrement the frequency of the
            // string as once occurrence has been
            // used in the current pair
            mp[s2[i]]--;
        }
    }

    // Return the count
    return cnt;
}

// Driver code
int main()
{
    string s1[] = { "abc", "def" };
    string s2[] = { "abc", "abc" };
    int n1 = sizeof(s1) / sizeof(string);
    int n2 = sizeof(s2) / sizeof(string);

    cout << count_pairs(s1, s2, n1, n2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return
    // the count of required pairs
    static int count_pairs(String s1[],
                           String s2[],
                           int n1, int n2)
    {

        // Map to store the frequencies of
        // all the strings of array s1[]
        HashMap<String,
                Integer> mp = new HashMap<String,
                                          Integer>();

        // Update the frequencies
        for (int i = 0; i < n1; i++)
            mp.put(s1[i], 0);

        // Update the frequencies
        for (int i = 0; i < n1; i++)
            mp.put(s1[i], mp.get(s1[i]) + 1);

        // To store the count of pairs
        int cnt = 0;

        // For every string of array s2[]
        for (int i = 0; i < n2; i++)
        {

            // If current string can make a pair
            if (mp.get(s2[i]) > 0)
            {

                // Increment the count of pairs
                cnt++;

                // Decrement the frequency of the
                // string as once occurrence has been
                // used in the current pair
                mp.put(s2[i], mp.get(s2[i]) - 1);
            }
        }

        // Return the count
        return cnt;
    }

    // Driver code
    public static void main (String[] args)
    {
        String s1[] = { "abc", "def" };
        String s2[] = { "abc", "abc" };
        int n1 = s1.length;
        int n2 = s2.length;

        System.out.println(count_pairs(s1, s2, n1, n2));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# python 3 implementation of the approach

# Function to return the count of required pairs
def count_pairs(s1, s2,n1,n2):
    # Map to store the frequencies of
    # all the strings of array s1[]
    mp = {s1[i]:0 for i in range(len(s1))}

    # Update the frequencies
    for i in range(n1):
        mp[s1[i]] += 1

    # To store the count of pairs
    cnt = 0

    # For every string of array s2[]
    for i in range(n2):
        # If current string can make a pair
        if (mp[s2[i]] > 0):
            # Increment the count of pairs
            cnt += 1

            # Decrement the frequency of the
            # string as once occurrence has been
            # used in the current pair
            mp[s2[i]] -= 1

    # Return the count
    return cnt

# Driver code
if __name__ == '__main__':
    s1 = ["abc", "def"]
    s2 = ["abc", "abc"]
    n1 = len(s1)
    n2 = len(s2)

    print(count_pairs(s1, s2, n1, n2))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return
    // the count of required pairs
    static int count_pairs(String []s1,
                           String []s2,
                           int n1, int n2)
    {

        // Map to store the frequencies of
        // all the strings of array s1[]
        Dictionary<String,
                   int> mp = new Dictionary<String,
                                            int>();

        // Update the frequencies
        for (int i = 0; i < n1; i++)
            mp.Add(s1[i], 0);

        // Update the frequencies
        for (int i = 0; i < n1; i++)
        {
            var v = mp[s1[i]] + 1;
            mp.Remove(s1[i]);
            mp.Add(s1[i], v);
        }

        // To store the count of pairs
        int cnt = 0;

        // For every string of array s2[]
        for (int i = 0; i < n2; i++)
        {

            // If current string can make a pair
            if (mp[s2[i]] > 0)
            {

                // Increment the count of pairs
                cnt++;

                // Decrement the frequency of the
                // string as once occurrence has been
                // used in the current pair
                if(mp.ContainsKey(s2[i]))
                {
                    var v = mp[s2[i]] - 1;
                    mp.Remove(s2[i]);
                    mp.Add(s2[i], v);
                }
                else
                    mp.Add(s2[i], mp[s2[i]] - 1);
            }
        }

        // Return the count
        return cnt;
    }

    // Driver code
    public static void Main (String[] args)
    {
        String []s1 = { "abc", "def" };
        String []s2 = { "abc", "abc" };
        int n1 = s1.Length;
        int n2 = s2.Length;

        Console.WriteLine(count_pairs(s1, s2, n1, n2));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of required pairs
function count_pairs(s1, s2, n1, n2)
{

    // Map to store the frequencies of
    // all the strings of array s1[]
    var mp = new Map();

    // Update the frequencies
    for (var i = 0; i < n1; i++)
    {
        if(mp.has(s1[i]))
        {
            mp.set(s1[i], mp.get(s1[i])+1)
        }
        else
        {
            mp.set(s1[i], 1)
        }
    }

    // To store the count of pairs
    var cnt = 0;

    // For every string of array s2[]
    for (var i = 0; i < n2; i++) {

        // If current string can make a pair
        if (mp.get(s2[i]) > 0) {

            // Increment the count of pairs
            cnt++;

            // Decrement the frequency of the
            // string as once occurrence has been
            // used in the current pair
            mp.set(s2[i], mp.get(s2[i])-1)
        }
    }

    // Return the count
    return cnt;
}

// Driver code
var s1 = ["abc", "def" ];
var s2 = ["abc", "abc" ];
var n1 = s1.length;
var n2 = s2.length;

document.write( count_pairs(s1, s2, n1, n2));

</script>
```

**Output:** 

```
1
```