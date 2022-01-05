# s[I]和 s[j]是字谜的索引对的数量

> 原文:[https://www . geesforgeks . org/index-pairs-so-si-and-SJ-is-anagrams/](https://www.geeksforgeeks.org/number-of-index-pairs-such-that-si-and-sj-are-anagrams/)

给定一个由 **N** 根弦组成的数组 **s[]** 。任务是找到指数对 **(i，j)** 的数量，使得 **s[i]** 是 **s[j]** 的[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。

**示例:**

> **输入:**s[]= {“aaab”、“aaba”、“cde”、“dec”}
> **输出:**2
> (“aaab”、“aaba”)和(“cde”、“dec”)是唯一有效的对。
> 
> **输入:**s[]= {“ab”、“bc”、“CD”}
> **输出:** 0

**方法:**一个有效的方法是[对每个字符串进行排序](https://www.geeksforgeeks.org/merge-sort/)，并在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中增加其计数。对于地图中的每个字符串，如果 **k** 是其计数，则**(k *(k–1))/2**是有效对的数量。

下面是上述方法的实现:

## C++

```
// CPP program to find number of pairs of integers
// i, j such that s[i] is an anagram of s[j].
#include <bits/stdc++.h>
using namespace std;

// Function to find number of pairs of integers
// i, j such that s[i] is an anagram of s[j].
int anagram_pairs(vector<string> s, int n)
{
    // To store count of strings
    map<string, int> mp;

    // Traverse all strings and store in the map
    for (int i = 0; i < n; i++) {
        // Sort the string
        sort(s[i].begin(), s[i].end());

        // Store in the map
        mp[s[i]]++;
    }

    // To store the number of pairs
    int ans = 0;

    // Traverse through the map
    for (auto i = mp.begin(); i != mp.end(); i++) {
        int k = i->second;

        // Count the pairs for each string
        ans += (k * (k - 1)) / 2;
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    vector<string> s = { "aaab", "aaba", "baaa",
                         "cde", "dec" };

    int n = s.size();

    // Function call
    cout << anagram_pairs(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of pairs of integers
// i, j such that s[i] is an anagram of s[j].
import java.util.*;
class GFG
{

// Function to find number of pairs of integers
// i, j such that s[i] is an anagram of s[j].
static int anagram_pairs(String []s, int n)
{
    // To store count of strings
    Map<String, Integer> mp = new HashMap<>();

    // Traverse all strings and store in the map
    for (int i = 0; i < n; i++)
    {
        // Sort the string
        char []chArr = s[i].toCharArray();
        Arrays.sort(chArr);
        s[i] = new String(chArr);

        // Store in the map
        if(mp.containsKey(s[i]))
        {
            mp.put(s[i], mp.get(s[i]) + 1);
        }
        else
        {
            mp.put(s[i], 1);
        }
    }

    // To store the number of pairs
    int ans = 0;

    // Traverse through the map
    for (Map.Entry<String,
                   Integer> i : mp.entrySet())
    {
        int k = i.getValue();

        // Count the pairs for each string
        ans += (k * (k - 1)) / 2;
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String []args)
{
    String [] s = { "aaab", "aaba", "baaa",
                            "cde", "dec" };

    int n = s.length;

    // Function call
    System.out.println(anagram_pairs(s, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find 
# number of pairs of integers i, j 
# such that s[i] is an anagram of s[j]. 

# Function to find number of pairs of integers 
# i, j such that s[i] is an anagram of s[j].
def anagram_pairs(s, n):
    # To store the count of sorted strings
    mp = dict()

    # Traverse all strings and store in the map
    for i in range(n):
        # Sort the string
        temp_str = "".join(sorted(s[i]))

        # If string exists in map, increment count
        # Else create key value pair with count = 1
        if temp_str in mp:
            mp[temp_str] += 1
        else:
            mp[temp_str] = 1

    # To store the number of pairs
    ans = 0

    # Traverse through the map
    for k in mp.values():

        # Count the pairs for each string
        ans += (k * (k - 1)) // 2

    # Return the required answer
    return ans

# Driver code
if __name__ == "__main__":
    s = ["aaab", "aaba", "baaa", "cde", "dec"]
    n = len(s)

    print(anagram_pairs(s, n))

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find number of pairs of integers
// i, j such that s[i] is an anagram of s[j].
using System;
using System.Collections.Generic;

class GFG
{

// Function to find number of pairs of integers
// i, j such that s[i] is an anagram of s[j].
static int anagram_pairs(String []s, int n)
{
    // To store count of strings
    Dictionary<String,
               int> mp = new Dictionary<String,
                                        int>();

    // Traverse all strings and store in the map
    for (int i = 0; i < n; i++)
    {
        // Sort the string
        char []chArr = s[i].ToCharArray();
        Array.Sort(chArr);
        s[i] = new String(chArr);

        // Store in the map
        if(mp.ContainsKey(s[i]))
        {
            mp[s[i]] = mp[s[i]] + 1;
        }
        else
        {
            mp.Add(s[i], 1);
        }
    }

    // To store the number of pairs
    int ans = 0;

    // Traverse through the map
    foreach (KeyValuePair<String,
                    int> i in mp)
    {
        int k = i.Value;

        // Count the pairs for each string
        ans += (k * (k - 1)) / 2;
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void Main(String []args)
{
    String [] s = { "aaab", "aaba", "baaa",
                            "cde", "dec" };

    int n = s.Length;

    // Function call
    Console.WriteLine(anagram_pairs(s, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find number of pairs of integers
// i, j such that s[i] is an anagram of s[j].

// Function to find number of pairs of integers
// i, j such that s[i] is an anagram of s[j].
function anagram_pairs(s, n)
{
    // To store count of strings
    let mp = new Map();

    // Traverse all strings and store in the map
    for (let i = 0; i < n; i++) {
        // Sort the string
        let chArr = s[i].split("");
        chArr.sort();
        s[i] = chArr.join("");

        // Store in the map
        if(mp.has(s[i])){
            mp.set(s[i], mp.get(s[i]) + 1)
        }else{
            mp.set(s[i], 1)
        }
    }

    // To store the number of pairs
    let ans = 0;

    // Traverse through the map
    for (let i of mp) {
        let k = i[1];

        // Count the pairs for each string
        ans += Math.floor((k * (k - 1)) / 2);
    }

    // Return the required answer
    return ans;
}

// Driver code
    let s = [ "aaab", "aaba", "baaa", "cde", "dec" ];

    let n = s.length;

    // Function call
    document.write(anagram_pairs(s, n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(n <sup>2</sup> * logn)

**辅助空间:** O(n)