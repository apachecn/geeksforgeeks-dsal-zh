# 检查字符串是否遵循 a^nb^n 模式

> 原文:[https://www . geesforgeks . org/check-string-follow-anbn-pattern-not/](https://www.geeksforgeeks.org/check-string-follows-anbn-pattern-not/)

给定字符串 str，返回真字符串遵循模式 a <sup>n</sup> b <sup>n</sup> ，即它有 a 后跟 b，这样 a 和 b 的数量相同。

**示例:**

```
Input : str = "aabb"
Output : Yes

Input : str = "abab"
Output : No

Input : str = "aabbb"
Output : No
```

想法是先数 a。如果 a 的个数不等于字符串长度的一半，则返回 false。否则检查是否所有剩余字符都是 b。

下面是上述想法的实现:

## C++

```
// C++ program to check if a string is of
// the form a^nb^n.
#include <iostream>
using namespace std;

// Returns true str is of the form a^nb^n.
bool isAnBn(string str)
{
    int n = str.length();

    // After this loop 'i' has count of a's
    int i;
    for (i = 0; i < n; i++)
        if (str[i] != 'a')
            break;

    // Since counts of a's and b's should
    // be equal, a should appear exactly
    // n/2 times
    if (i * 2 != n)
        return false;

    // Rest of the characters must be all 'b'
    int j;
    for (j = i; j < n; j++)
        if (str[j] != 'b')
            return false;

    return true;
}

// Driver code
int main()
{
    string str = "abab";

    // Function call
    isAnBn(str) ? cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string is of
// the form a^nb^n.
import java.util.*;
import java.lang.*;
import java.io.*;

class CheckPattern {
    public static boolean isAnBn(String s)
    {
        int l = s.length();

        // Only even length strings will have same number of
        // a's and b's
        if (l % 2 == 1) {
            return false;
        }
        // Set two pointers, one from the left and another
        // from right
        int i = 0;
        int j = l - 1;

        // Compare the characters till the center
        while (i < j) {
            if (s.charAt(i) != 'a' || s.charAt(j) != 'b') {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }

    public static void main(String[] args)
        throws java.lang.Exception
    {
        String s = "abab";

        // Function call
        boolean value = isAnBn(s);
        if (value == true) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }
}

// Code contributed by Shivani Sanjay Shinde.
```

## 蟒蛇 3

```
# Python 3program to check if a
# string is of the form a^nb^n.

# Returns true str is of the
# form a^nb^n.

def isAnBn(str):

    n = len(str)

    # After this loop 'i' has
    # count of a's
    for i in range(n):
        if (str[i] != 'a'):
            break

    # Since counts of a's and b's should
    # be equal, a should appear exactly
    # n/2 times
    if (i * 2 != n):
        return False

    # Rest of the characters must
    # be all 'b'
    for j in range(i, n):
        if (str[j] != 'b'):
            return False

    return True

# Driver code
if __name__ == "__main__":
    str = "abab"
    print("Yes") if isAnBn(str) else print("No")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to check if a string
// is of the form a^ nb ^ n.
using System;

class GFG {

    // Function returns true str is of the form a^nb^n.
    public static bool isAnBn(String s)
    {
        int l = s.Length;

        // Only even length strings will have
        // same number of a's and b's
        if (l % 2 == 1) {
            return false;
        }

        // Set two pointers, one from the
        // left and another from right
        int i = 0;
        int j = l - 1;

        // Compare the characters
        // till the center
        while (i < j) {
            if (s[i] != 'a' || s[j] != 'b') {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }

    // Driver Code
    public static void Main()
    {
        String s = "abab";

        // Function call
        bool value = isAnBn(s);
        if (value == true) {
            Console.Write("Yes");
        }
        else {
            Console.Write("No");
        }
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a string
// is of the form a^nb^n.

// Returns true str is of
// the form a^nb^n.
function isAnBn($str)
{
    $n = strlen($str);

    // After this loop 'i'
    // has count of a's
    $i;
    for($i = 0; $i < $n; $i++)
        if ($str[$i] != 'a')
            break;

    // Since counts of a's and b's should
    // be equal, a should appear exactly
    // n/2 times
    if ($i * 2 != $n)
        return false;

    // Rest of the characters
    // must be all 'b'
    $j;
    for($j = $i; $j < $n; $j++)
        if ($str[$j] != 'b')
            return false;

    return true;
}

    // Driver code
    $str = "abab";
    if(isAnBn($str))
        echo "Yes";
    else   
        echo "No";

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// Javascript program to check if a string is of
// the form a^nb^n.

function isAnBn(s)
{
    let l = s.length;

        // Only even length strings will have same number of
        // a's and b's
        if (l % 2 == 1) {
            return false;
        }
        // Set two pointers, one from the left and another
        // from right
        let i = 0;
        let j = l - 1;

        // Compare the characters till the center
        while (i < j) {
            if (s[i] != 'a' || s[j] != 'b') {
                return false;
            }
            i++;
            j--;
        }
        return true;
}

let s = "abab";

// Function call
let value = isAnBn(s);
if (value == true) {
    document.write("Yes");
}
else {
    document.write("No");
}

// This code is contributed by ab2127
</script>
```

**Output**

```
No
```

**另一种方法:**
想法是从第一个和最后一个检查元素，如果在任何阶段我们的条件不满足，那么返回 false。

下面是上述代码的实现:

## C++

```
// C++ code to check a^nb^n
// pattern
#include <iostream>
using namespace std;

// Returns "Yes" str is of the form a^nb^n.
string isAnBn(string str)
{
    int n = str.length();
    if (n & 1)
        return "No";

    // check first half is 'a' and other half is full of 'b'
    int i;
    for (i = 0; i < n / 2; i++)
        if (str[i] != 'a' || str[n - i - 1] != 'b')
            return "No";
    return "Yes";
}

// Driver code
int main()
{
    string str = "ab";

    // Function call
    cout << isAnBn(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check a^nb^n
// pattern
import java.io.*;
class GFG {

  // Returns "Yes" str is of the form a^nb^n.
  static String isAnBn(String str)
  {
    int n = str.length();
    if ((n & 1) != 0)
      return "No";

    // check first half is 'a' and other half is full of 'b'
    int i;
    for (i = 0; i < n / 2; i++)
      if (str.charAt(i) != 'a' || str.charAt(n - i - 1) != 'b')
        return "No";
    return "Yes";
  }

  // Driver code
  public static void main (String[] args)
  {
    String str = "ab";

    // Function call
    System.out.println(isAnBn(str));
  }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 code to check
# a^nb^n pattern

def isanbn(str):
  n=len(str)

  # if length of str is odd return No
  if n&1:
    return "No"

  # check first half is 'a' and other half is full of 'b'
  for i in range(int(n/2)):
    if str[i]!='a' or str[n-i-1]!='b':
      return "No"
  return "Yes"

# Driver code
input_str = "ab"

# Function call
print(isanbn(input_str))
```

## C#

```
// C# code to check a^nb^n
// pattern
using System;
public class GFG
{

  // Returns "Yes" str is of the form a^nb^n.
  static string isAnBn(string str)
  {
    int n = str.Length;
    if ((n & 1) != 0)
      return "No";

    // check first half is 'a' and other half is full of 'b'
    int i;
    for (i = 0; i < n / 2; i++)
      if (str[i] != 'a' || str[n-i-1] != 'b')
        return "No";
    return "Yes";
  }

  // Driver code
  static public void Main ()
  {
    string str = "ab";

    // Function call
    Console.WriteLine(isAnBn(str));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript code to check a^nb^n
// pattern

// Returns "Yes" str is of the form a^nb^n.
function isAnBn(str)
{
    let n = str.length;
    if ((n & 1) != 0)
      return "No";

    // check first half is 'a' and other half is full of 'b'
    let i;
    for (i = 0; i < n / 2; i++)
      if (str[i] != 'a' || str[n - i - 1] != 'b')
        return "No";
    return "Yes";
}

// Driver code
let str = "ab";

// Function call
document.write(isAnBn(str));

// This code is contributed by unknown2108
</script>
```

**Output**

```
Yes
```

本文由[阿迪蒂亚·库马尔](https://www.linkedin.com/in/aditya-kumar-837315100/)、[拉格哈夫·曼多瓦拉](https://www.linkedin.com/in/raghav-mandowara-b270a7192/)投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。