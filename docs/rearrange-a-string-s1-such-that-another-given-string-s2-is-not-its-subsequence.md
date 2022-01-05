# 重新排列一个字符串 S1，使得另一个给定的字符串 S2 不是它的子序列

> 原文:[https://www . geesforgeks . org/rearray-a-string-S1-so-另一个给定的字符串-S2-不是它的子序列/](https://www.geeksforgeeks.org/rearrange-a-string-s1-such-that-another-given-string-s2-is-not-its-subsequence/)

给定两个大小分别为 **N 和 M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S1** 和 **S2** ，任务是重新排列字符串 **S1** 中的字符，使得 **S2** 不是它的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。如果无法进行这样的重新排列，则打印**-1”**。否则，打印重新排列的字符串 **S1** 。

**示例:**

> **输入:**S1 =【ABCD】，S2 =【ab】
> **输出:**【dcba】
> **解释:**
> 将字符串 S1 重新排列为“dcba”。
> 现在，字符串 S2 =“ab”不是 S1 的子序列。
> 
> **输入:**S1 =“aa”，S2 =“a”
> **输出:** -1

**方法:**按照以下步骤解决问题:

*   将字符串 S2 中的[字符频率存储在辅助](https://www.geeksforgeeks.org/c-program-to-find-the-frequency-of-characters-in-a-string/)[数组](https://www.geeksforgeeks.org/array-data-structure/)中，比如**CNT【26】**。
*   初始化一个变量，比如说 **ch** ，来存储字符串 **S2** 中存在的唯一字符。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **cnt[]** 。如果**CNT【I】**的值等于 **M** ，这意味着 **S2** 仅由 **1 个唯一字符**组成。将该字符存储在 **ch** 和[中，脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   如果未定义 **ch** 的值，则执行以下操作:
    *   [使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)**【S2】**，如果在任何索引处**S2【I】>S2【I+1】**[按递增顺序排序**S1**](https://www.geeksforgeeks.org/sort-string-characters/)，并且[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   如果穿越时没有遇到上述情况，[按照递减顺序](https://www.geeksforgeeks.org/sort-string-characters/)对 **S1** 进行排序。
    *   打印字符串 **S1** 。
*   否则，将 **ch** 的出现存储在字符串 **S1** 中 **freq** 中。如果 **freq** 的值小于 **M** ，则打印 **S1** 。否则，打印 **-1** 。

下面是执行上述方法的情况:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange characters
// in string S1 such that S2 is not
// a subsequence of it
void rearrangeString(string s1, string s2)
{
    // Store the frequencies of
    // characters of string s2
    int cnt[26] = { 0 };

    // Traverse the string s2
    for (int i = 0; i < s2.size(); i++)

        // Update the frequency
        cnt[s2[i] - 'a']++;

    // Find the number of unique
    // characters in s2
    int unique = 0;
    for (int i = 0; i < 26; i++)

        // Increment unique by 1 if the
        // condition satisfies
        if (cnt[i] != 0)
            unique++;

    // Check if the number of unique
    // characters in string s2 is 1
    if (unique == 1) {

        // Store the unique character
        // frequency
        int count_in_s2 = s2.size();

        // Store occurence of it in s1
        int count_in_s1 = 0;

        // Find count of that character
        // in the string s1
        for (int i = 0; i < s1.size(); i++)

            // Increment count by 1 if
            // that unique character is
            // same as current character
            if (s1[i] == s2[0])
                count_in_s1++;

        // If count count_in_s1 is
        // less than count_in_s2, then
        // print s1 and return
        if (count_in_s1 < count_in_s2) {
            cout << s1;
            return;
        }

        // Otherwise, there is no
        // possible arrangement
        cout << -1;
    }
    else {

        // Checks if any character in
        // s2 is less than its next
        // character
        int inc = 1;

        // Iterate the string, s2
        for (int i = 0; i < s2.size() - 1; i++)

            // If s[i] is greater
            // than the s[i+1]
            if (s2[i] > s2[i + 1])

                // Set inc to 0
                inc = 0;

        // If inc=1, print s1 in
        // decreasing order
        if (inc == 1) {
            sort(s1.begin(),
                 s1.end(),
                 greater<char>());
            cout << s1;
        }

        // Otherwise, print s1 in
        // increasing order
        else {
            sort(s1.begin(), s1.end());
            cout << s1;
        }
    }
}

// Driver code
int main()
{
    string s1 = "abcd", s2 = "ab";
    rearrangeString(s1, s2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to rearrange characters
// in string S1 such that S2 is not
// a subsequence of it
static void rearrangeString(char[] s1, char[] s2)
{

    // Store the frequencies of
    // characters of string s2
    int[] cnt = new int[26];

    // Traverse the string s2
    for(int i = 0; i < s2.length; i++)

        // Update the frequency
        cnt[s2[i] - 'a']++;

    // Find the number of unique
    // characters in s2
    int unique = 0;

    for(int i = 0; i < 26; i++)

        // Increment unique by 1 if the
        // condition satisfies
        if (cnt[i] != 0)
            unique++;

    // Check if the number of unique
    // characters in string s2 is 1
    if (unique == 1)
    {

        // Store the unique character
        // frequency
        int count_in_s2 = s2.length;

        // Store occurence of it in s1
        int count_in_s1 = 0;

        // Find count of that character
        // in the string s1
        for(int i = 0; i < s1.length; i++)

            // Increment count by 1 if
            // that unique character is
            // same as current character
            if (s1[i] == s2[0])
                count_in_s1++;

        // If count count_in_s1 is
        // less than count_in_s2, then
        // print s1 and return
        if (count_in_s1 < count_in_s2)
        {
            System.out.print(new String(s1));
            return;
        }

        // Otherwise, there is no
        // possible arrangement
        System.out.print(-1);
    }
    else
    {

        // Checks if any character in
        // s2 is less than its next
        // character
        int inc = 1;

        // Iterate the string, s2
        for(int i = 0; i < s2.length - 1; i++)

            // If s[i] is greater
            // than the s[i+1]
            if (s2[i] > s2[i + 1])

                // Set inc to 0
                inc = 0;

        // If inc=1, print s1 in
        // decreasing order
        if (inc == 1)
        {
            Arrays.sort(s1);
            for(int k = 0; k < s1.length / 2; k++)
            {
                char temp = s1[k];
                s1[k] = s1[s1.length - k - 1];
                s1[s1.length - k - 1] = temp;
            }
            System.out.print(new String(s1));
        }

        // Otherwise, print s1 in
        // increasing order
        else
        {
            Arrays.sort(s1);
            System.out.print(new String(s1));
        }
    }
}

// Driver code 
public static void main(String[] args)
{
    char[] s1 = "abcd".toCharArray();
    char[] s2 = "ab".toCharArray();

    rearrangeString(s1, s2);
}
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to rearrange characters
# in S1 such that S2 is not
# a subsequence of it
def rearrangeString(s1, s2):

    # Store the frequencies of
    # characters of s2
    cnt = [0]*26

    # Traverse the s2
    for i in range(len(s2)):

        # Update the frequency
        cnt[ord(s2[i]) - ord('a')] += 1

    # Find the number of unique
    # characters in s2
    unique = 0
    for i in range(26):

        # Increment unique by 1 if the
        # condition satisfies
        if (cnt[i] != 0):
            unique += 1

    # Check if the number of unique
    # characters in s2 is 1
    if (unique == 1):

        # Store the unique character
        # frequency
        count_in_s2 = len(s2)

        # Store occurence of it in s1
        count_in_s1 = 0

        # Find count of that character
        # in the s1
        for i in range(len(s1)):

            # Increment count by 1 if
            # that unique character is
            # same as current character
            if (s1[i] == s2[0]):
                count_in_s1 += 1

        # If count count_in_s1 is
        # less than count_in_s2, then
        # prs1 and return
        if (count_in_s1 < count_in_s2):
            print (s1, end = "")
            return

        # Otherwise, there is no
        # possible arrangement
        print (-1, end = "")
    else:

        # Checks if any character in
        # s2 is less than its next
        # character
        inc = 1

        # Iterate the string, s2
        for i in range(len(s2) - 1):

            # If s[i] is greater
            # than the s[i+1]
            if (s2[i] > s2[i + 1]):

                # Set inc to 0
                inc = 0

        # If inc=1, prs1 in
        # decreasing order
        if (inc == 1):
            s1 = sorted(s1)[::-1]
            print ("".join(s1), end = "")

        # Otherwise, prs1 in
        # increasing order
        else:
            s1 = sorted(s1)
            print ("".join(s1), end = "")

# Driver code
if __name__ == '__main__':
    s1, s2 = "abcd", "ab"
    rearrangeString(s1, s2)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to rearrange characters
  // in string S1 such that S2 is not
  // a subsequence of it
  static void rearrangeString(char[] s1, char[] s2)
  {

    // Store the frequencies of
    // characters of string s2
    int[] cnt = new int[26];

    // Traverse the string s2
    for (int i = 0; i < s2.Length; i++)

      // Update the frequency
      cnt[s2[i] - 'a']++;

    // Find the number of unique
    // characters in s2
    int unique = 0;
    for (int i = 0; i < 26; i++)

      // Increment unique by 1 if the
      // condition satisfies
      if (cnt[i] != 0)
        unique++;

    // Check if the number of unique
    // characters in string s2 is 1
    if (unique == 1) {

      // Store the unique character
      // frequency
      int count_in_s2 = s2.Length;

      // Store occurence of it in s1
      int count_in_s1 = 0;

      // Find count of that character
      // in the string s1
      for (int i = 0; i < s1.Length; i++)

        // Increment count by 1 if
        // that unique character is
        // same as current character
        if (s1[i] == s2[0])
          count_in_s1++;

      // If count count_in_s1 is
      // less than count_in_s2, then
      // print s1 and return
      if (count_in_s1 < count_in_s2) {
        Console.Write(new string(s1));
        return;
      }

      // Otherwise, there is no
      // possible arrangement
      Console.Write(-1);
    }
    else {

      // Checks if any character in
      // s2 is less than its next
      // character
      int inc = 1;

      // Iterate the string, s2
      for (int i = 0; i < s2.Length - 1; i++)

        // If s[i] is greater
        // than the s[i+1]
        if (s2[i] > s2[i + 1])

          // Set inc to 0
          inc = 0;

      // If inc=1, print s1 in
      // decreasing order
      if (inc == 1) {
        Array.Sort(s1);
        Array.Reverse(s1);
        Console.Write(new string(s1));
      }

      // Otherwise, print s1 in
      // increasing order
      else {
        Array.Sort(s1);
        Console.Write(new string(s1));
      }
    }
  }

  // Driver code
  static void Main() {
    char[] s1 = "abcd".ToCharArray();
    char[] s2 = "ab".ToCharArray();
    rearrangeString(s1, s2);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to rearrange characters
    // in string S1 such that S2 is not
    // a subsequence of it
    function rearrangeString(s1, s2)
    {

      // Store the frequencies of
      // characters of string s2
      let cnt = new Array(26);
      cnt.fill(0);

      // Traverse the string s2
      for (let i = 0; i < s2.length; i++)

        // Update the frequency
        cnt[s2[i].charCodeAt() -
           'a'.charCodeAt()]++;

      // Find the number of unique
      // characters in s2
      let unique = 0;
      for (let i = 0; i < 26; i++)

        // Increment unique by 1 if the
        // condition satisfies
        if (cnt[i] != 0)
          unique++;

      // Check if the number of unique
      // characters in string s2 is 1
      if (unique == 1) {

        // Store the unique character
        // frequency
        let count_in_s2 = s2.length;

        // Store occurence of it in s1
        let count_in_s1 = 0;

        // Find count of that character
        // in the string s1
        for (let i = 0; i < s1.length; i++)

          // Increment count by 1 if
          // that unique character is
          // same as current character
          if (s1[i] == s2[0])
            count_in_s1++;

        // If count count_in_s1 is
        // less than count_in_s2, then
        // print s1 and return
        if (count_in_s1 < count_in_s2) {
          document.write(s1.join(""));
          return;
        }

        // Otherwise, there is no
        // possible arrangement
        document.write(-1);
      }
      else {

        // Checks if any character in
        // s2 is less than its next
        // character
        let inc = 1;

        // Iterate the string, s2
        for (let i = 0; i < s2.length - 1; i++)

          // If s[i] is greater
          // than the s[i+1]
          if (s2[i].charCodeAt() >
              s2[i + 1].charCodeAt())

            // Set inc to 0
            inc = 0;

        // If inc=1, print s1 in
        // decreasing order
        if (inc == 1) {
          s1.sort();
          s1.reverse();
          document.write(s1.join(""));
        }

        // Otherwise, print s1 in
        // increasing order
        else {
          s1.sort();
          document.write(s1.join(""));
        }
      }
    }

    let s1 = "abcd".split('');
    let s2 = "ab".split('');
    rearrangeString(s1, s2);

</script>
```

**Output:** 

```
dcba
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*