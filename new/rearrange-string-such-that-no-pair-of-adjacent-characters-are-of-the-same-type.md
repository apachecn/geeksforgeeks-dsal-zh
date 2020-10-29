# 重新排列字符串，以使相邻的字符对都不属于同一类型

> 原文：[https://www.geeksforgeeks.org/rearrange-string-such-that-no-pair-of-adjacent-characters-are-of-the-same-type/](https://www.geeksforgeeks.org/rearrange-string-such-that-no-pair-of-adjacent-characters-are-of-the-same-type/)

给定字母数字字符串 **str** ，任务是重新排列字符串，以使两个相邻字符都不属于同一类型，即，两个相邻字符不能为字母或数字。 如果没有这种安排，请打印 **-1** 。

**示例**：

> **输入**：str =“ geeks2020”
> **输出**：g2e0e2k0s
> 
> **输入**：str =“ IPL20”
> **输出**：I2P0L

**天真的方法**：最简单的方法是[生成给定字符串](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有可能排列，并针对每个排列检查是否满足给定条件。 如果对任何排列均正确，则打印该排列。 如果不存在这样的排列，则打印***-1*** 。

***时间复杂度**：O（2 <sup>N</sup> ）*

***辅助空间**：O（1）*

**高效方法**：为了优化上述方法，其思想是将所有字母和数字分开存储，并通过将它们交替放置在结果字符串中来重新排列它们。 如果字母和数字的位数相差大于 1，则打印 ***-1*** ，因为可能的排列不可行。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to rearrange given
// alphanumeric string such that
// no two adjacent characters
// are of the same type
string rearrange(string s)
{
    // Stores alphabets and digits
    string s1 = "", s2 = "";

    // Store the alphabets and digits
    // separately in the strings
    for (char x : s) {
        isalpha(x) ? s1.push_back(x)
                   : s2.push_back(x);
    }

    // Stores the count of
    // alphabets and digits
    int n = s1.size();
    int m = s2.size();

    // If respective counts
    // differ by 1
    if (abs(n - m) > 1)

        // Desired arrangement
        // not possible
        return "-1";

    // Stores the indexes
    int i = 0, j = 0, k = 0;

    // Check if first character
    // should be alphabet or digit
    int flag = (n >= m) ? 1 : 0;

    // Place alphabets and digits
    // alternatively
    while (i < n and j < m) {

        // If current character
        // needs to be alphabet
        if (flag)
            s[k++] = s1[i++];

        // If current character
        // needs to be a digit
        else
            s[k++] = s2[j++];

        // Flip flag for alternate
        // arrangement
        flag = !flag;
    }

    // Return resultant string
    return s;
}

// Driver Code
int main()
{
    // Given String
    string str = "geeks2020";

    // Function Call
    cout << rearrange(str) << endl;

    return 0;
}

```

## Java

```java

// Java program to implement
// the above approach
class GFG{

// Function to rearrange given
// alphanumeric String such that
// no two adjacent characters
// are of the same type
static String rearrange(String s)
{
  // Stores alphabets and digits
  String s1 = "", s2 = "", ans = "";
  char []s3 = s.toCharArray();

  // Store the alphabets and digits
  // separately in the Strings
  for (char x : s3) 
  {
    if(x >= 'a' && x <= 'z')
      s1 += x ;
    else
      s2 += x;
  }

  // Stores the count of
  // alphabets and digits
  int n = s1.length();
  int m = s2.length();

  // If respective counts
  // differ by 1
  if (Math.abs(n - m) > 1)

    // Desired arrangement
    // not possible
    return "-1";

  // Stores the indexes
  int i = 0, j = 0, k = 0;

  // Check if first character
  // should be alphabet or digit
  int flag = (n >= m) ? 1 : 0;

  // Place alphabets and digits
  // alternatively
  while (i < n && j < m) 
  {
    // If current character
    // needs to be alphabet
    if (flag != 0)
      ans += s1.charAt(i++); 

    // If current character
    // needs to be a digit
    else
      ans += s2.charAt(j++);

    // Flip flag for alternate
    // arrangement
    if(flag == 1)
      flag = 0;
    else
      flag = 1;
  }

  // Return resultant String
  return ans;
}

// Driver Code
public static void main(String[] args)
{
  // Given String
  String str = "geeks2020";

  // Function Call
  System.out.print(rearrange(str) + "\n");
}
}

// This code is contributed by gauravrajput1

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to rearrange given
# alphanumeric such that no 
# two adjacent characters
# are of the same type
def rearrange(s):

    # Stores alphabets and digits
    s1 = []
    s2 = []

    # Store the alphabets and digits
    # separately in the strings
    for x in s:
        if x.isalpha():
            s1.append(x)
        else:
            s2.append(x)

    # Stores the count of
    # alphabets and digits
    n = len(s1)
    m = len(s2)

    # If respective counts
    # differ by 1
    if (abs(n - m) > 1):

        # Desired arrangement
        # not possible
        return "-1"

    # Stores the indexes
    i = 0
    j = 0
    k = 0

    # Check if first character
    # should be alphabet or digit
    flag = 0
    if (n >= m):
        flag = 1
    else:
        flag = 0

    # Place alphabets and digits
    # alternatively
    while (i < n and j < m):

        # If current character
        # needs to be alphabet
        if (flag):
            s[k] = s1[i]
            k += 1
            i += 1

        # If current character
        # needs to be a digit
        else:
            s[k] = s2[j]
            k += 1
            j += 1

        # Flip flag for alternate
        # arrangement
        flag = not flag

    # Return resultant string
    return "".join(s)

# Driver Code
if __name__ == '__main__':

    # Given String
    str = "geeks2020"

    str1 = [i for i in str]

    # Function call
    print(rearrange(str1))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program to implement
// the above approach
using System;
class GFG{

// Function to rearrange given
// alphanumeric String such that
// no two adjacent characters
// are of the same type
static String rearrange(String s)
{
  // Stores alphabets and digits
  String s1 = "", s2 = "", ans = "";
  char []s3 = s.ToCharArray();

  // Store the alphabets and digits
  // separately in the Strings
  foreach (char x in s3) 
  {
    if(x >= 'a' && x <= 'z')
      s1 += x ;
    else
      s2 += x;
  }

  // Stores the count of
  // alphabets and digits
  int n = s1.Length;
  int m = s2.Length;

  // If respective counts
  // differ by 1
  if (Math.Abs(n - m) > 1)

    // Desired arrangement
    // not possible
    return "-1";

  // Stores the indexes
  int i = 0, j = 0, k = 0;

  // Check if first character
  // should be alphabet or digit
  int flag = (n >= m) ? 1 : 0;

  // Place alphabets and digits
  // alternatively
  while (i < n && j < m) 
  {
    // If current character
    // needs to be alphabet
    if (flag != 0)
      ans += s1[i++]; 

    // If current character
    // needs to be a digit
    else
      ans += s2[j++];

    // Flip flag for alternate
    // arrangement
    if(flag == 1)
      flag = 0;
    else
      flag = 1;
  }

  // Return resultant String
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  // Given String
  String str = "geeks2020";

  // Function Call
  Console.Write(rearrange(str) + "\n");
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
g2e0e2k00

```

***时间复杂度**：`O(n)`*

***辅助空间**：`O(n)`*



* * *

* * *



