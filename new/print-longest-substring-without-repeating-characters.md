# 打印无重复字符的最长子字符串

> 原文：[https://www.geeksforgeeks.org/print-longest-substring-without-repeating-characters/](https://www.geeksforgeeks.org/print-longest-substring-without-repeating-characters/)

给定一个字符串，打印最长的子字符串，而不重复字符。 例如，`ABDEFGABEF`的没有重复字符的最长子串是`BDEFGA`和`DEFGAB`，长度为 6。对于`BBBB`，最长子串是`B`，长度为 1。所需的时间复杂度为`O(n)`，其中`n`是字符串的长度。

**先决条件**：[最长子串的长度，不包含重复字符](https://www.geeksforgeeks.org/length-of-the-longest-substring-without-repeating-characters/)

**示例**：

```
Input : GEEKSFORGEEKS
Output : EKSFORG

Input : ABDEFGABEF
Output : BDEFGA

```

[Recommended : Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org)

**方法**：想法是遍历字符串，对于每个已访问的字符，将其最后一次出现存储在哈希表中（此处`unordered_map`用作哈希，键作为字符，值作为其最后位置）。 变量`st`存储当前子串的起点，`maxlen`存储最大长度子串​​的长度，`start`存储最大长度子串​​的起始索引。 在遍历字符串时，请检查哈希表中是否存在当前字符。 如果不存在，则将当前字符存储在哈希表中，并将值作为当前索引。 如果哈希表中已经存在该字符，则意味着当前字符可以在当前子字符串中重复。 对于此检查，字符的上一次出现是在当前子字符串的起点`st`之前还是之后。 如果它在`st`之前，则仅更新哈希表中的值。 如果在`st`之后，则找到当前子串`currlen`的长度为`i - st`，其中`i`是当前索引。 比较`currlen`和`maxlen`。 如果`maxlen`小于`currlen`，则将`maxlen`更新为`currlen`并从`st`开始。 完整遍历字符串后，所需的最长子字符串（不重复字符）为`s[start]`到`s [start + maxlen - 1]`。

**实现**：

## C++

```cpp

// C++ program to find and print longest
// substring without repeating characters.
#include <bits/stdc++.h>

using namespace std;

// Function to find and print longest
// substring without repeating characters.
string findLongestSubstring(string str)
{
    int i;
    int n = str.length();

    // starting point of current substring.
    int st = 0;

    // length of current substring.
    int currlen;

    // maximum length substring without repeating 
    // characters.
    int maxlen = 0;

    // starting index of maximum length substring.
    int start;

    // Hash Map to store last occurrence of each
    // already visited character.
    unordered_map<char, int> pos;

    // Last occurrence of first character is index 0;
    pos[str[0]] = 0;

    for (i = 1; i < n; i++) {

        // If this character is not present in hash,
        // then this is first occurrence of this
        // character, store this in hash.
        if (pos.find(str[i]) == pos.end())
            pos[str[i]] = i;

        else {
            // If this character is present in hash then
            // this character has previous occurrence,
            // check if that occurrence is before or after
            // starting point of current substring.
            if (pos[str[i]] >= st) {

                // find length of current substring and
                // update maxlen and start accordingly.
                currlen = i - st;
                if (maxlen < currlen) {
                    maxlen = currlen;
                    start = st;
                }

                // Next substring will start after the last
                // occurrence of current character to avoid
                // its repetition.
                st = pos[str[i]] + 1;
            }

            // Update last occurrence of
            // current character.
            pos[str[i]] = i;
        }
    }

    // Compare length of last substring with maxlen and
    // update maxlen and start accordingly.
    if (maxlen < i - st) {
        maxlen = i - st;
        start = st;
    }

    // The required longest substring without
    // repeating characters is from str[start]
    // to str[start+maxlen-1].
    return str.substr(start, maxlen);
}

// Driver function
int main()
{
    string str = "GEEKSFORGEEKS";
    cout << findLongestSubstring(str);
    return 0;
}

```

## Java

```java

// Java program to find 
// and print longest substring
// without repeating characters. 
import java.util.*; 
class GFG{

// Function to find and print longest 
// substring without repeating characters. 
public static String findLongestSubstring(String str) 
{ 
    int i; 
    int n = str.length(); 

    // Starting point 
    // of current substring. 
    int st = 0; 

    // length of 
    // current substring. 
    int currlen = 0; 

    // maximum length 
    // substring without 
    // repeating characters. 
    int maxlen = 0; 

    // starting index of 
    // maximum length substring. 
    int start = 0; 

    // Hash Map to store last 
    // occurrence of each 

    // already visited character. 
    HashMap<Character, 
            Integer> pos = new HashMap<Character, 
                                        Integer>(); 

    // Last occurrence of first 
    // character is index 0; 
    pos.put(str.charAt(0), 0); 

    for (i = 1; i < n; i++) 
    {
        // If this character is not present in hash, 
        // then this is first occurrence of this 
        // character, store this in hash. 
        if (!pos.containsKey(str.charAt(i)))
        {
            pos.put(str.charAt(i), i);
        }
        else
        { 
            // If this character is present 
            // in hash then this character 
            // has previous occurrence, 
            // check if that occurrence 
            // is before or after starting 
            // point of current substring. 
            if (pos.get(str.charAt(i)) >= st) 
            {
                // find length of current 
                // substring and update maxlen
                // and start accordingly. 
                currlen = i - st; 
                if (maxlen < currlen) 
                { 
                maxlen = currlen; 
                start = st; 
                } 

                // Next substring will start 
                // after the last occurrence 
                // of current character to avoid 
                // its repetition. 
                st = pos.get(str.charAt(i)) + 1; 
            } 

            // Update last occurrence of 
            // current character. 
            pos.replace(str.charAt(i), i);
        } 
    } 

    // Compare length of last 
    // substring with maxlen and 
    // update maxlen and start 
    // accordingly. 
    if (maxlen < i - st) 
    { 
        maxlen = i - st; 
        start = st; 
    } 

    // The required longest 
    // substring without 
    // repeating characters 
    // is from str[start] 
    // to str[start+maxlen-1]. 
    return str.substring(start, 
                         start + 
                         maxlen); 
} 

// Driver Code
public static void main(String[] args) 
{
    String str = "GEEKSFORGEEKS";
    System.out.print(findLongestSubstring(str));
}
}

// This code is contributed by divyeshrabadiya07

```

## Python3

```py

# Python3 program to find and print longest 
# substring without repeating characters. 

# Function to find and print longest 
# substring without repeating characters. 
def findLongestSubstring(string):

    n = len(string) 

    # starting point of current substring. 
    st = 0

    # maximum length substring without 
    # repeating characters. 
    maxlen = 0

    # starting index of maximum 
    # length substring. 
    start = 0

    # Hash Map to store last occurrence 
    # of each already visited character. 
    pos = {} 

    # Last occurrence of first
    # character is index 0 
    pos[string[0]] = 0

    for i in range(1, n): 

        # If this character is not present in hash, 
        # then this is first occurrence of this 
        # character, store this in hash. 
        if string[i] not in pos: 
            pos[string[i]] = i 

        else:
            # If this character is present in hash then 
            # this character has previous occurrence, 
            # check if that occurrence is before or after 
            # starting point of current substring. 
            if pos[string[i]] >= st: 

                # find length of current substring and 
                # update maxlen and start accordingly. 
                currlen = i - st 
                if maxlen < currlen: 
                    maxlen = currlen 
                    start = st 

                # Next substring will start after the last 
                # occurrence of current character to avoid 
                # its repetition. 
                st = pos[string[i]] + 1

            # Update last occurrence of 
            # current character. 
            pos[string[i]] = i 

    # Compare length of last substring with maxlen 
    # and update maxlen and start accordingly. 
    if maxlen < i - st: 
        maxlen = i - st 
        start = st 

    # The required longest substring without 
    # repeating characters is from string[start] 
    # to string[start+maxlen-1]. 
    return string[start : start + maxlen] 

# Driver Code
if __name__ == "__main__": 

    string = "GEEKSFORGEEKS"
    print(findLongestSubstring(string)) 

# This code is contributed by Rituraj Jain

```

## C#

```cs

// C# program to find 
// and print longest substring
// without repeating characters. 
using System;
using System.Collections.Generic;
class GFG{

// Function to find and 
// print longest substring 
// without repeating characters. 
public static String findlongestSubstring(String str) 
{ 
  int i; 
  int n = str.Length; 

  // Starting point 
  // of current substring. 
  int st = 0; 

  // length of 
  // current substring. 
  int currlen = 0; 

  // maximum length 
  // substring without 
  // repeating characters. 
  int maxlen = 0; 

  // starting index of 
  // maximum length substring. 
  int start = 0; 

  // Hash Map to store last 
  // occurrence of each 

  // already visited character. 
  Dictionary<char, 
             int> pos = new Dictionary<char, 
                                       int>();

  // Last occurrence of first 
  // character is index 0; 
  pos.Add(str[0], 0); 

  for (i = 1; i < n; i++) 
  {
    // If this character is not present in hash, 
    // then this is first occurrence of this 
    // character, store this in hash. 
    if (!pos.ContainsKey(str[i]))
    {
      pos.Add(str[i], i);
    }
    else
    { 
      // If this character is present 
      // in hash then this character 
      // has previous occurrence, 
      // check if that occurrence 
      // is before or after starting 
      // point of current substring. 
      if (pos[str[i]] >= st) 
      {
        // find length of current 
        // substring and update maxlen
        // and start accordingly. 
        currlen = i - st; 
        if (maxlen < currlen) 
        { 
          maxlen = currlen; 
          start = st; 
        } 

        // Next substring will start 
        // after the last occurrence 
        // of current character to avoid 
        // its repetition. 
        st = pos[str[i]] + 1; 
      } 

      // Update last occurrence of 
      // current character. 
      pos[str[i]] = i;
    } 
  } 

  // Compare length of last 
  // substring with maxlen and 
  // update maxlen and start 
  // accordingly. 
  if (maxlen < i - st) 
  { 
    maxlen = i - st; 
    start = st; 
  } 

  // The required longest 
  // substring without 
  // repeating characters 
  // is from str[start] 
  // to str[start+maxlen-1]. 
  return str.Substring(start,  
                       maxlen); 
} 

// Driver Code
public static void Main(String[] args) 
{
  String str = "GEEKSFORGEEKS";
  Console.Write(findlongestSubstring(str));
}
}

// This code is contributed by shikhasingrajput

```

**输出**：

```
EKSFORG 

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



