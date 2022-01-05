# 检查一个字符串是否包含另一个字符串的字谜作为其子字符串

> 原文:[https://www . geesforgeks . org/check-if-a-string-contains-a-anagram-of-other-string-as-it-substring/](https://www.geeksforgeeks.org/check-if-a-string-contains-an-anagram-of-another-string-as-its-substring/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/)**【S1】**和 **S2** ，任务是检查 **S2** 是否包含 **S1** 的字谜作为其[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)。

**例:**

> **输入:**S1 =“ab”，S2 =“bbpobac”
> **输出:**是
> **说明:**字符串 S2 包含 S1 的字谜“ba”(“ba”)。
> 
> **输入:**S1 =“ab”，S2 =“cbddoo”
> T3】输出:否

**方法:**按照以下步骤解决问题:

1.  初始化两个[hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)**S1 hash**和 **s2hash** ，存储两个字符串的字母出现频率。
2.  如果 **S1** 的长度大于 **S2** 的长度，则打印**“否”**。
3.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**【S1】**的字符，更新 **s1hash** 。
4.  [使用**滑动窗口**技术迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S2** 的字符，并相应地更新哈希表。
5.  对于长度等于 S1 长度的 S2 子串，如果发现两个 Hashmaps 相等，则打印**“是”**。
6.  否则，打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if string s2
// contains anagram of the string
// s1 as its substring
bool checkAnagram(string s1, string s2)
{
    // Stores frequencies of
    // characters in substrings of s2
    vector<int> s2hash(26, 0);

    // Stores frequencies of
    // characters in s1
    vector<int> s1hash(26, 0);
    int s1len = s1.size();
    int s2len = s2.size();

    // If length of s2 exceeds length of s1
    if (s1len > s2len)
        return false;

    int left = 0, right = 0;

    // Store frequencies of characters in first
    // substring of length s1len in string s2
    while (right < s1len) {

        s1hash[s1[right] - 'a'] += 1;
        s2hash[s2[right] - 'a'] += 1;
        right++;
    }

    right -= 1;

    // Perform Sliding Window technique
    while (right < s2len) {

        // If hashmaps are found to be
        // identical for any substring
        if (s1hash == s2hash)
            return true;

        right++;

        if (right != s2len)
            s2hash[s2[right] - 'a'] += 1;

        s2hash[s2[left] - 'a'] -= 1;
        left++;
    }
    return false;
}

// Driver Code
int main()
{
    string s1 = "ab";
    string s2 = "bbpobac";

    if (checkAnagram(s1, s2))
        cout << "YES\n";
    else
        cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to check if string s2
  // contains anagram of the string
  // s1 as its substring
  public static boolean checkAnagram(String s1, String s2)
  {

    // Stores frequencies of
    // characters in substrings of s2
    int s2hash[] = new int[26];

    // Stores frequencies of
    // characters in s1
    int s1hash[] = new int[26];
    int s1len = s1.length();
    int s2len = s2.length();

    // If length of s2 exceeds length of s1
    if (s1len > s2len)
      return false;
    int left = 0, right = 0;

    // Store frequencies of characters in first
    // substring of length s1len in string s2
    while (right < s1len)
    {
      s1hash[s1.charAt(right) - 'a'] += 1;
      s2hash[s2.charAt(right) - 'a'] += 1;
      right++;
    }

    right -= 1;

    // Perform Sliding Window technique
    while (right < s2len) {

      // If hashmaps are found to be
      // identical for any substring
      if (Arrays.equals(s1hash, s2hash))
        return true;

      right++;

      if (right != s2len)
        s2hash[s2.charAt(right) - 'a'] += 1;

      s2hash[s2.charAt(left) - 'a'] -= 1;
      left++;
    }
    return false;
  }

  // Driver Code
  public static void main(String[] args)
  {

    String s1 = "ab";
    String s2 = "bbpobac";

    if (checkAnagram(s1, s2))
      System.out.println("YES");
    else
      System.out.println("No");
  }
}

// This code is contributed by kingash.
```

## 蟒蛇 3

```
# Python 3 Program to implement
# the above approach

# Function to check if string s2
# contains anagram of the string
# s1 as its substring
def checkAnagram(s1, s2):
    # Stores frequencies of
    # characters in substrings of s2
    s2hash = [0 for i in range(26)]

    # Stores frequencies of
    # characters in s1
    s1hash = [0 for i in range(26)]
    s1len = len(s1)
    s2len = len(s2)

    # If length of s2 exceeds length of s1
    if (s1len > s2len):
        return False

    left = 0
    right = 0

    # Store frequencies of characters in first
    # substring of length s1len in string s2
    while (right < s1len):
        s1hash[ord(s1[right]) - 97] += 1
        s2hash[ord(s2[right]) - 97] += 1
        right += 1

    right -= 1

    # Perform Sliding Window technique
    while (right < s2len):
        # If hashmaps are found to be
        # identical for any substring
        if (s1hash == s2hash):
            return True
        right += 1

        if (right != s2len):
            s2hash[ord(s2[right]) - 97] += 1

        s2hash[ord(s2[left]) - 97] -= 1
        left += 1

    return False

# Driver Code
if __name__ == '__main__':
    s1 = "ab"
    s2 = "bbpobac"

    if (checkAnagram(s1, s2)):
        print("YES")
    else:
        print("No")

        # This code is contributed by ipg2016107
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to check if string s2
// contains anagram of the string
// s1 as its substring
static bool checkAnagram(string s1, string s2)
{
    // Stores frequencies of
    // characters in substrings of s2
    List<int> s2hash = new List<int>();
    for(int i=0;i<26;i++)
        s2hash.Add(0);

    // Stores frequencies of
    // characters in s1
    List<int> s1hash = new List<int>();
    for(int i=0;i<26;i++)
        s1hash.Add(0);
    int s1len = s1.Length;
    int s2len = s2.Length;

    // If length of s2 exceeds length of s1
    if (s1len > s2len)
        return false;

    int left = 0, right = 0;

    // Store frequencies of characters in first
    // substring of length s1len in string s2
    while (right < s1len) {

        s1hash[s1[right] - 'a'] += 1;
        s2hash[s2[right] - 'a'] += 1;
        right++;
    }

    right -= 1;

    // Perform Sliding Window technique
    while (right < s2len) {

        // If hashmaps are found to be
        // identical for any substring
        if (s1hash == s2hash)
            return true;

        right++;

        if(right != s2len)
            s2hash[s2[right] - 'a'] += 1;

        s2hash[s2[left] - 'a'] -= 1;
        left++;
    }
    return false;
}

// Driver Code
public static void Main()
{
    string s1 = "ab";
    string s2 = "bbpobac";

    if (checkAnagram(s1, s2)==true)
        Console.WriteLine("NO");
    else
        Console.WriteLine("YES");
}
}

// This code is contributed by bgangawar59.
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to check if string s2
// contains anagram of the string
// s1 as its substring
function checkAnagram(s1, s2)
{
    // Stores frequencies of
    // characters in substrings of s2
    var s2hash = Array(26).fill(0);

    // Stores frequencies of
    // characters in s1
    var s1hash = Array(26).fill(0);
    var s1len = s1.length;
    var s2len = s2.length;

    // If length of s2 exceeds length of s1
    if (s1len > s2len)
        return false;

    var left = 0, right = 0;

    // Store frequencies of characters in first
    // substring of length s1len in string s2
    while (right < s1len) {

        s1hash[s1[right].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;
        s2hash[s2[right].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;
        right++;
    }

    right -= 1;

    // Perform Sliding Window technique
    while (right < s2len) {

        var ans = true;

        // If hashmaps are found to be
        // identical for any substring
        for(var i =0; i<26; i++)
        {
            if(s1hash[i]!=s2hash[i])
            {
                ans = false;
            }
        }

        if(ans)
            return true;

        right++;

        if (right != s2len)
            s2hash[s2[right].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;

        s2hash[s2[left].charCodeAt(0) - 'a'.charCodeAt(0)] -= 1;
        left++;
    }
    return false;
}

// Driver Code
var s1 = "ab";
var s2 = "bbpobac";
if (checkAnagram(s1, s2))
    document.write( "YES");
else
    document.write( "No");

// This code is contributed by importantly.
</script>
```

**Output:** 

```
YES
```

**时间复杂度:**O(26 * len(S2))
T3】辅助空间: O(26)