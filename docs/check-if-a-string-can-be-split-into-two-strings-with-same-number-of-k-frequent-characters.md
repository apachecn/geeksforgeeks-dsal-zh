# 检查一个字符串是否可以拆分成 K-频数相同的两个字符串

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-split-two-string-with-number-k-frequency-characters/](https://www.geeksforgeeks.org/check-if-a-string-can-be-split-into-two-strings-with-same-number-of-k-frequent-characters/)

给定一个字符串 **S** 和一个整数 **K** ，任务是检查是否有可能将这些字符分配到两个字符串中，使得两个字符串中具有频率 **K** 的字符数相等。
如果可以，那么打印一个由 **1** 和 **2** 组成的序列，表示哪个字符应该放在哪个字符串中。否则，打印**否**。
**注意:**这些新字符串中的一个可以是空的。

**示例:**

> **输入:**S = " abbbccc "，K = 1
> **输出:** 1111211
> **说明:**
> 这两个字符串是“abbcc”和“c”。
> 因此，这两个字符串恰好有一个字符的频率为 K( = 1)。
> 
> **输入:**S =“aaaa”，K = 3
> **输出:** 1111
> **说明:**
> 字符串可以拆分为“AAAA”和“”。
> 因此，在两个字符串中没有字符的频率为 3。

**方法:**
按照以下步骤解决问题:

*   检查以下三个条件以确定分割是否可能:
    1。如果初始字符串中出现频率为 **K** 的字符总数为**甚至**，则这些字符可以平均放入两个字符串中，其余字符(出现频率不等于 **K** 的字符)可以放入两组中的任何一组。
    2。如果初始字符串中频率为 **K** 的字符总数为**奇数**，则如果初始字符串中频率大于 **K** 但不等于 **2K** 的字符，则这种分布是可能的。

> **图解:**T2【S =【abceee】，K = 1
> 拆分为“abeee”和“ce”。因此，两个字符串都有 2 个字符，频率为 1。

3.如果初始字符串中频率为 **K** 的字符总数为**奇数**，则如果初始字符串中频率等于 **2K** 的字符，则这种分布是可能的。

> **插图:**T2【S = " aaaaabccdde "，K = 2
> 拆分为“aabbc”和“aaddce”，这样两个字符串都有两个频率为 2 的字符。

*   如果上述三个条件都失败，那么答案是**“否”**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the
// arrangement of characters
void DivideString(string s, int n,
                  int k)
{
    int i, c = 0, no = 1;
    int c1 = 0, c2 = 0;

    // Stores frequency of
    // characters
    int fr[26] = { 0 };

    string ans = "";

    for (i = 0; i < n; i++) {
        fr[s[i] - 'a']++;
    }

    char ch, ch1;
    for (i = 0; i < 26; i++) {

        // Count the character
        // having frequency K
        if (fr[i] == k) {
            c++;
        }

        // Count the character
        // having frequency
        // greater than K and
        // not equal to 2K
        if (fr[i] > k
            && fr[i] != 2 * k) {
            c1++;
            ch = i + 'a';
        }

        if (fr[i] == 2 * k) {
            c2++;
            ch1 = i + 'a';
        }
    }

    for (i = 0; i < n; i++)
        ans = ans + "1";

    map<char, int> mp;
    if (c % 2 == 0 || c1 > 0 || c2 > 0) {
        for (i = 0; i < n; i++) {

            // Case 1
            if (fr[s[i] - 'a'] == k) {
                if (mp.find(s[i])
                    != mp.end()) {
                    ans[i] = '2';
                }
                else {
                    if (no <= (c / 2)) {
                        ans[i] = '2';
                        no++;
                        mp[s[i]] = 1;
                    }
                }
            }
        }

        // Case 2
        if (c % 2 == 1 && c1 > 0) {
            no = 1;
            for (i = 0; i < n; i++) {
                if (s[i] == ch && no <= k) {

                    ans[i] = '2';
                    no++;
                }
            }
        }

        // Case 3
        if (c % 2 == 1 && c1 == 0) {
            no = 1;
            int flag = 0;
            for (int i = 0; i < n; i++) {
                if (s[i] == ch1 && no <= k) {
                    ans[i] = '2';
                    no++;
                }
                if (fr[s[i] - 'a'] == k
                    && flag == 0
                    && ans[i] == '1') {
                    ans[i] = '2';
                    flag = 1;
                }
            }
        }

        cout << ans << endl;
    }
    else {
        // If all cases fail
        cout << "NO" << endl;
    }
}

// Driver Code
int main()
{

    string S = "abbbccc";
    int N = S.size();
    int K = 1;

    DivideString(S, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
import java.util.*;

class GFG{

// Function to print the
// arrangement of characters
public static void DivideString(String s, int n,
                                          int k)
{
    int i, c = 0, no = 1;
    int c1 = 0, c2 = 0;

    // Stores frequency of
    // characters
    int[] fr = new int[26];

    char[] ans = new char[n];

    for(i = 0; i < n; i++)
    {
        fr[s.charAt(i) - 'a']++;
    }

    char ch = 'a', ch1 = 'a';
    for(i = 0; i < 26; i++)
    {

        // Count the character
        // having frequency K
        if (fr[i] == k)
        {
            c++;
        }

        // Count the character
        // having frequency
        // greater than K and
        // not equal to 2K
        if (fr[i] > k && fr[i] != 2 * k)
        {
            c1++;
            ch = (char)(i + 'a');
        }

        if (fr[i] == 2 * k)
        {
            c2++;
            ch1 = (char)(i + 'a');
        }
    }

    for(i = 0; i < n; i++)
        ans[i] = '1';

    HashMap<Character, Integer> mp = new HashMap<>();

    if (c % 2 == 0 || c1 > 0 || c2 > 0)
    {
        for(i = 0; i < n; i++)
        {

            // Case 1
            if (fr[s.charAt(i) - 'a'] == k)
            {
                if (mp.containsKey(s.charAt(i)))
                {
                    ans[i] = '2';
                }
                else
                {
                    if (no <= (c / 2))
                    {
                        ans[i] = '2';
                        no++;
                        mp.replace(s.charAt(i), 1);
                    }
                }
            }
        }

        // Case 2
        if ( (c % 2 == 1) && (c1 > 0) )
        {
            no = 1;
            for(i = 0; i < n; i++)
            {
                if (s.charAt(i) == ch && no <= k)
                {
                    ans[i] = '2';
                    no++;
                }
            }
        }

        // Case 3
        if (c % 2 == 1 && c1 == 0)
        {
            no = 1;
            int flag = 0;

            for(i = 0; i < n; i++)
            {
                if (s.charAt(i) == ch1 && no <= k)
                {
                    ans[i] = '2';
                    no++;
                }
                if (fr[s.charAt(i) - 'a'] == k &&
                      flag == 0 && ans[i] == '1')
                {
                    ans[i] = '2';
                    flag = 1;
                }
            }
        }
        System.out.println(ans);
    }
    else
    {

        // If all cases fail
        System.out.println("NO");
    }
}

// Driver code
public static void main(String[] args)
{
    String S = "abbbccc";
    int N = S.length();
    int K = 1;

    DivideString(S, N, K);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to print the
# arrangement of characters
def DivideString(s, n, k):

    c = 0
    no = 1
    c1 = 0
    c2 = 0

    # Stores frequency of
    # characters
    fr = [0] * 26

    ans = []
    for i in range(n):
        fr[ord(s[i]) - ord('a')] += 1

    for i in range(26):

        # Count the character
        # having frequency K
        if (fr[i] == k):
            c += 1

        # Count the character having
        # frequency greater than K and
        # not equal to 2K
        if (fr[i] > k and fr[i] != 2 * k):
            c1 += 1
            ch = chr(ord('a') + i)

        if (fr[i] == 2 * k):
            c2 += 1
            ch1 = chr(ord('a') + i)

    for i in range(n):
        ans.append("1")

    mp = {}
    if (c % 2 == 0 or c1 > 0 or c2 > 0):
        for i in range(n):

            # Case 1
            if (fr[ord(s[i]) - ord('a')] == k):
                if (s[i] in mp):
                    ans[i] = '2'

                else:
                    if (no <= (c // 2)):
                        ans[i] = '2'
                        no += 1
                        mp[s[i]] = 1

        # Case 2
        if (c % 2 == 1 and c1 > 0):
            no = 1
            for i in range(n):
                if (s[i] == ch and no <= k):
                    ans[i] = '2'
                    no += 1

        # Case 3
        if (c % 2 == 1 and c1 == 0):
            no = 1
            flag = 0

            for i in range(n):
                if (s[i] == ch1 and no <= k):
                    ans[i] = '2'
                    no += 1

                if (fr[s[i] - 'a'] == k and
                              flag == 0 and
                            ans[i] == '1'):
                    ans[i] = '2'
                    flag = 1

        print("".join(ans))
    else:

        # If all cases fail
        print("NO")

# Driver Code
if __name__ == '__main__':

    S = "abbbccc"
    N = len(S)
    K = 1

    DivideString(S, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above problem
using System;
using System.Collections.Generic;

class GFG{

// Function to print the
// arrangement of characters
public static void DivideString(string s, int n,
                                          int k)
{
    int i, c = 0, no = 1;
    int c1 = 0, c2 = 0;

    // Stores frequency of
    // characters
    int[] fr = new int[26];

    char[] ans = new char[n];

    for(i = 0; i < n; i++)
    {
        fr[s[i] - 'a']++;
    }

    char ch = 'a', ch1 = 'a';
    for(i = 0; i < 26; i++)
    {

        // Count the character
        // having frequency K
        if (fr[i] == k)
        {
            c++;
        }

        // Count the character having
        // frequency greater than K and
        // not equal to 2K
        if (fr[i] > k && fr[i] != 2 * k)
        {
            c1++;
            ch = (char)(i + 'a');
        }

        if (fr[i] == 2 * k)
        {
            c2++;
            ch1 = (char)(i + 'a');
        }
    }

    for(i = 0; i < n; i++)
        ans[i] = '1';

    Dictionary<char,
               int> mp = new Dictionary<char,
                                        int>();

    if (c % 2 == 0 || c1 > 0 || c2 > 0)
    {
        for(i = 0; i < n; i++)
        {

            // Case 1
            if (fr[s[i] - 'a'] == k)
            {
                if (mp.ContainsKey(s[i]))
                {
                    ans[i] = '2';
                }
                else
                {
                    if (no <= (c / 2))
                    {
                        ans[i] = '2';
                        no++;
                        mp[s[i]] = 1;
                    }
                }
            }
        }

        // Case 2
        if ( (c % 2 == 1) && (c1 > 0) )
        {
            no = 1;
            for(i = 0; i < n; i++)
            {
                if (s[i]== ch && no <= k)
                {
                    ans[i] = '2';
                    no++;
                }
            }
        }

        // Case 3
        if (c % 2 == 1 && c1 == 0)
        {
            no = 1;
            int flag = 0;

            for(i = 0; i < n; i++)
            {
                if (s[i] == ch1 && no <= k)
                {
                    ans[i] = '2';
                    no++;
                }
                if (fr[s[i] - 'a'] == k &&
                    flag == 0 && ans[i] == '1')
                {
                    ans[i] = '2';
                    flag = 1;
                }
            }
        }
        Console.Write(ans);
    }
    else
    {

        // If all cases fail
        Console.Write("NO");
    }
}

// Driver code
public static void Main(string[] args)
{
    string S = "abbbccc";
    int N = S.Length;
    int K = 1;

    DivideString(S, N, K);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
      // JavaScript program for the above problem
      // Function to print the
      // arrangement of characters
      function DivideString(s, n, k) {
        var i,
          c = 0,
          no = 1;
        var c1 = 0,
          c2 = 0;

        // Stores frequency of
        // characters
        var fr = new Array(26).fill(0);

        var ans = [];

        for (i = 0; i < n; i++) {
          fr[s[i].charCodeAt(0) - "a".charCodeAt(0)]++;
        }

        var ch = "a",
          ch1 = "a";
        for (i = 0; i < 26; i++) {
          // Count the character
          // having frequency K
          if (fr[i] === k) {
            c++;
          }

          // Count the character having
          // frequency greater than K and
          // not equal to 2K
          if (fr[i] > k && fr[i] !== 2 * k) {
            c1++;
            ch = String.fromCharCode(i + "a".charCodeAt(0));
          }

          if (fr[i] === 2 * k) {
            c2++;
            ch1 = String.fromCharCode(i + "a".charCodeAt(0));
          }
        }

        for (i = 0; i < n; i++) ans.push("1");

        var mp = {};

        if (c % 2 === 0 || c1 > 0 || c2 > 0) {
          for (i = 0; i < n; i++) {
            // Case 1
            if (fr[s[i].charCodeAt(0) - "a".charCodeAt(0)] === k) {
              if (mp.hasOwnProperty(s[i])) {
                ans[i] = "2";
              }
              else {
                if (no <= parseInt(c / 2)) {
                  ans[i] = "2";
                  no++;
                  mp[s[i]] = 1;
                }
              }
            }
          }

          // Case 2
          if (c % 2 === 1 && c1 > 0) {
            no = 1;
            for (i = 0; i < n; i++) {
              if (s[i] === ch && no <= k) {
                ans[i] = "2";
                no++;
              }
            }
          }

          // Case 3
          if (c % 2 === 1 && c1 === 0) {
            no = 1;
            var flag = 0;

            for (i = 0; i < n; i++) {
              if (s[i] === ch1 && no <= k) {
                ans[i] = "2";
                no++;
              }
              if (
                fr[s[i].charCodeAt(0) - "a".charCodeAt(0)] === k &&
                flag === 0 &&
                ans[i] === "1"
              ) {
                ans[i] = "2";
                flag = 1;
              }
            }
          }
          document.write(ans.join(""));
        }
        else {
          // If all cases fail
          document.write("NO");
        }
      }

      // Driver code
      var S = "abbbccc";
      var N = S.length;
      var K = 1;

      DivideString(S, N, K);
</script>
```

**Output:** 

```
1111211
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*