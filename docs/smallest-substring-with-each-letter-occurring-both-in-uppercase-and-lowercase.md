# 每个字母都以大写和小写出现的最小子串

> 原文:[https://www . geesforgeks . org/minist-substring-with-每个字母都出现-大写和小写并存/](https://www.geeksforgeeks.org/smallest-substring-with-each-letter-occurring-both-in-uppercase-and-lowercase/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是在 **S** 中找到最小的**平衡子字符串**。如果不存在这样的子串，打印 **-1** 。

> 如果字符串中的每个字母都以大写和小写形式出现，则该字符串是平衡的，即“AabB”是平衡的字符串，而“Ab”不是平衡的字符串。

**示例:**

> **输入:**S = " azababba "
> T3】输出: ABaab
> **解释:**
> 子串{S[2]，…，S[6]} ( *基于 0 的索引*)是平衡的最小子串。
> 
> **输入:**S = " Technocat "
> T3】输出: -1

**朴素方法:**最简单的方法是[生成给定字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的所有可能的子串，并检查是否存在满足给定条件的子串。打印所有这些子字符串中最小的一个。

***时间复杂度:**T3】O(N<sup>3</sup>)
*T8】辅助空间:T10】O(N)**

**高效途径:**优化上述途径，思路是使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)的概念。按照以下步骤解决问题:

*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并将输入字符串中只有小写或大写形式的字符存储在[地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **地图**中。
*   初始化两个数组来跟踪到目前为止获得的小写和大写字符。
*   现在，[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)保持两个指针 **i** 和 **st** (用 **0** 初始化)，其中 **st** 将指向当前子字符串的开始，而 **i** 将指向当前字符。
    *   如果当前字符在 **mp** 中，忽略目前获得的所有字符，从下一个字符开始，并相应地调整数组。
    *   如果当前字符不在 **mp** 中，则借助 **st** 指针去除子串开头多余的字符，这样任何字符的频率都不会转换为 **0** 并相应调整数组。
    *   现在，检查子字符串 **{S[st]，…..，S[i]}** 是否平衡。如果平衡并且**I–ST+1**小于目前获得的平衡子串的长度。更新长度并存储子串的开始和结束索引，即 **st** 和 **i** 。
    *   重复这些步骤，直到字符串结束。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the current
// string is balanced or not
bool balanced(int small[], int caps[])
{
    // For every character, check if
    // there exists uppercase as well
    // as lowercase characters
    for (int i = 0; i < 26; i++) {

        if (small[i] != 0 && (caps[i] == 0))
            return 0;

        else if ((small[i] == 0) && (caps[i] != 0))
            return 0;
    }
    return 1;
}

// Function to find smallest length substring
// in the given string which is balanced
void smallestBalancedSubstring(string s)
{

    // Store frequency of
    // lowercase characters
    int small[26];

    // Stores frequency of
    // uppercase characters
    int caps[26];

    memset(small, 0, sizeof(small));
    memset(caps, 0, sizeof(caps));

    // Count frequency of characters
    for (int i = 0; i < s.length(); i++) {

        if (s[i] >= 65 && s[i] <= 90)
            caps[s[i] - 'A']++;
        else
            small[s[i] - 'a']++;
    }

    // Mark those characters which
    // are not present in both
    // lowercase and uppercase
    unordered_map<char, int> mp;
    for (int i = 0; i < 26; i++) {

        if (small[i] && !caps[i])
            mp[char(i + 'a')] = 1;

        else if (caps[i] && !small[i])
            mp[char(i + 'A')] = 1;
    }

    // Initialize the frequencies
    // back to 0
    memset(small, 0, sizeof(small));
    memset(caps, 0, sizeof(caps));

    // Marks the start and
    // end of current substring
    int i = 0, st = 0;

    // Marks the start and end
    // of required substring
    int start = -1, end = -1;

    // Stores the length of
    // smallest balanced substring
    int minm = INT_MAX;

    while (i < s.length()) {
        if (mp[s[i]]) {

            // Remove all characters
            // obtained so far
            while (st < i) {

                if (s[st] >= 65 && s[st] <= 90)
                    caps[s[st] - 'A']--;
                else
                    small[s[st] - 'a']--;

                st++;
            }
            i += 1;
            st = i;
        }
        else {

            if (s[i] >= 65 && s[i] <= 90)
                caps[s[i] - 'A']++;
            else
                small[s[i] - 'a']++;

            // Remove extra characters from
            // front of the current substring
            while (1) {

                if (s[st] >= 65 && s[st] <= 90
                    && caps[s[st] - 'A'] > 1) {
                    caps[s[st] - 'A']--;
                    st++;
                }
                else if (s[st] >= 97 && s[st] <= 122
                         && small[s[st] - 'a'] > 1) {
                    small[s[st] - 'a']--;
                    st++;
                }
                else
                    break;
            }

            // If substring (st, i) is balanced
            if (balanced(small, caps)) {

                if (minm > (i - st + 1)) {

                    minm = i - st + 1;
                    start = st;
                    end = i;
                }
            }
            i += 1;
        }
    }

    // No balanced substring
    if (start == -1 || end == -1)
        cout << -1 << endl;

    // Store answer string
    else {

        string ans = "";
        for (int i = start; i <= end; i++)
            ans += s[i];
        cout << ans << endl;
    }
}

// Driver Code
int main()
{

    // Given string
    string s = "azABaabba";

    smallestBalancedSubstring(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check if the current
// string is balanced or not
static boolean balanced(int small[],
                        int caps[])
{

    // For every character, check if
    // there exists uppercase as well
    // as lowercase characters
    for(int i = 0; i < 26; i++)
    {
        if (small[i] != 0 && (caps[i] == 0))
            return false;

        else if ((small[i] == 0) && (caps[i] != 0))
            return false;
    }
    return true;
}

// Function to find smallest length substring
// in the given string which is balanced
static void smallestBalancedSubstring(String s)
{

    // Store frequency of
    // lowercase characters
    int[] small = new int[26];

    // Stores frequency of
    // uppercase characters
    int[] caps = new int[26];

    Arrays.fill(small, 0);
    Arrays.fill(caps, 0);

    // Count frequency of characters
    for(int i = 0; i < s.length(); i++)
    {
        if (s.charAt(i) >= 65 && s.charAt(i) <= 90)
            caps[s.charAt(i) - 'A']++;
        else
            small[s.charAt(i) - 'a']++;
    }

    // Mark those characters which
    // are not present in both
    // lowercase and uppercase
    Map<Character,
        Integer> mp = new HashMap<Character,
                                  Integer>();

    for(int i = 0; i < 26; i++)
    {
        if (small[i] != 0 && caps[i] == 0)
            mp.put((char)(i + 'a'), 1);
        else if (caps[i] != 0 && small[i] == 0)
            mp.put((char)(i + 'A'), 1);
        // mp[char(i + 'A')] = 1;
    }

    // Initialize the frequencies
    // back to 0
    Arrays.fill(small, 0);
    Arrays.fill(caps, 0);

    // Marks the start and
    // end of current substring
    int i = 0, st = 0;

    // Marks the start and end
    // of required substring
    int start = -1, end = -1;

    // Stores the length of
    // smallest balanced substring
    int minm = Integer.MAX_VALUE;

    while (i < s.length())
    {
        if (mp.get(s.charAt(i)) != null)
        {

            // Remove all characters
            // obtained so far
            while (st < i)
            {
                if (s.charAt(st) >= 65 &&
                    s.charAt(st) <= 90)
                    caps[s.charAt(st) - 'A']--;
                else
                    small[s.charAt(st) - 'a']--;

                st++;
            }
            i += 1;
            st = i;
        }
        else
        {
            if (s.charAt(i) >= 65 && s.charAt(i) <= 90)
                caps[s.charAt(i) - 'A']++;
            else
                small[s.charAt(i) - 'a']++;

            // Remove extra characters from
            // front of the current substring
            while (true)
            {
                if (s.charAt(st) >= 65 &&
                    s.charAt(st) <= 90 &&
                    caps[s.charAt(st) - 'A'] > 1)
                {
                    caps[s.charAt(st) - 'A']--;
                    st++;
                }
                else if (s.charAt(st) >= 97 &&
                         s.charAt(st) <= 122 &&
                         small[s.charAt(st) - 'a'] > 1)
                {
                    small[s.charAt(st) - 'a']--;
                    st++;
                }
                else
                    break;
            }

            // If substring (st, i) is balanced
            if (balanced(small, caps))
            {
                if (minm > (i - st + 1))
                {
                    minm = i - st + 1;
                    start = st;
                    end = i;
                }
            }
            i += 1;
        }
    }

    // No balanced substring
    if (start == -1 || end == -1)
        System.out.println(-1);

    // Store answer string
    else
    {
        String ans = "";
        for(int j = start; j <= end; j++)
            ans += s.charAt(j);

        System.out.println(ans);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given string
    String s = "azABaabba";

    smallestBalancedSubstring(s);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# python 3 program for the above approach
import sys

# Function to check if the current
# string is balanced or not
def balanced(small, caps):

    # For every character, check if
    # there exists uppercase as well
    # as lowercase characters
    for i in range(26):
        if (small[i] != 0 and (caps[i] == 0)):
            return 0

        elif((small[i] == 0) and (caps[i] != 0)):
            return 0
    return 1

# Function to find smallest length substring
# in the given string which is balanced
def smallestBalancedSubstring(s):

    # Store frequency of
    # lowercase characters
    small = [0 for i in range(26)]

    # Stores frequency of
    # uppercase characters
    caps = [0 for i in range(26)]

    # Count frequency of characters
    for i in range(len(s)):
        if (ord(s[i]) >= 65 and ord(s[i]) <= 90):
            caps[ord(s[i]) - 65] += 1
        else:
            small[ord(s[i]) - 97] += 1

    # Mark those characters which
    # are not present in both
    # lowercase and uppercase
    mp = {}
    for i in range(26):
        if (small[i] and caps[i]==0):
            mp[chr(i + 97)] = 1

        elif (caps[i] and small[i]==0):
            mp[chr(i + 65)] = 1

    # Initialize the frequencies
    # back to 0
    for i in range(len(small)):
        small[i] = 0
        caps[i] = 0

    # Marks the start and
    # end of current substring
    i = 0
    st = 0

    # Marks the start and end
    # of required substring
    start = -1
    end = -1

    # Stores the length of
    # smallest balanced substring
    minm = sys.maxsize

    while (i < len(s)):
        if(s[i] in mp):

            # Remove all characters
            # obtained so far
            while (st < i):
                if (ord(s[st]) >= 65 and ord(s[st]) <= 90):
                    caps[ord(s[st]) - 65] -= 1
                else:
                    small[ord(s[st]) - 97] -= 1

                st += 1
            i += 1
            st = i
        else:
            if (ord(s[i]) >= 65 and ord(s[i]) <= 90):
                caps[ord(s[i]) - 65] += 1
            else:
                small[ord(s[i] )- 97] += 1

            # Remove extra characters from
            # front of the current substring
            while (1):
                if (ord(s[st]) >= 65 and ord(s[st])<= 90 and caps[ord(s[st])- 65] > 1):
                    caps[ord(s[st]) - 65] -= 1
                    st += 1
                elif (ord(s[st]) >= 97 and ord(s[st]) <= 122 and small[ord(s[st]) - 97] > 1):
                    small[ord(s[st]) - 97] -= 1
                    st += 1
                else:
                    break

            # If substring (st, i) is balanced
            if (balanced(small, caps)):
                if (minm > (i - st + 1)):
                    minm = i - st + 1
                    start = st
                    end = i
            i += 1

    # No balanced substring
    if (start == -1 or end == -1):
        print(-1)

    # Store answer string
    else:
        ans = ""
        for i in range(start,end+1,1):
            ans +=  s[i]
        print(ans)

# Driver Code
if __name__ == '__main__':

    # Given string
    s = "azABaabba"
    smallestBalancedSubstring(s)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{
  public const int MaxValue = 2147483647;

  // Function to check if the current
  // string is balanced or not
  static bool balanced(int []small,
                       int []caps)
  {

    // For every character, check if
    // there exists uppercase as well
    // as lowercase characters
    for(int i = 0; i < 26; i++)
    {
      if (small[i] != 0 && (caps[i] == 0))
        return false;

      else if ((small[i] == 0) && (caps[i] != 0))
        return false;
    }
    return true;
  }

  // Function to find smallest length substring
  // in the given string which is balanced
  static void smallestBalancedSubstring(string s)
  {

    // Store frequency of
    // lowercase characters
    int[] small = new int[26];
    int i;

    // Stores frequency of
    // uppercase characters
    int[] caps = new int[26];
    Array.Clear(small, 0, small.Length);
    Array.Clear(caps, 0, caps.Length);

    // Count frequency of characters
    for(i = 0; i < s.Length; i++)
    {
      if (s[i] >= 65 && s[i] <= 90)
        caps[(int)s[i] - 65]++;
      else
        small[(int)s[i]- 97]++;
    }

    // Mark those characters which
    // are not present in both
    // lowercase and uppercase
    Dictionary<char,int> mp = new Dictionary<char,int>();

    for(i = 0; i < 26; i++)
    {
      if (small[i] != 0 && caps[i] == 0){
        mp[(char)(i+97)] = 1;
      }
      else if (caps[i] != 0 && small[i] == 0)
        mp[(char)(i+65)] = 1;
      // mp[char(i + 'A')] = 1;
    }

    // Initialize the frequencies
    // back to 0
    Array.Clear(small, 0, small.Length);
    Array.Clear(caps, 0, caps.Length);

    // Marks the start and
    // end of current substring
    i = 0;
    int st = 0;

    // Marks the start and end
    // of required substring
    int start = -1, end = -1;

    // Stores the length of
    // smallest balanced substring
    int minm = MaxValue;

    while (i < s.Length)
    {
      if (mp.ContainsKey(s[i]))
      {

        // Remove all characters
        // obtained so far
        while (st < i)
        {
          if ((int)s[st] >= 65 &&
              (int)s[st] <= 90)
            caps[(int)s[st] - 65]--;
          else
            small[(int)s[st] - 97]--;

          st++;
        }
        i += 1;
        st = i;
      }
      else
      {
        if ((int)s[i] >= 65 && (int)s[i] <= 90)
          caps[(int)s[i] - 65]++;
        else
          small[(int)s[i] - 97]++;

        // Remove extra characters from
        // front of the current substring
        while (true)
        {
          if ((int)s[st] >= 65 &&
              (int)s[st] <= 90 &&
              caps[(int)s[st] - 65] > 1)
          {
            caps[(int)s[st] - 65]--;
            st++;
          }
          else if ((int)s[st] >= 97 &&
                   (int)s[st] <= 122 &&
                   small[(int)s[st] - 97] > 1)
          {
            small[(int)s[st] - 97]--;
            st++;
          }
          else
            break;
        }

        // If substring (st, i) is balanced
        if (balanced(small, caps))
        {
          if (minm > (i - st + 1))
          {
            minm = i - st + 1;
            start = st;
            end = i;
          }
        }
        i += 1;
      }
    }

    // No balanced substring
    if (start == -1 || end == -1)
      Console.WriteLine(-1);

    // Store answer string
    else
    {
      string ans = "";
      for(int j = start; j <= end; j++)
        ans += s[j];

      Console.WriteLine(ans);
    }
  }

  // Driver Code
  public static void Main()
  {

    // Given string
    string s = "azABaabba";

    smallestBalancedSubstring(s);
  }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    let MaxValue = 2147483647;

    // Function to check if the current
    // string is balanced or not
    function balanced(small, caps)
    {

      // For every character, check if
      // there exists uppercase as well
      // as lowercase characters
      for(let i = 0; i < 26; i++)
      {
        if (small[i] != 0 && (caps[i] == 0))
          return false;

        else if ((small[i] == 0) && (caps[i] != 0))
          return false;
      }
      return true;
    }

    // Function to find smallest length substring
    // in the given string which is balanced
    function smallestBalancedSubstring(s)
    {

      // Store frequency of
      // lowercase characters
      let small = new Array(26);
      let i;

      // Stores frequency of
      // uppercase characters
      let caps = new Array(26);
      small.fill(0);
      caps.fill(0);

      // Count frequency of characters
      for(i = 0; i < s.length; i++)
      {
        if (s[i].charCodeAt() >= 65 && s[i].charCodeAt() <= 90)
          caps[s[i].charCodeAt() - 65]++;
        else
          small[s[i].charCodeAt()- 97]++;
      }

      // Mark those characters which
      // are not present in both
      // lowercase and uppercase
      let mp = new Map();

      for(i = 0; i < 26; i++)
      {
        if (small[i] != 0 && caps[i] == 0){
          mp.set(String.fromCharCode(i+97), 1);
        }
        else if (caps[i] != 0 && small[i] == 0)
          mp.set(String.fromCharCode(i+65), 1);
        // mp[char(i + 'A')] = 1;
      }

      // Initialize the frequencies
      // back to 0
      small.fill(0);
      caps.fill(0);

      // Marks the start and
      // end of current substring
      i = 0;
      let st = 0;

      // Marks the start and end
      // of required substring
      let start = -1, end = -1;

      // Stores the length of
      // smallest balanced substring
      let minm = MaxValue;

      while (i < s.length)
      {
        if (mp.has(s[i]))
        {

          // Remove all characters
          // obtained so far
          while (st < i)
          {
            if (s[st].charCodeAt() >= 65 &&
                s[st].charCodeAt() <= 90)
              caps[s[st].charCodeAt() - 65]--;
            else
              small[s[st].charCodeAt() - 97]--;

            st++;
          }
          i += 1;
          st = i;
        }
        else
        {
          if (s[i].charCodeAt() >= 65 && s[i].charCodeAt() <= 90)
            caps[s[i].charCodeAt() - 65]++;
          else
            small[s[i].charCodeAt() - 97]++;

          // Remove extra characters from
          // front of the current substring
          while (true)
          {
            if (s[st].charCodeAt() >= 65 &&
                s[st].charCodeAt() <= 90 &&
                caps[s[st].charCodeAt() - 65] > 1)
            {
              caps[s[st].charCodeAt() - 65]--;
              st++;
            }
            else if (s[st].charCodeAt() >= 97 &&
                     s[st].charCodeAt() <= 122 &&
                     small[s[st].charCodeAt() - 97] > 1)
            {
              small[s[st].charCodeAt() - 97]--;
              st++;
            }
            else
              break;
          }

          // If substring (st, i) is balanced
          if (balanced(small, caps))
          {
            if (minm > (i - st + 1))
            {
              minm = i - st + 1;
              start = st;
              end = i;
            }
          }
          i += 1;
        }
      }

      // No balanced substring
      if (start == -1 || end == -1)
        document.write(-1 + "</br>");

      // Store answer string
      else
      {
        let ans = "";
        for(let j = start; j <= end; j++)
          ans += s[j];

        document.write(ans + "</br>");
      }
    }

    // Given string
    let s = "azABaabba";

    smallestBalancedSubstring(s);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
ABaab
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)