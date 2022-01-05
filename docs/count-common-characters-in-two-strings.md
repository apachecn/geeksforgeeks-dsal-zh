# 统计两个字符串中的常用字符

> 原文:[https://www . geesforgeks . org/count-两个字符串中的常用字符/](https://www.geeksforgeeks.org/count-common-characters-in-two-strings/)

给定由小写英文字母组成的两个字符串 **s1** 和 **s2** ，任务是从给定的字符串中计数所有的索引对 **(i，j)** ，使得 **s1[i] = s2[j]** 和所有的索引是不同的，即如果 **s1[i]** 与一些 **s2[j]** 成对，那么这两个字符将不会与任何其他字符成对。
**例**

> **输入:**S1 =“ABCD”，S2 =“aad”
> T3】输出: 2
> (s1[0]，s2[0])和(s1[3]，s2[2])是唯一有效的对。
> (s1[0]，s2[1])不包括，因为 s1[0]已经与 s2[0]
> **配对输入:**S1 =“geeks forgeeks”，S2 =“platformforkeks”
> **输出:** 8

**方法:**统计两个字符串中所有字符的频率。现在，对于每个字符，如果该字符在字符串 **s1** 中的频率为 **freq1** ，在字符串 **s2** 中的频率为 **freq2** ，则该字符的有效对总数将为 **min(freq1，freq2)** 。所有字符的该值之和即为所需答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// valid indices pairs
int countPairs(string s1, int n1, string s2, int n2)
{

    // To store the frequencies of characters
    // of string s1 and s2
    int freq1[26] = { 0 };
    int freq2[26] = { 0 };

    // To store the count of valid pairs
    int i, count = 0;

    // Update the frequencies of
    // the characters of string s1
    for (i = 0; i < n1; i++)
        freq1[s1[i] - 'a']++;

    // Update the frequencies of
    // the characters of string s2
    for (i = 0; i < n2; i++)
        freq2[s2[i] - 'a']++;

    // Find the count of valid pairs
    for (i = 0; i < 26; i++)
        count += (min(freq1[i], freq2[i]));

    return count;
}

// Driver code
int main()
{
    string s1 = "geeksforgeeks", s2 = "platformforgeeks";
    int n1 = s1.length(), n2 = s2.length();
    cout << countPairs(s1, n1, s2, n2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of
// valid indices pairs
static int countPairs(String s1, int n1,
                        String s2, int n2)
{

    // To store the frequencies of characters
    // of string s1 and s2
    int []freq1 = new int[26];
    int []freq2 = new int[26];
    Arrays.fill(freq1, 0);
    Arrays.fill(freq2, 0);

    // To store the count of valid pairs
    int i, count = 0;

    // Update the frequencies of
    // the characters of string s1
    for (i = 0; i < n1; i++)
        freq1[s1.charAt(i) - 'a']++;

    // Update the frequencies of
    // the characters of string s2
    for (i = 0; i < n2; i++)
        freq2[s2.charAt(i) - 'a']++;

    // Find the count of valid pairs
    for (i = 0; i < 26; i++)
        count += (Math.min(freq1[i], freq2[i]));

    return count;
}

// Driver code
public static void main(String args[])
{
    String s1 = "geeksforgeeks", s2 = "platformforgeeks";
    int n1 = s1.length(), n2 = s2.length();
    System.out.println(countPairs(s1, n1, s2, n2));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# valid indices pairs
def countPairs(s1, n1, s2, n2) :

    # To store the frequencies of characters
    # of string s1 and s2
    freq1 = [0] * 26;
    freq2 = [0] * 26;

    # To store the count of valid pairs
    count = 0;

    # Update the frequencies of
    # the characters of string s1
    for i in range(n1) :
        freq1[ord(s1[i]) - ord('a')] += 1;

    # Update the frequencies of
    # the characters of string s2
    for i in range(n2) :
        freq2[ord(s2[i]) - ord('a')] += 1;

    # Find the count of valid pairs
    for i in range(26) :
        count += min(freq1[i], freq2[i]);

    return count;

# Driver code
if __name__ == "__main__" :

    s1 = "geeksforgeeks";
    s2 = "platformforgeeks";

    n1 = len(s1) ;
    n2 = len(s2);

    print(countPairs(s1, n1, s2, n2));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// valid indices pairs
static int countPairs(string s1, int n1,
                      string s2, int n2)
{

    // To store the frequencies of
    // characters of string s1 and s2
    int []freq1 = new int[26];
    int []freq2 = new int[26];
    Array.Fill(freq1, 0);
    Array.Fill(freq2, 0);

    // To store the count of valid pairs
    int i, count = 0;

    // Update the frequencies of
    // the characters of string s1
    for (i = 0; i < n1; i++)
        freq1[s1[i] - 'a']++;

    // Update the frequencies of
    // the characters of string s2
    for (i = 0; i < n2; i++)
        freq2[s2[i] - 'a']++;

    // Find the count of valid pairs
    for (i = 0; i < 26; i++)
        count += (Math.Min(freq1[i],
                           freq2[i]));

    return count;
}

// Driver code
public static void Main()
{
    string s1 = "geeksforgeeks",
           s2 = "platformforgeeks";
    int n1 = s1.Length, n2 = s2.Length;
    Console.WriteLine(countPairs(s1, n1, s2, n2));
}
}

// This code is contributed by
// Akanksha Rai
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the count of
    // valid indices pairs
    function countPairs(s1, n1, s2, n2)
    {

        // To store the frequencies of
        // characters of string s1 and s2
        let freq1 = new Array(26);
        let freq2 = new Array(26);
        freq1.fill(0);
        freq2.fill(0);

        // To store the count of valid pairs
        let i, count = 0;

        // Update the frequencies of
        // the characters of string s1
        for (i = 0; i < n1; i++)
            freq1[s1[i].charCodeAt() - 'a'.charCodeAt()]++;

        // Update the frequencies of
        // the characters of string s2
        for (i = 0; i < n2; i++)
            freq2[s2[i].charCodeAt() - 'a'.charCodeAt()]++;

        // Find the count of valid pairs
        for (i = 0; i < 26; i++)
            count += (Math.min(freq1[i], freq2[i]));

        return count;
    }

    let s1 = "geeksforgeeks", s2 = "platformforgeeks";
    let n1 = s1.length, n2 = s2.length;
    document.write(countPairs(s1, n1, s2, n2));

</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(max(n1，n2))
**辅助空间:** O(1)