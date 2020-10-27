# 检查是否可以通过对子字符串进行排序将字符串转换为另一个字符串

给定两个字符串 **str1** 和 **str2，**，每个字符串的长度 **N** ，并且仅由小写英文字母组成，任务是检查字符串 **str1** 通过多次执行以下操作，可以将]转换为字符串 **str2** 。

*   在 **str1** 和[中选择一个非空的子字符串，按字典顺序](https://www.geeksforgeeks.org/sort-string-characters/)就地排序，以不降序排列子字符串的字符。

**示例：**

> **输入：** str1 =“ hdecb”，str2 =“ cdheb” str1 中的“”将字符串修改为“ hdceb”。
> 对 str1 中的子字符串“ hdc”进行排序将字符串修改为“ cdheb”。
> 由于修改后的字符串与 str2 相同，因此答案为是。
> 
> **输入：** str1 =“ abcdef”，str2 =“ dacbfe”
> **输出：**否

**方法：**请按照以下步骤解决问题：

*   请注意，在字符串 **str1** 中，如果有两个字符 **str1 [i]** 和 **str2 [j]** 使得 **str1 [i] < str1 [j]** ，则可以交换这些字符。
*   换句话说，可以将字符自由地向左移动，直到遇到较小的字符。 例如，“ acdb”可以转换为“ **acbd** ”，“ **abcd** ”，因为“ **b** ”可以向左自由移动，直到“ [ ''发生。
*   因此，检查是否可以将所需字符向左移动到字符串 **str2** 中的相应位置。
*   将字符串 **str1** 的每个字符的索引存储在数组中。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **str2，**，对于每个字符，检查 **str1** 中的相同字符是否可以移到该位置。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if str1 can be
// transformed to t by sorting substrings
void canTransform(string& s, string& t)
{
    int n = s.length();

    // Occur[i] stores the indices
    // of char ('a'+i) in string s
    vector<int> occur[26];
    for (int x = 0; x < n; x++) {
        char ch = s[x] - 'a';
        occur[ch].push_back(x);
    }

    // idx[i] stores the next available
    // index of char ('a'+i) in occur[i]
    vector<int> idx(26, 0);
    bool poss = true;
    for (int x = 0; x < n; x++) {
        char ch = t[x] - 'a';

        // If this char is not available
        // anymore
        if (idx[ch] >= occur[ch].size()) {

            // Conversion not possible
            poss = false;
            break;
        }
        for (int small = 0; small < ch; small++) {

            // If one of the smaller characters
            // is available and occurs before
            if (idx[small] < occur[small].size()
                && occur[small][idx[small]]
                       < occur[ch][idx[ch]]) {

                // Conversion not possible
                poss = false;
                break;
            }
        }
        idx[ch]++;
    }

    // Print the answer
    if (poss) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }
}

// Driver Code
int main()
{
    string s, t;

    s = "hdecb";
    t = "cdheb";

    canTransform(s, t);
    return 0;
}

```

## Java

```java

// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to check if str1 
// can be transformed to t by 
// sorting subStrings
static void canTransform(String s, 
                         String t)
{
  int n = s.length();

  // Occur[i] stores the indices
  // of char ('a'+i) in String s
  Vector<Integer> occur[] = new Vector[26];

  for (int i = 0; i < occur.length; i++)
    occur[i] = new Vector<Integer>();

  for (int x = 0; x < n; x++) 
  {
    char ch = (char)(s.charAt(x) - 'a');
    occur[ch].add(x);
  }

  // idx[i] stores the next available
  // index of char ('a'+i) in occur[i]
  int []idx = new int[26];
  boolean poss = true;

  for (int x = 0; x < n; x++) 
  {
    char ch = (char)(t.charAt(x) - 'a');

    // If this char is 
    // not available anymore
    if (idx[ch] >= occur[ch].size()) 
    {
      // Conversion not possible
      poss = false;
      break;
    }
    for (int small = 0; small < ch; small++) 
    {
      // If one of the smaller characters
      // is available and occurs before
      if (idx[small] < occur[small].size() && 
          occur[small].get(idx[small]) < 
          occur[ch].get(idx[ch])) 
      {
        // Conversion not possible
        poss = false;
        break;
      }
    }
    idx[ch]++;
  }

  // Print the answer
  if (poss) 
  {
    System.out.print("Yes" + "\n");
  }
  else
  {
    System.out.print("No" + "\n");
  }
}

// Driver Code
public static void main(String[] args)
{
  String s, t;
  s = "hdecb";
  t = "cdheb";
  canTransform(s, t);
}
}

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to check if str1 can be
# transformed to t by sorting substrings
def canTransform(s, t):

    n = len(s)

    # Occur[i] stores the indices
    # of ('a'+i) in string s
    occur = [[] for i in range(26)]

    for x in range(n):
        ch = ord(s[x]) - ord('a')
        occur[ch].append(x)

    # idx[i] stores the next available
    # index of ('a'+i) in occur[i]
    idx = [0] * (26)
    poss = True

    for x in range(n):
        ch = ord(t[x]) - ord('a')

        # If this is not available
        # anymore
        if (idx[ch] >= len(occur[ch])):

            # Conversion not possible
            poss = False
            break

        for small in range(ch):

            # If one of the smaller characters
            # is available and occurs before
            if (idx[small] < len(occur[small]) and
                occur[small][idx[small]] < 
                occur[ch][idx[ch]]):

                # Conversion not possible
                poss = False
                break

        idx[ch] += 1

    # Print the answer
    if (poss):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    s = "hdecb"
    t = "cdheb"

    canTransform(s, t)

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if str1 
// can be transformed to t by 
// sorting subStrings
static void canTransform(String s, 
                         String t)
{
  int n = s.Length;

  // Occur[i] stores the indices
  // of char ('a'+i) in String s
  List<int> []occur = new List<int>[26];

  for(int i = 0; i < occur.Length; i++)
    occur[i] = new List<int>();

  for(int x = 0; x < n; x++) 
  {
    char ch = (char)(s[x] - 'a');
    occur[ch].Add(x);
  }

  // idx[i] stores the next available
  // index of char ('a'+i) in occur[i]
  int []idx = new int[26];
  bool poss = true;

  for(int x = 0; x < n; x++) 
  {
    char ch = (char)(t[x] - 'a');

    // If this char is 
    // not available anymore
    if (idx[ch] >= occur[ch].Count) 
    {

      // Conversion not possible
      poss = false;
      break;
    }
    for(int small = 0; small < ch; small++) 
    {

      // If one of the smaller characters
      // is available and occurs before
      if (idx[small] < occur[small].Count && 
            occur[small][idx[small]] < 
            occur[ch][idx[ch]]) 
      {

        // Conversion not possible
        poss = false;
        break;
      }
    }
    idx[ch]++;
  }

  // Print the answer
  if (poss) 
  {
    Console.Write("Yes" + "\n");
  }
  else
  {
    Console.Write("No" + "\n");
  }
}

// Driver Code
public static void Main(String[] args)
{
  String s, t;
  s = "hdecb";
  t = "cdheb";

  canTransform(s, t);
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
Yes

```

***时间复杂度：** O（N）*
***辅助空间：** O（N）*



* * *

* * *



