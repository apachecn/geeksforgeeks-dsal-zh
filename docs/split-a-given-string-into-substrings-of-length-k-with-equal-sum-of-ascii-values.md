# 将一个给定的字符串分割成长度为 K 的子串，并且 ASCII 值的总和相等

> 原文:[https://www . geeksforgeeks . org/将给定字符串拆分为长度为 k 且 ascii 值总和相等的子字符串/](https://www.geeksforgeeks.org/split-a-given-string-into-substrings-of-length-k-with-equal-sum-of-ascii-values/)

给定一个大小为 **N** 的字符串 **str** 和一个整数 **K** ，任务是检查输入字符串是否可以划分为大小为 **K** 的子字符串，这些子字符串具有恒定的 ASCII 值之和。
**举例:**

> **输入:** str = "abdcbbdba" K = 3
> **输出:** YES
> **解释:**
> 3 个长度子串{ " and " " cbb " " DBA " }它们的 ASCII 值之和等于 295。
> **输入:**str = " ababcdabas " K = 5
> **输出:** NO
> **解释:**
> 5 个长度子串{“ababc”、“dabas”}其 ASCII 值之和等于 507。

**进场:**
按照以下步骤解决问题:

1.  检查 **N** 是否能被 **K** 整除。如果 **N** 不能被 **K** 整除，那么不可能所有子串的长度都是 K
2.  计算长度为 **K** 的所有子串的 ASCII 和。如果只为所有子字符串生成一个总和，则打印“是”。
3.  否则，打印“否”。

以下是上述方法的实现:

## C++

```
// C++ program to check if a given
// string can be split into substrings
// of size K having an equal sum of
// ASCII values.
#include <bits/stdc++.h>
using namespace std;

// Function for checking string
bool check(string str, int K)
{
    // Check if the string can
    // be split into substrings
    // of K length only
    if (str.size() % K == 0) {
        int sum = 0, i;

        // Compute the sum of first
        // substring of length K
        for (i = 0; i < K; i++) {
            sum += str[i];
        }
        // Compute the sum of
        // remaining substrings
        for (int j = i; j < str.size();
             j += K) {
            int s_comp = 0;
            for (int p = j; p < j + K;
                 p++)
                s_comp += str[p];
            // Check if sum is equal
            // to that of the first
            // substring
            if (s_comp != sum)
                // Since all sums are not
                // equal, return false
                return false;
        }
        // All sums are equal,
        // Return true
        return true;
    }
    // All substrings cannot
    // be of size K
    return false;
}
// Driver Program
int main()
{

    int K = 3;
    string str = "abdcbbdba";

    if (check(str, K))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given
// string can be split into substrings
// of size K having an equal sum of
// ASCII values.
class GFG{

// Function for checking string
static boolean check(String str, int K)
{

    // Check if the string can
    // be split into substrings
    // of K length only
    if (str.length() % K == 0)
    {
        int sum = 0, i;

        // Compute the sum of first
        // substring of length K
        for(i = 0; i < K; i++)
        {
           sum += str.charAt(i);
        }

        // Compute the sum of
        // remaining substrings
        for(int j = i; j < str.length(); j += K)
        {
           int s_comp = 0;
           for(int p = j; p < j + K; p++)
              s_comp += str.charAt(p);

           // Check if sum is equal
           // to that of the first
           // substring
           if (s_comp != sum)

               // Since all sums are not
               // equal, return false
               return false;
        }

        // All sums are equal,
        // Return true
        return true;
    }

    // All substrings cannot
    // be of size K
    return false;
}

// Driver code
public static void main(String args[])
{
    int K = 3;
    String str = "abdcbbdba";

    if (check(str, K))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to check if a given
# string can be split into substrings
# of size K having an equal sum of
# ASCII values.

# Function for checking string
def check(str, K):

    # Check if the string can
    # be split into substrings
    # of K length only
    if (len(str) % K == 0):
        sum = 0

        # Compute the sum of first
        # substring of length K
        for i in range(K):
            sum += ord(str[i]);

        # Compute the sum of
        # remaining substrings
        for j in range(K, len(str), K):
            s_comp = 0;
            for p in range(j, j + K):
                s_comp += ord( str[p]);

            # Check if sum is equal
            # to that of the first
            # substring
            if (s_comp != sum):

                # Since all sums are not
                # equal, return False
                return False;

        # All sums are equal,
        # Return true
        return True;

    # All substrings cannot
    # be of size K
    return False;

# Driver code
K = 3;
str = "abdcbbdba";

if (check(str, K)):
    print("YES")
else:
    print("NO")

# This is code contributed by grand_master
```

## C#

```
// C# program to check if a given
// string can be split into substrings
// of size K having an equal sum of
// ASCII values.
using System;
class GFG{

// Function for checking string
static bool check(string str, int K)
{

    // Check if the string can
    // be split into substrings
    // of K length only
    if (str.Length % K == 0)
    {
        int sum = 0, i;

        // Compute the sum of first
        // substring of length K
        for(i = 0; i < K; i++)
        {
            sum += str[i];
        }

        // Compute the sum of
        // remaining substrings
        for(int j = i; j < str.Length; j += K)
        {
            int s_comp = 0;
            for(int p = j; p < j + K; p++)
                s_comp += str[p];

            // Check if sum is equal
            // to that of the first
            // substring
            if (s_comp != sum)

                // Since all sums are not
                // equal, return false
                return false;
        }

        // All sums are equal,
        // Return true
        return true;
    }

    // All substrings cannot
    // be of size K
    return false;
}

// Driver code
public static void Main(string []args)
{
    int K = 3;
    string str = "abdcbbdba";

    if (check(str, K))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>
      // JavaScript program to check if a given
      // string can be split into substrings
      // of size K having an equal sum of
      // ASCII values.
      // Function for checking string
      function check(str, K) {
        // Check if the string can
        // be split into substrings
        // of K length only
        if (str.length % K === 0) {
          var sum = 0,
            i;

          // Compute the sum of first
          // substring of length K
          for (i = 0; i < K; i++) {
            sum += str[i].charCodeAt(0);
          }

          // Compute the sum of
          // remaining substrings
          for (var j = i; j < str.length; j += K) {
            var s_comp = 0;
            for (var p = j; p < j + K; p++) s_comp += str[p].charCodeAt(0);

            // Check if sum is equal
            // to that of the first
            // substring
            if (s_comp !== sum)
              // Since all sums are not
              // equal, return false
              return false;
          }

          // All sums are equal,
          // Return true
          return true;
        }

        // All substrings cannot
        // be of size K
        return false;
      }

      // Driver code
      var K = 3;
      var str = "abdcbbdba";

      if (check(str, K)) document.write("YES");
      else document.write("NO");
    </script>
```

**Output:** 

```
YES
```

***时间复杂度:** O (N)*
***辅助空间:** O (1)*