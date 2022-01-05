# 最小替换，使得相同字符的索引之间的差异可被 3 整除

> 原文:[https://www . geeksforgeeks . org/最小替换-相同字符的索引之间的差异可被 3 整除/](https://www.geeksforgeeks.org/minimum-replacements-such-that-the-difference-between-the-index-of-the-same-characters-is-divisible-by-3/)

给定一个由“0”、“1”和“2”组成的字符串。任务是找到字符串中的最小替换，以便相同字符的索引之间的差异可以被 3 整除。
**例:**

> **输入:** s = "2101200"
> **输出:** 3
> 1201201 或 2102102 可以是有 3 个替换的合成字符串
> 。
> **输入:** s = "012"
> **输出:** 0

**方法:**可以有 6 个不同的字符串，这样相似字符的索引之间的差异可以被 3 整除。因此，生成所有 6 个不同的字符串，并将替换字符串与原始字符串进行比较。存储替换次数最少的字符串。不同的字符串可以使用 C++中的[next _ arrangement](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)生成。
以下是上述方法的实施:

## C++

```
// C++ program to find minimum replacements
// such that the difference between the
// index of the same characters
// is divisible by 3
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// minimal replacements
int countMinimalReplacements(string s)
{

    int n = s.length();

    int mini = INT_MAX;
    string dup = "012";

    // Generate all permutations
    do {

        // Count the replacements
        int dif = 0;
        for (int i = 0; i < n; i++)
            if (s[i] != dup[i % 3])
                dif++;

        mini = min(mini, dif);
    } while (next_permutation(dup.begin(), dup.end()));

    // Return the replacements
    return mini;
}

// Driver Code
int main()
{
    string s = "2101200";
    cout << countMinimalReplacements(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum replacements
// such that the difference between the
// index of the same characters
// is divisible by 3
class GFG {

    // Function to count the number of
    // minimal replacements
    static int countMinimalReplacements(String s)
    {

        int n = s.length();

        int mini = Integer.MAX_VALUE;
        char[] dup = "012".toCharArray();

        // Generate all permutations
        do {

            // Count the replacements
            int dif = 0;
            for (int i = 0; i < n; i++) {
                if (s.charAt(i) != dup[i % 3]) {
                    dif++;
                }
            }

            mini = Math.min(mini, dif);
        } while (next_permutation(dup));

        // Return the replacements
        return mini;
    }

    static boolean next_permutation(char[] p)
    {
        for (int a = p.length - 2; a >= 0; --a) {
            if (p[a] < p[a + 1]) {
                for (int b = p.length - 1;; --b) {
                    if (p[b] > p[a]) {
                        char t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                        for (++a, b = p.length - 1; a < b; ++a, --b) {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }
                }
            }
        }
        return false;
    }

    // Driver Code
    public static void main(String args[])
    {
        String s = "2101200";
        System.out.println(countMinimalReplacements(s));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## C#

```
// C# program to find minimum replacements
// such that the difference between the
// index of the same characters
// is divisible by 3
using System;

class GFG {

    // Function to count the number of
    // minimal replacements
    static int countMinimalReplacements(String s)
    {

        int n = s.Length;

        int mini = int.MaxValue;
        char[] dup = "012".ToCharArray();

        // Generate all permutations
        do {

            // Count the replacements
            int dif = 0;
            for (int i = 0; i < n; i++) {
                if (s[i] != dup[i % 3]) {
                    dif++;
                }
            }

            mini = Math.Min(mini, dif);
        } while (next_permutation(dup));

        // Return the replacements
        return mini;
    }

    static bool next_permutation(char[] p)
    {
        for (int a = p.Length - 2; a >= 0; --a) {
            if (p[a] < p[a + 1]) {
                for (int b = p.Length - 1;; --b) {
                    if (p[b] > p[a]) {
                        char t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                        for (++a, b = p.Length - 1; a < b; ++a, --b) {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }
                }
            }
        }
        return false;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "2101200";
        Console.WriteLine(countMinimalReplacements(s));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript program to find minimum replacements
      // such that the difference between the
      // index of the same characters
      // is divisible by 3
      // Function to count the number of
      // minimal replacements
      function countMinimalReplacements(s) {
        var n = s.length;

        //Max Integer Value
        var mini = 2147483647;
        var dup = "012".split("");

        // Generate all permutations
        do {
          // Count the replacements
          var dif = 0;
          for (var i = 0; i < n; i++) {
            if (s[i] !== dup[i % 3]) {
              dif++;
            }
          }

          mini = Math.min(mini, dif);
        } while (next_permutation(dup));

        // Return the replacements
        return mini;
      }

      function next_permutation(p) {
        for (var a = p.length - 2; a >= 0; --a) {
          if (p[a] < p[a + 1]) {
            for (var b = p.length - 1; ; --b) {
              if (p[b] > p[a]) {
                var t = p[a];
                p[a] = p[b];
                p[b] = t;
                for (++a, b = p.length - 1; a < b; ++a, --b) {
                  t = p[a];
                  p[a] = p[b];
                  p[b] = t;
                }
                return true;
              }
            }
          }
        }
        return false;
      }

      // Driver Code
      var s = "2101200";
      document.write(countMinimalReplacements(s));
    </script>
```

**Output:** 

```
3
```