# 将一个字符串拆分成最大数量的唯一子字符串

> 原文:[https://www . geesforgeks . org/split-a-string-in-max-number-unique-substrings/](https://www.geeksforgeeks.org/split-a-string-into-maximum-number-of-unique-substrings/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是将该字符串拆分成最大数量的唯一[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)**并打印它们的计数。**

****示例:****

> ****输入:** str = "ababccc"
> **输出:** 5
> **解释:**
> 将给定的字符串拆分为子字符串“a”、“b”、“ab”、“c”和“cc”。
> 因此，唯一子串的最大计数为 5。**
> 
> ****输入:**str = " ABA "
> T3】输出: 2**

****进场:**问题可以通过[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:**

1.  **初始化一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)T2。**
2.  **[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **字符串**的字符，并为每个 **i** 找到该索引的子字符串。**
3.  **如果给定的子串不在[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)**S**[中，则插入](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)更新最大计数，[将其从集合](https://www.geeksforgeeks.org/seterase-c-stl/)中移除，因为同一字符不能重复使用。**
4.  **返回最大计数。**

**下面是上述方法的实现:**

## **C++**

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Utility function to find maximum count of
// unique substrings by splitting the string
int maxUnique(string S, set<string> st)
{

  // Stores maximum count of unique substring
  // by splitting the string into substrings
  int mx = 0;

  // Iterate over the characters of the string
  for (int i = 1; i <= S.length(); i++)
  {

    // Stores prefix substring
    string tmp = S.substr(0, i);

    // Check if the current substring
    // already exists
    if (st.find(tmp) == st.end())
    {

      // Insert tmp into set
      st.insert(tmp);

      // Recursively call for remaining
      // characters of string
      mx = max(mx, maxUnique(S.substr(i), st) + 1);

      // Remove from the set
      st.erase(tmp);
    }
  }

  // Return answer
  return mx;
}

// Function to find the maximum count of
// unique substrings by splitting a string
// into maximum number of unique substrings
int maxUniqueSplit(string S)
{
  set<string> st;
  return maxUnique(S, st);
}

// Driver Code
int main()
{
  string S = "ababccc";
  int res = maxUniqueSplit(S);

  cout<<res;
}

// This code is contributed by jana_sayantan.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class Solution {

    // Function to find the maximum count of
    // unique substrings by splitting a string
    // into maximum number of unique substrings
    public int maxUniqueSplit(String S)
    {
        return maxUnique(S, new HashSet<String>());
    }

    // Utility function to find maximum count of
    // unique substrings by splitting the string
    public int maxUnique(String S, Set<String> set)
    {

        // Stores maximum count of unique substring
        // by splitting the string into substrings
        int max = 0;

        // Iterate over the characters of the string
        for (int i = 1; i <= S.length(); i++) {

            // Stores prefix substring
            String tmp = S.substring(0, i);

            // Check if the current substring
            // already exists
            if (!set.contains(tmp)) {

                // Insert tmp into set
                set.add(tmp);

                // Recursively call for remaining
                // characters of string
                max = Math.max(max, maxUnique(
                                        S.substring(i), set)
                                        + 1);

                // Remove from the set
                set.remove(tmp);
            }
        }

        // Return answer
        return max;
    }
}

// Driver Code
class GFG {

    public static void main(String[] args)
    {
        Solution st = new Solution();
        String S = "ababccc";
        int res = st.maxUniqueSplit(S);

        System.out.println(res);
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Utility function to find maximum count of
# unique substrings by splitting the string
def maxUnique(S):
    global d

    # Stores maximum count of unique substring
    # by splitting the string into substrings
    maxm = 0

    # Iterate over the characters of the string
    for i in range(1, len(S) + 1):

        # Stores prefix substring
        tmp = S[0:i]

        # Check if the current substring
        # already exists
        if (tmp not in d):

            # Insert tmp into set
            d[tmp] = 1

            # Recursively call for remaining
            # characters of string
            maxm = max(maxm, maxUnique(S[i:]) + 1)

            # Remove from the set
            del d[tmp]

    # Return answer
    return maxm

# Driver Code
if __name__ == '__main__':

    # Solution st = new Solution()
    S = "ababccc"
    d = {}
    res = maxUnique(S)
    # d = {}

    print(res)

# This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

  // Function to find the maximum count of
  // unique substrings by splitting a string
  // into maximum number of unique substrings
  public int maxUniqueSplit(String S)
  {
    return maxUnique(S, new HashSet<String>());
  }

  // Utility function to find maximum count of
  // unique substrings by splitting the string
  public int maxUnique(String S, HashSet<String> set)
  {

    // Stores maximum count of unique substring
    // by splitting the string into substrings
    int max = 0;

    // Iterate over the characters of the string
    for (int i = 1; i <= S.Length; i++) {

      // Stores prefix substring
      String tmp = S.Substring(0, i);

      // Check if the current substring
      // already exists
      if (!set.Contains(tmp)) {

        // Insert tmp into set
        set.Add(tmp);

        // Recursively call for remaining
        // characters of string
        max = Math.Max(max, maxUnique(
          S.Substring(i), set)
                       + 1);

        // Remove from the set
        set.Remove(tmp);
      }
    }

    // Return answer
    return max;
  }
}

// Driver Code
public class GFG {

  public static void Main(String[] args)
  {
    Solution st = new Solution();
    String S = "ababccc";
    int res = st.maxUniqueSplit(S);

    Console.WriteLine(res);
  }
}

// This code contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Utility function to find maximum count of
// unique substrings by splitting the string
function maxUnique(S, st)
{

  // Stores maximum count of unique substring
  // by splitting the string into substrings
  var mx = 0;

  // Iterate over the characters of the string
  for (var i = 1; i <= S.length; i++)
  {

    // Stores prefix substring
    var tmp = S.substring(0, i);

    // Check if the current substring
    // already exists
    if (!st.has(tmp))
    {

      // Insert tmp into set
      st.add(tmp);

      // Recursively call for remaining
      // characters of string
      mx = Math.max(mx, maxUnique(S.substring(i), st) + 1);

      // Remove from the set
      st.delete(tmp);
    }
  }

  // Return answer
  return mx;
}

// Function to find the maximum count of
// unique substrings by splitting a string
// into maximum number of unique substrings
function maxUniqueSplit(S)
{
  var st = new Set();
  return maxUnique(S, st);
}

// Driver Code
var S = "ababccc";
var res = maxUniqueSplit(S);
document.write( res);

</script>
```

****Output:** 

```
5
```** 

*****时间复杂度:** O(* ![2^N  ](img/2f4905fd3477679aa0472880a249804e.png "Rendered by QuickLaTeX.com") * )***

*****辅助空间:** O(N)***