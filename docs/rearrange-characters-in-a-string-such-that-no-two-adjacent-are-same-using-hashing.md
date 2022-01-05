# 使用散列法重新排列字符串中的字符，使相邻的字符不相同

> 原文:[https://www . geeksforgeeks . org/重排-字符串中的字符-这样-没有两个相邻的字符是相同的-使用哈希/](https://www.geeksforgeeks.org/rearrange-characters-in-a-string-such-that-no-two-adjacent-are-same-using-hashing/)

给定具有重复字符的字符串 **str** ，任务是重新排列字符串中的字符，使得没有两个相邻的字符相同。如果可能，则打印**是**否则打印**否**。
**示例:**

> **输入:**str = " geeks forgeks "
> T3】输出:是的
> “egeks forgeks”就是这样一种安排。
> 
> **输入:**str = " bbbbbbb "
> T3】输出:否

**方法:**思路是将每个字符的频率存储在一个[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)中，将字符的最大频率与字符串长度和最大频率数的差值进行比较。如果最大频率小于该差值，则可以不这样安排。

1.  让我们开始交替放置所有具有最大频率的字符。那么至少，我们需要它们之间的(max_freq-1)个空间来解决这个问题，这样它们就不会彼此相邻。
2.  但是我们还剩下(字符串长度–max _ freq)个空格。因此，(字符串的长度–max _ freq)应该至少为(max_freq-1)，这样就不会有两个字符相同。
3.  所以是这样的:(max_freq-1) <= (length of the string – max_freq) 

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#include <time.h>
using namespace std;

// Function that returns true if it is possible
// to rearrange the characters of the string
// such that no two consecutive characters are same
int isPossible(string str)
{

    // To store the frequency of
    // each of the character
    unordered_map<char, int> freq;

    // To store the maximum frequency so far
    int max_freq = 0;
    for (int j = 0; j < (str.length()); j++) {
        freq[str[j]]++;
        if (freq[str[j]] > max_freq)
            max_freq = freq[str[j]];
    }

    // If possible
    if (max_freq <= (str.length() - max_freq + 1))
        return true;
    return false;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    if (isPossible(str))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function that returns true if it is possible
    // to rearrange the characters of the string
    // such that no two consecutive characters are same
    static boolean isPossible(char[] str)
    {

        // To store the frequency of
        // each of the character
        Map<Character, Integer> freq = new HashMap<>();

        // To store the maximum frequency so far
        int max_freq = 0;
        for (int j = 0; j < (str.length); j++) {
            if (freq.containsKey(str[j])) {
                freq.put(str[j], freq.get(str[j]) + 1);
                if (freq.get(str[j]) > max_freq)
                    max_freq = freq.get(str[j]);
            }
            else {
                freq.put(str[j], 1);
                if (freq.get(str[j]) > max_freq)
                    max_freq = freq.get(str[j]);
            }
        }

        // If possible
        if (max_freq <= (str.length - max_freq + 1))
            return true;
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";

        if (isPossible(str.toCharArray()))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if it is possible
# to rearrange the characters of the String
# such that no two consecutive characters are same
def isPossible(Str):

    # To store the frequency of
    # each of the character
    freq = dict()

    # To store the maximum frequency so far
    max_freq = 0
    for j in range(len(Str)):
        freq[Str[j]] = freq.get(Str[j], 0) + 1
        if (freq[Str[j]] > max_freq):
            max_freq = freq[Str[j]]

    # If possible
    if (max_freq <= (len(Str) - max_freq + 1)):
        return True
    return False

# Driver code
Str = "geeksforgeeks"

if (isPossible(Str)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG {

    // Function that returns true if it is possible
    // to rearrange the characters of the string
    // such that no two consecutive characters are same
    static Boolean isPossible(char[] str)
    {

        // To store the frequency of
        // each of the character
        Dictionary<char, int> freq = new Dictionary<char, int>();

        // To store the maximum frequency so far
        int max_freq = 0;
        for (int j = 0; j < (str.Length); j++) {
            if (freq.ContainsKey(str[j])) {
                var v = freq[str[j]] + 1;
                freq.Remove(str[j]);
                freq.Add(str[j], v);
                if (freq[str[j]] > max_freq)
                    max_freq = freq[str[j]];
            }
            else {
                freq.Add(str[j], 1);
                if (freq[str[j]] > max_freq)
                    max_freq = freq[str[j]];
            }
        }

        // If possible
        if (max_freq <= (str.Length - max_freq + 1))
            return true;
        return false;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";

        if (isPossible(str.ToCharArray()))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function that returns true if it is possible
    // to rearrange the characters of the string
    // such that no two consecutive characters are same
    function isPossible(str)
    {

        // To store the frequency of
        // each of the character
        let freq = new Map();

        // To store the maximum frequency so far
        let max_freq = 0;
        for (let j = 0; j < (str.length); j++) {
            if (freq.has(str[j])) {
                freq.set(str[j], freq.get(str[j]) + 1);
                if (freq.get(str[j]) > max_freq)
                    max_freq = freq.get(str[j]);
            }
            else {
                freq.set(str[j], 1);
                if (freq.get(str[j]) > max_freq)
                    max_freq = freq.get(str[j]);
            }
        }

        // If possible
        if (max_freq <= (str.length - max_freq + 1))
            return true;
        return false;
    }

    // Driver code

     let str = "geeksforgeeks";

        if (isPossible(str.split('')))
            document.write("Yes");
        else
           document.write("No");

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)