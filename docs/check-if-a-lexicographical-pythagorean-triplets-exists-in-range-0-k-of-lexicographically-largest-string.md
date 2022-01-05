# 检查字典序毕达哥拉斯三元组是否存在于字典序最大字符串

的范围[0，K]内

> 原文:[https://www . geeksforgeeks . org/check-if-a-字典序-毕达哥拉斯-三元组-存在范围-0-k-of-字典序-最大-字符串/](https://www.geeksforgeeks.org/check-if-a-lexicographical-pythagorean-triplets-exists-in-range-0-k-of-lexicographically-largest-string/)

给定一个字符串**字符串**和一个正整数 **K** 。任务是在大小为 K 的第一个窗口**中找出是否存在一个与 str 具有相同字符但在字典顺序中最大的字符串**。****

**注意:**每个字符都是小写，考虑每个字母表的以下值，检查是否存在毕达哥拉斯三元组:a = 1，b = 2，。。。，y = 25，z = 26。

> 一个三元组(ch <sub>1</sub> ，ch <sub>2</sub> ，ch <sub>3</sub> )叫做毕达哥拉斯三元组如果(ch<sub>1</sub>)<sup>2</sup><sub>+(ch<sub>2</sub>)<sup>2</sup>=(ch<sub>3</sub>)<sup>2</sup>。</sub>

**示例:**

> **输入:** str = "abxczde "，K = 4
> **输出:** NO
> **说明:**具有相同字符的字典上最大的字符串是 zxedcba。
> 大小为 4 的第一个窗口为“zxed”，不包含任何这样的三元组。
> 
> **输入:** str = "abcdef "，K = 4
> **输出:** YES
> **解释:**可能的字典上最大的字符串是“fedcba”。
> 第一个大小为 4 的窗口有“fedc”，它有一个三重体(c，d，e)，是毕达哥拉斯的。
> 
> **输入:** str = "dce "，K = 2
> **输出:**否
> **说明:**由于窗口大小小于 3，选择三重是不可能的。

**方法:**这个问题可以用[贪婪算法](http://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤进行操作:

*   [给定字符串按降序排序](https://www.geeksforgeeks.org/program-sort-string-descending-order/)。
*   在**子串** *0 到 K-1* 中，检查是否存在字典序毕达哥拉斯三元组，使用 [**两个指针**](https://www.geeksforgeeks.org/two-pointers-technique/) 的方法。
*   如果找到任何这样的三元组，打印“是”并返回。否则打印号。

以下是该方法的实施情况:

## C++

```
// C++ code to implementat the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check for
// Lexicographical Pythagorean triplet
bool Pythagorean(string s, int k)
{
    // If k is less than 3 no triple possible
    if (k < 3) {
        return false;
    }

    // Sort the string in descending order
    sort(s.begin(), s.end(), greater<char>());

    // Loop to check Pythagorean triples
    for (int i = 0; i < k - 2; ++i) {

        // Variables to define boundary of window
        int r = k - 1;
        int l = i + 1;

        // Loop for using two pointer approach
        // to find the other two elements
        while (r > l) {
            int a = pow(s[i] - 'a' + 1, 2);
            int b = pow(s[l] - 'a' + 1, 2);
            int c = pow(s[r] - 'a' + 1, 2);

            // If triple is found
            if (a == b + c) {
                return true;
            }

            // If 'a' is greater
            else if (a > b + c) {
                r--;
            }

            // If 'a' is less
            else
                l++;
        }
    }

    // No such triple found
    return false;
}

// Driver code
int main()
{
    string str = "abcdef";
    int K = 4;
    bool ans = Pythagorean(str, K);
    if (ans)
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implementat the above approach
import java.util.*;

public class GFG
{
// Utility function to reverse an array
static void reverse(char[] a)
{
    int i, n = a.length;
    char t;
    for (i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}   

// Function to check for
// Lexicographical Pythagorean triplet
static boolean Pythagorean(String str, int k)
{
    // If k is less than 3 no triple possible
    if (k < 3) {
        return false;
    }

    // Sort the string in descending order
    char[] s = str.toCharArray();
    Arrays.sort(s);
    reverse(s);

    // Loop to check Pythagorean triples
    for (int i = 0; i < k - 2; ++i) {

        // Variables to define boundary of window
        int r = k - 1;
        int l = i + 1;

        // Loop for using two pointer approach
        // to find the other two elements
        while (r > l) {
            int a = (int)Math.pow(s[i] - 'a' + 1, 2);
            int b = (int)Math.pow(s[l] - 'a' + 1, 2);
            int c = (int)Math.pow(s[r] - 'a' + 1, 2);

            // If triple is found
            if (a == b + c) {
                return true;
            }

            // If 'a' is greater
            else if (a > b + c) {
                r--;
            }

            // If 'a' is less
            else
                l++;
        }
    }

    // No such triple found
    return false;
}

// Driver code
public static void main(String args[])
{
    String str = "abcdef";
    int K = 4;
    boolean ans = Pythagorean(str, K);
    if (ans)
        System.out.println("YES");
    else
        System.out.println("NO");
}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to check for
# Lexicographical Pythagorean triplet
def Pythagorean(st, k):

    # If k is less than 3 no triple possible
    if (k < 3):
        return False

    # Sort the string in descending order
    s = []
    for i in range(len(st)):
         s.append(st[i])
    s.sort()
    s.reverse()

    # Loop to check Pythagorean triples
    for i in range(k - 2):
        # Variables to define boundary of window
        r = k - 1
        l = i + 1

        # Loop for using two pointer approach
        # to find the other two elements
        while (r > l):
            a = pow(ord(s[i]) - ord('a') + 1, 2)
            b = pow(ord(s[l]) - ord('a') + 1, 2)
            c = pow(ord(s[r]) - ord('a') + 1, 2)

            # If triple is found
            if (a == b + c):
                return True

            # If 'a' is greater
            elif (a > b + c) :
                r -= 1

            # If 'a' is less
            else:
                l += 1

    # No such triple found
    return False

# Driver code
str = "abcdef"
K = 4
ans = Pythagorean(str, K)
if (ans):
    print("YES")
else:
    print("NO")

# This code is contributed by gfgking
```

## C#

```
// C# code to implementat the above approach
using System;

public class GFG
{
// Utility function to reverse an array
static void reverse(char[] a)
{
    int i, n = a.Length;
    char t;
    for (i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}   

// Function to check for
// Lexicographical Pythagorean triplet
static bool Pythagorean(string str, int k)
{
    // If k is less than 3 no triple possible
    if (k < 3) {
        return false;
    }

    // Sort the string in descending order
    char[] s = str.ToCharArray();
    Array.Sort(s);
    reverse(s);

    // Loop to check Pythagorean triples
    for (int i = 0; i < k - 2; ++i) {

        // Variables to define boundary of window
        int r = k - 1;
        int l = i + 1;

        // Loop for using two pointer approach
        // to find the other two elements
        while (r > l) {
            int a = (int)Math.Pow(s[i] - 'a' + 1, 2);
            int b = (int)Math.Pow(s[l] - 'a' + 1, 2);
            int c = (int)Math.Pow(s[r] - 'a' + 1, 2);

            // If triple is found
            if (a == b + c) {
                return true;
            }

            // If 'a' is greater
            else if (a > b + c) {
                r--;
            }

            // If 'a' is less
            else
                l++;
        }
    }

    // No such triple found
    return false;
}

// Driver code
public static void Main()
{
    string str = "abcdef";
    int K = 4;
    bool ans = Pythagorean(str, K);
    if (ans)
        Console.Write("YES");
    else
        Console.Write("NO");
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

      // JavaScript Program to implement
      // the above approach

      // Function to check for
      // Lexicographical Pythagorean triplet
      function Pythagorean(st, k)
      {

          // If k is less than 3 no triple possible
          if (k < 3) {
              return false;
          }

          // Sort the string in descending order
          s = [];
          for (let i = 0; i < st.length; i++) { s.push(st.charAt(i)); }
          s.sort(function (a, b) { return b.charCodeAt(0) - a.charCodeAt(0) })

          // Loop to check Pythagorean triples
          for (let i = 0; i < k - 2; ++i) {

              // Variables to define boundary of window
              let r = k - 1;
              let l = i + 1;

              // Loop for using two pointer approach
              // to find the other two elements
              while (r > l) {
                  let a = Math.pow(s[i].charCodeAt(0) - 'a'.charCodeAt(0) + 1, 2);
                  let b = Math.pow(s[l].charCodeAt(0) - 'a'.charCodeAt(0) + 1, 2);
                  let c = Math.pow(s[r].charCodeAt(0) - 'a'.charCodeAt(0) + 1, 2);
                  5
                  // If triple is found
                  if (a == b + c) {
                      return true;
                  }

                  // If 'a' is greater
                  else if (a > b + c) {
                      r--;
                  }

                  // If 'a' is less
                  else
                      l++;
              }
          }

          // No such triple found
          return false;
      }

      // Driver code
      let str = "abcdef";
      let K = 4;
      let ans = Pythagorean(str, K);
      if (ans)
          document.write("YES");
      else
          document.write("NO");

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
YES
```

**时间复杂度:**O(K<sup>2</sup>)
T5】辅助空间: O(1)