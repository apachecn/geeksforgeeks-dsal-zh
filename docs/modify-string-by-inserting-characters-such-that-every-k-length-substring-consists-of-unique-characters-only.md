# 通过插入字符修改字符串，使得每个 K 长度的子串仅由唯一的字符组成

> 原文:[https://www . geeksforgeeks . org/通过插入字符修改字符串，以便每 k 个长度的子字符串仅由唯一字符组成/](https://www.geeksforgeeks.org/modify-string-by-inserting-characters-such-that-every-k-length-substring-consists-of-unique-characters-only/)

给定大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)T2 S，由 **K** 不同的字符和**(N–K)****' '组成** s，任务是替换所有**'？'**字符串中的现有字符，使得大小为 **K** 的每个[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)仅由唯一字符组成。如果不可能，则打印**-1”**。

**示例:**

> **输入:** S =？？？？abcd "，K = 4
> T3】输出:abcdab
> **解释:**
> 替换 4 '？带有“abcd”的 S 将字符串 S 修改为“abcdabcd”，满足给定条件。
> 
> **输入:** S =？a？b？c "，K = 3
> **输出:** bacbac
> **解释:**
> 将 S[0]替换为‘b’，S[2]替换为‘c’，S[4]替换为‘a’，将字符串 S 修改为“bacbac”，满足给定条件。

**方法:**这个想法是基于这样的观察:在最终的结果字符串中，每个字符必须出现在恰好 **K 个位置之后，**就像 **(K + 1) <sup>第</sup>字符**必须与**1<sup>ST</sup>T11】、 **(K + 2) <sup>第</sup>字符**必须与 **2 <sup>和</sup>T19】相同****

按照以下步骤解决问题:

*   初始化一个 [hashmap](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 来存储字符的位置。
*   [使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果当前字符**S【I】**与“**不相同？**'，然后更新 **M[i % K] = S[i]** 。
*   [使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果 [**i%k** 的值在**地图 M**](https://www.geeksforgeeks.org/map-find-function-in-c-stl/) 中不存在，则打印**-1”**和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。否则将 **S[i]** 更新为 **M[i % K]** 。
*   完成上述步骤后，如果循环没有中断，则打印 **S** 作为结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to replace all '?'
// characters in a string such
// that the given conditions are satisfied
void fillString(string s, int k)
{
    unordered_map<int, char> mp;

    // Traverse the string to Map the
    // characters with respective positions
    for (int i = 0; i < s.size(); i++) {
        if (s[i] != '?') {
            mp[i % k] = s[i];
        }
    }

    // Traverse the string again and
    // replace all unknown characters
    for (int i = 0; i < s.size(); i++) {

        // If i % k is not found in
        // the Map M, then return -1
        if (mp.find(i % k) == mp.end()) {

            cout << -1;
            return;
        }

        // Update S[i]
        s[i] = mp[i % k];
    }

    // Print the string S
    cout << s;
}

// Driver Code
int main()
{
    string S = "????abcd";
    int K = 4;
    fillString(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to replace all '?'
    // characters in a string such
    // that the given conditions are satisfied
    static void fillString(String str, int k)
    {

        char s[] = str.toCharArray();

        HashMap<Integer, Character> mp = new HashMap<>();

        // Traverse the string to Map the
        // characters with respective positions
        for (int i = 0; i < s.length; i++) {
            if (s[i] != '?') {
                mp.put(i % k, s[i]);
            }
        }

        // Traverse the string again and
        // replace all unknown characters
        for (int i = 0; i < s.length; i++) {

            // If i % k is not found in
            // the Map M, then return -1
            if (!mp.containsKey(i % k)) {
                System.out.println(-1);
                return;
            }

            // Update S[i]
            s[i] = mp.getOrDefault(i % k, s[i]);
        }

        // Print the string S
        System.out.println(new String(s));
    }

    // Driver Code
    public static void main(String[] args)
    {

        String S = "????abcd";
        int K = 4;
        fillString(S, K);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to replace all '?'
# characters in a string such
# that the given conditions are satisfied
def fillString(s, k):
    mp = {}

    # Traverse the string to Map the
    # characters with respective positions
    for i in range(len(s)):
        if (s[i] != '?'):
            mp[i % k] = s[i]

    # Traverse the string again and
    # replace all unknown characters
    s = list(s)
    for i in range(len(s)):

        # If i % k is not found in
        # the Map M, then return -1
        if ((i % k) not in mp):
            print(-1)
            return

        # Update S[i]
        s[i] = mp[i % k]

    # Print the string S
    s =   ''.join(s)
    print(s)

# Driver Code
if __name__ == '__main__':
    S = "????abcd"
    K = 4
    fillString(S, K)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

  // Function to replace all '?'
  // characters in a string such
  // that the given conditions are satisfied
  static void fillString(string str, int k)
  {

    char[] s = str.ToCharArray();

    Dictionary<int,
    int> mp = new Dictionary<int,
    int>();

    // Traverse the string to Map the
    // characters with respective positions
    for (int i = 0; i < s.Length; i++) {
      if (s[i] != '?') {
        mp[i % k] = s[i];
      }
    }

    // Traverse the string again and
    // replace all unknown characters
    for (int i = 0; i < s.Length; i++) {

      // If i % k is not found in
      // the Map M, then return -1
      if (!mp.ContainsKey(i % k)) {
        Console.WriteLine(-1);
        return;
      }

      // Update S[i]
      s[i] = (char)mp[i % k];

    }

    // Print the string S
    Console.WriteLine(new string(s));
  }

  // Driver code
  static void Main()
  {
    string S = "????abcd";
    int K = 4;
    fillString(S, K);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to replace all '?'
      // characters in a string such
      // that the given conditions are satisfied
      function fillString(str, k) {
        var s = str.split("");

        var mp = {};

        // Traverse the string to Map the
        // characters with respective positions
        for (var i = 0; i < s.length; i++) {
          if (s[i] !== "?") {
            mp[i % k] = s[i];
          }
        }

        // Traverse the string again and
        // replace all unknown characters
        for (var i = 0; i < s.length; i++) {
          // If i % k is not found in
          // the Map M, then return -1
          if (!mp.hasOwnProperty(i % k)) {
            document.write(-1);
            return;
          }

          // Update S[i]
          s[i] = mp[i % k];
        }

        // Print the string S
        document.write(s.join("") + "<br>");
      }

      // Driver code
      var S = "????abcd";
      var K = 4;
      fillString(S, K);
    </script>
```

**Output:** 

```
abcdabcd
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)