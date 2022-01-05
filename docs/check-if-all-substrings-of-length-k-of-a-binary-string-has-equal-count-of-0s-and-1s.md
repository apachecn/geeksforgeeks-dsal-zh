# 检查一个二进制串的长度为 K 的所有子串是否具有相等的 0 和 1 的计数

> 原文:[https://www . geesforgeks . org/check-if-all-length-k-of-a-binary-string-具有相等的-0 和-1 计数/](https://www.geeksforgeeks.org/check-if-all-substrings-of-length-k-of-a-binary-string-has-equal-count-of-0s-and-1s/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和一个偶数 **K** ，任务是检查长度为 **K** 的所有子字符串是否包含相同数量的 **0** s 和 **1** s。如果发现为真，则打印“是”。否则，打印“否”。

**示例:**

> **输入:**S =“101010”，K = 2
> **输出:**是
> **说明:**
> 由于长度为 2 的所有子串的 0 和 1 个数相等，所以答案为是。
> 
> **输入:**S =“101011”，K = 4
> **输出:**否
> **说明:**
> 由于子串“1011”有 0 和 1 不等的计数，所以答案是否..

**天真方法:**解决问题最简单的方法是[生成所有长度为 K 的子串](https://www.geeksforgeeks.org/print-all-combinations-of-given-length/)，并检查它是否包含 1 和 0 的相等计数。

***时间复杂度:**O(N<sup>2</sup>)*
T7】辅助空间: O(1)

**高效方法:**优化上述方法的主要观察是，对于长度为 **K** 、**S【I】**的子串，串 S 的计数要等于 0 和 1，必须等于**S【I+K】**。按照以下步骤解决问题:

*   遍历字符串，对于每个 i <sup>第</sup>个字符，检查是否**S【I】= S【j】**其中 **(i == (j % k))**
*   如果在任何时刻发现是假的，那么打印“否”。
*   否则，检查长度为 K 的第一个子字符串，以及它是否包含相等数量的 1 和 0。如果发现是真的，那么打印“是”。否则，打印“否”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check if the substring
// of length K has equal 0 and 1
int check(string& s, int k)
{
    int n = s.size();

    // Traverse the string
    for (int i = 0; i < k; i++) {
        for (int j = i; j < n; j += k) {

            // Check if every K-th character
            // is the same or not
            if (s[i] != s[j])
                return false;
        }
    }
    int c = 0;

    // Traverse substring of length K
    for (int i = 0; i < k; i++) {

        // If current character is 0
        if (s[i] == '0')

            // Increment count
            c++;

        // Otherwise
        else

            // Decrement count
            c--;
    }

    // Check for equal 0s and 1s
    if (c == 0)
        return true;
    else
        return false;
}

// Driver code
int main()
{
    string s = "101010";
    int k = 2;

    if (check(s, k))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to check if the substring
// of length K has equal 0 and 1
static boolean check(String s, int k)
{
  int n = s.length();

  // Traverse the String
  for (int i = 0; i < k; i++)
  {
    for (int j = i; j < n; j += k)
    {
      // Check if every K-th character
      // is the same or not
      if (s.charAt(i) != s.charAt(j))
        return false;
    }
  }
  int c = 0;

  // Traverse subString of length K
  for (int i = 0; i < k; i++)
  {
    // If current character is 0
    if (s.charAt(i) == '0')

      // Increment count
      c++;

    // Otherwise
    else

      // Decrement count
      c--;
  }

  // Check for equal 0s and 1s
  if (c == 0)
    return true;
  else
    return false;
}

// Driver code
public static void main(String[] args)
{
  String s = "101010";
  int k = 2;

  if (check(s, k))
    System.out.print("Yes" + "\n");
  else
    System.out.print("No" + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the substring
# of length K has equal 0 and 1
def check(s, k):

    n = len(s)

    # Traverse the string
    for i in range(k):
        for j in range(i, n, k):

            # Check if every K-th character
            # is the same or not
            if (s[i] != s[j]):
                return False

    c = 0

    # Traverse substring of length K
    for i in range(k):

        # If current character is 0
        if (s[i] == '0'):

            # Increment count
            c += 1

        # Otherwise
        else:

            # Decrement count
            c -= 1

    # Check for equal 0s and 1s
    if (c == 0):
        return True
    else:
        return False

# Driver code
s = "101010"
k = 2

if (check(s, k) != 0):
    print("Yes")
else:
    print("No")

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to check if the substring
// of length K has equal 0 and 1
static bool check(String s, int k)
{
  int n = s.Length;

  // Traverse the String
  for (int i = 0; i < k; i++)
  {
    for (int j = i; j < n; j += k)
    {
      // Check if every K-th character
      // is the same or not
      if (s[i] != s[j])
        return false;
    }
  }
  int c = 0;

  // Traverse subString of length K
  for (int i = 0; i < k; i++)
  {
    // If current character is 0
    if (s[i] == '0')

      // Increment count
      c++;

    // Otherwise
    else

      // Decrement count
      c--;
  }

  // Check for equal 0s and 1s
  if (c == 0)
    return true;
  else
    return false;
}

// Driver code
public static void Main(String[] args)
{
  String s = "101010";
  int k = 2;

  if (check(s, k))
    Console.Write("Yes" + "\n");
  else
    Console.Write("No" + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to check if the substring
// of length K has equal 0 and 1
function check(s, k)
{
  let n = s.length;

  // Traverse the String
  for (let i = 0; i < k; i++)
  {
    for (let j = i; j < n; j += k)
    {
      // Check if every K-th character
      // is the same or not
      if (s[i] != s[j])
        return false;
    }
  }
  let c = 0;

  // Traverse subString of length K
  for (let i = 0; i < k; i++)
  {
    // If current character is 0
    if (s[i]== '0')

      // Increment count
      c++;

    // Otherwise
    else

      // Decrement count
      c--;
  }

  // Check for equal 0s and 1s
  if (c == 0)
    return true;
  else
    return false;
}

// Driver Code

     let s = "101010";
  let k = 2;

  if (check(s, k))
    document.write("Yes" + "<br/>");
  else
    document.write("No");

// This code is contributed by target_2.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)