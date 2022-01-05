# 分割字符串的方法，使得每个分区都以不同的字符开始

> 原文:[https://www . geesforgeks . org/way-split-string-partition-starts-distinct-character/](https://www.geeksforgeeks.org/ways-split-string-partition-starts-distinct-character/)

给定一根绳子 **s** 。假设 **k** 是给定字符串中可能的最大分区数，每个分区以不同的字符开头。任务是找出将字符串 s 拆分成 **k** 分区(非空)的方法，以便每个分区以不同的字符开始。
**举例:**

```
Input : s = "abb"
Output : 2
"abb" can be maximum split into 2 
partitions {a, bb} with distinct 
starting character, so k = 2\. And, 
number of ways to split "abb" into 
2 partition with distinct starting 
character is 2 that are {a, bb} and
{ab, b}.

Input : s = "acbbcc"
Output : 6
```

首先，我们需要找到 k 的值。注意，k 将等于字符串中不同字符的数量，因为只有分区的数量可以是最大的，这样每个分区都有不同的起始元素。
现在，要找到将字符串拆分成 k 个部分的方法，每个分区从不同的字符开始。首先，观察第一个分区将总是固定字符串的第一个字符，不管它有多长。现在，我们需要处理除了第一个角色之外的所有其他角色。
我们举个例子，比如说 s =“acbbcc”，上面我们已经讨论过第一个字符‘a’。现在，为了处理“b”和“c”，请注意“b”出现在字符串中的两个位置，而“c”出现在三个位置。如果我们从两个位置中选择任何一个位置作为 b，从三个位置中选择任何一个位置作为 c，那么，我们可以在这些位置对字符串进行划分。请注意，零件数量将等于 3(等于 s，即 k 中不同字符的数量)。
因此概括观察，让计数 <sub>i</sub> 是字符 I 在 s 中出现的次数。因此我们的答案将是所有 I 的计数 <sub>i</sub> 的乘积，这样 I 出现在字符串中，并且 I 不等于字符串的第一个字符。
以下是本办法的实施:

## C++

```
// CPP Program to find number of way
// to split string such that each partition
// starts with distinct character with
// maximum number of partitions.
#include <bits/stdc++.h>

using namespace std;

// Returns the number of we can split
// the string
int countWays(string s)
{
    int count[26] = { 0 };

    // Finding the frequency of each
    // character.
    for (char x : s)
        count[x - 'a']++;

    // making frequency of first character
    // of string equal to 1.
    count[s[0] - 'a'] = 1;

    // Finding the product of frequency
    // of occurrence of each character.
    int ans = 1;
    for (int i = 0; i < 26; ++i)
        if (count[i] != 0)
            ans *= count[i];

    return ans;
}

// Driven Program
int main()
{
    string s = "acbbcc";
    cout << countWays(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find number
// of way to split string such
// that each partition starts
// with distinct character with
// maximum number of partitions.
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Returns the number of we
// can split the string
static int countWays(String s)
{
    int count[] = new int[26];

    // Finding the frequency of
    // each character.
    for (int i = 0; i < s.length(); i++)
        count[s.charAt(i) - 'a']++;

    // making frequency of first
    // character of string equal to 1.
    count[s.charAt(0) - 'a'] = 1;

    // Finding the product of frequency
    // of occurrence of each character.
    int ans = 1;
    for (int i = 0; i < 26; ++i)
        if (count[i] != 0)
            ans *= count[i];

    return ans;
}

// Driver Code
public static void main(String ags[])
{
    String s = "acbbcc";
    System.out.println(countWays(s));
}
}

// This code is contributed
// by Subhadeep
```

## 蟒蛇 3

```
# Python3 Program to find number of way
# to split string such that each partition
# starts with distinct character with
# maximum number of partitions.

# Returns the number of we can split
# the string
def countWays(s):
    count = [0] * 26;

    # Finding the frequency of each
    # character.
    for x in s:
        count[ord(x) -
              ord('a')] = (count[ord(x) -
                                 ord('a')]) + 1;

    # making frequency of first character
    # of string equal to 1.
    count[ord(s[0]) - ord('a')] = 1;

    # Finding the product of frequency
    # of occurrence of each character.
    ans = 1;
    for i in range(26):
        if (count[i] != 0):
            ans *= count[i];

    return ans;

# Driver Code
if __name__ == '__main__':
    s = "acbbcc";
    print(countWays(s));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# Program to find number
// of way to split string such
// that each partition starts
// with distinct character with
// maximum number of partitions.

using System;

class GFG
{

// Returns the number of we
// can split the string
static int countWays(string s)
{
    int[] count = new int[26];

    // Finding the frequency of
    // each character.
    for (int i = 0; i < s.Length; i++)
        count[s[i] - 'a']++;

    // making frequency of first
    // character of string equal to 1.
    count[s[0] - 'a'] = 1;

    // Finding the product of frequency
    // of occurrence of each character.
    int ans = 1;
    for (int i = 0; i < 26; ++i)
        if (count[i] != 0)
            ans *= count[i];

    return ans;
}

// Driver Code
public static void Main()
{
    string s = "acbbcc";
    Console.WriteLine(countWays(s));
}
}
```

## java 描述语言

```
<script>

    // Javascript Program to find number
    // of way to split string such
    // that each partition starts
    // with distinct character with
    // maximum number of partitions.

    // Returns the number of we
    // can split the string
    function countWays(s)
    {
        let count = new Array(26);
        count.fill(0);

        // Finding the frequency of
        // each character.
        for (let i = 0; i < s.length; i++)
            count[s[i].charCodeAt() -
            'a'.charCodeAt()]++;

        // making frequency of first
        // character of string equal to 1.
        count[s[0].charCodeAt() -
        'a'.charCodeAt()] = 1;

        // Finding the product of frequency
        // of occurrence of each character.
        let ans = 1;
        for (let i = 0; i < 26; ++i)
            if (count[i] != 0)
                ans *= count[i];

        return ans;
    }

    let s = "acbbcc";
    document.write(countWays(s));

</script>
```

**Output:** 

```
6
```