# 检查 K '0 '是否可以翻转，使得二进制字符串不包含一对相邻的' 1 '

> 原文:[https://www . geeksforgeeks . org/check-if-k-0s-可翻转-这样-二进制字符串-包含-无对相邻-1s/](https://www.geeksforgeeks.org/check-if-k-0s-can-be-flipped-such-that-binary-string-contains-no-pair-of-adjacent-1s/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和一个整数 **K** ，任务是检查是否有可能翻转 **K** **0s** ，使得生成的字符串不包含任何一对相邻的 **1s** 。如果可以，则打印**“是”**。否则，打印**“否”**。

> **输入:**S =“01001001000”，K = 1
> **输出:**是
> **解释:**
> 修改 S =“0100100100**0**到“01001001001”或者修改 S =“010010010**0**0”到“010010010010【T10
> 
> **输入:**S =“000001000”，K = 4
> T3】输出:否

**方法:**想法是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并用两个相邻字符都为“**0′**的“**0′**替换那些“**1′**s”，并翻转其中一个“**0′**s，以计算所有可能的翻转位置，从而不影响原始字符串。按照以下步骤解决问题:

*   初始化 s 变量，说 **cnt** 为 **0，**存储可以翻转的位置数。
*   [使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并执行以下步骤:
    *   如果当前字符是“**1′**，那么将 **i** 增加 **2** 。
    *   否则:
        *   **如果 i = 0，s[i + 1] = '0':** 将 **cnt** 增加 **1** 和 **i** 增加 **2** 。否则，将 **i** 增加 **1** 。
        *   **如果 I =(N–1)，并且 s[I–1]= ' 0 ':**将 **cnt** 增加 **1** ，将 **i** 增加 **2** 。否则，将 **i** 增加 **1** 。
        *   否则，**如果 s[i + 1] = '0 '和 s[I–1]= ' 0 ':**将 **cnt** 增加 **1** 和 **i** 增加 **2。**否则，将 **i** 增加 **1** 。
*   完成上述步骤后，如果 **cnt** 的值至少为 **K、**，则打印**“是”**，否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if k '0's can
// be flipped such that the string
// does not contain any pair of adjacent '1's
void canPlace(string s, int n, int k)
{
    // Store the count of flips
    int cnt = 0;

    // Variable to iterate the string
    int i = 0;

    // Iterate over characters
    // of the string
    while (i < n) {

        // If the current character
        // is '1', increment i by 2
        if (s[i] == '1') {
            i += 2;
        }

        // Otherwise, 3 cases arises
        else {

            // If the current index
            // is the starting index
            if (i == 0) {

                // If next character is '0'
                if (s[i + 1] == '0') {
                    cnt++;
                    i += 2;
                }

                // Increment i by 1
                else
                    i++;
            }

            // If the current index
            // is the last index
            else if (i == n - 1) {

                // If previous character is '0'
                if (s[i - 1] == '0') {

                    cnt++;
                    i += 2;
                }
                else
                    i++;
            }

            // For remaining characters
            else {

                // If both the adjacent
                // characters are '0'
                if (s[i + 1] == '0' && s[i - 1] == '0') {

                    cnt++;
                    i += 2;
                }
                else
                    i++;
            }
        }
    }

    // If cnt is at least K, print "Yes"
    if (cnt >= k) {
        cout << "Yes";
    }

    // Otherwise, print "No"
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    string S = "10001";
    int K = 1;
    int N = S.size();

    canPlace(S, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
class GFG
{

  // Function to check if k '0's can
  // be flipped such that the string
  // does not contain any pair of adjacent '1's
  public static void canPlace(String s, int n, int k)
  {

    // Store the count of flips
    int cnt = 0;

    // Variable to iterate the string
    int i = 0;

    // Iterate over characters
    // of the string
    while (i < n)
    {

      // If the current character
      // is '1', increment i by 2
      if (s.charAt(i) == '1')
      {
        i += 2;
      }

      // Otherwise, 3 cases arises
      else
      {

        // If the current index
        // is the starting index
        if (i == 0)
        {

          // If next character is '0'
          if (s.charAt(i + 1) == '0')
          {
            cnt++;
            i += 2;
          }

          // Increment i by 1
          else
            i++;
        }

        // If the current index
        // is the last index
        else if (i == n - 1)
        {

          // If previous character is '0'
          if (s.charAt(i - 1) == '0')
          {

            cnt++;
            i += 2;
          }
          else
            i++;
        }

        // For remaining characters
        else
        {

          // If both the adjacent
          // characters are '0'
          if (s.charAt(i + 1) == '0' && s.charAt(i - 1) == '0')
          {

            cnt++;
            i += 2;
          }
          else
            i++;
        }
      }
    }

    // If cnt is at least K, print "Yes"
    if (cnt >= k)
    {
      System.out.println("Yes");
    }

    // Otherwise, print "No"
    else
    {
      System.out.println("No");
    }
  }

  // Driver code
  public static void main (String[] args)
  {
    String S = "10001";
    int K = 1;
    int N = 5;
    canPlace(S, N, K);
  }
}

// This code is contributed by manupatharia.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if k '0's can
# be flipped such that the string
# does not contain any pair of adjacent '1's
def canPlace(s, n, k) :

    # Store the count of flips
    cnt = 0

    # Variable to iterate the string
    i = 0

    # Iterate over characters
    # of the string
    while (i < n) :

      # If the current character
      # is '1', increment i by 2
      if (s[i] == '1') :
        i += 2

      # Otherwise, 3 cases arises
      else :

        # If the current index
        # is the starting index
        if (i == 0) :

          # If next character is '0'
          if (s[i + 1] == '0') :
            cnt += 1
            i += 2

          # Increment i by 1
          else :
            i += 1

        # If the current index
        # is the last index
        elif (i == n - 1) :

          # If previous character is '0'
          if (s[i - 1] == '0') :

            cnt += 1
            i += 2

          else :
            i += 1

        # For remaining characters
        else :

          # If both the adjacent
          # characters are '0'
          if (s[i + 1] == '0' and s[i - 1] == '0') :

            cnt += 1
            i += 2

          else :
            i += 1

    # If cnt is at least K, print "Yes"
    if (cnt >= k) :

      print("Yes")

    # Otherwise, print "No"
    else :

      print("No")

      # Driver code
S = "10001"
K = 1
N = len(S)

canPlace(S, N, K)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to check if k '0's can
  // be flipped such that the string
  // does not contain any pair of adjacent '1's
  static void canPlace(string s, int n, int k)
  {

    // Store the count of flips
    int cnt = 0;

    // Variable to iterate the string
    int i = 0;

    // Iterate over characters
    // of the string
    while (i < n) {

      // If the current character
      // is '1', increment i by 2
      if (s[i] == '1') {
        i += 2;
      }

      // Otherwise, 3 cases arises
      else {

        // If the current index
        // is the starting index
        if (i == 0) {

          // If next character is '0'
          if (s[i + 1] == '0') {
            cnt++;
            i += 2;
          }

          // Increment i by 1
          else
            i++;
        }

        // If the current index
        // is the last index
        else if (i == n - 1) {

          // If previous character is '0'
          if (s[i - 1] == '0') {

            cnt++;
            i += 2;
          }
          else
            i++;
        }

        // For remaining characters
        else {

          // If both the adjacent
          // characters are '0'
          if (s[i + 1] == '0' && s[i - 1] == '0') {

            cnt++;
            i += 2;
          }
          else
            i++;
        }
      }
    }

    // If cnt is at least K, print "Yes"
    if (cnt >= k)
    {
      Console.WriteLine("Yes");
    }

    // Otherwise, print "No"
    else
    {
      Console.WriteLine("No");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    string S = "10001";
    int K = 1;
    int N = S.Length;

    canPlace(S, N, K);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>
/*package whatever //do not write package name here */
  // Function to check if k '0's can
  // be flipped such that the string
  // does not contain any pair of adjacent '1's
  function canPlace(s,  n,  k)
  {

    // Store the count of flips
    var cnt = 0;

    // Variable to iterate the string
    var i = 0;

    // Iterate over characters
    // of the string
    while (i < n)
    {

      // If the current character
      // is '1', increment i by 2
      if (s.charAt(i) == '1')
      {
        i += 2;
      }

      // Otherwise, 3 cases arises
      else
      {

        // If the current index
        // is the starting index
        if (i == 0)
        {

          // If next character is '0'
          if (s.charAt(i + 1) == '0')
          {
            cnt++;
            i += 2;
          }

          // Increment i by 1
          else
            i++;
        }

        // If the current index
        // is the last index
        else if (i == n - 1)
        {

          // If previous character is '0'
          if (s.charAt(i - 1) == '0')
          {

            cnt++;
            i += 2;
          }
          else
            i++;
        }

        // For remaining characters
        else
        {

          // If both the adjacent
          // characters are '0'
          if (s.charAt(i + 1) == '0' && s.charAt(i - 1) == '0')
          {

            cnt++;
            i += 2;
          }
          else
            i++;
        }
      }
    }

    // If cnt is at least K, print "Yes"
    if (cnt >= k)
    {
      document.write("Yes");
    }

    // Otherwise, print "No"
    else
    {
      document.write("No");
    }
  }

  // Driver code
    var S = "10001";
    var K = 1;
    var N = 5;
    canPlace(S, N, K);

// This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(n)*
T5**辅助空间:** O(1)