# 给定字符串中不存在长度超过 1 的回文子串的最小替换数

> 原文:[https://www . geesforgeks . org/minimum-replacements-so-no-回文-长度超过 1 的子串出现在给定的字符串中/](https://www.geeksforgeeks.org/minimum-replacements-such-that-no-palindromic-substring-of-length-exceeding-1-is-present-in-the-given-string/)

给定一个由小写字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是通过最少的字符替换来修改该字符串，使其不包含任何长度超过 **1** 的[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)子字符串。

**示例:**

> **输入:** str = "bbbbbbb"
> **输出:** 4
> 字符串可通过替换 4 个字符修改为“bacbacb”。
> 
> **输入:**输出: 2

**进场:**

解决问题的思路是，如果存在长度大于 3 的回文，那么就存在长度为 2 或 3 的回文。因此，贪婪地删除所有长度为 2 或 3 的回文。按照以下步骤解决问题:

*   初始化一个变量，比如说**改变**，以存储所需的替换次数。
*   [迭代给定字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并执行以下步骤:
    *   如果当前索引处的字符与下一个索引处的字符相同，则递增**将**更改为 **1** 。
    *   否则，检查上一索引处的字符是否与下一索引处的字符相同，即是否存在长度为 **3** 的回文子串。因此，增量**将**更改 1。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the changes required such
// that no palindromic substring of length
// exceeding 1 is present in the string
int maxChange(string str)
{

    // Base Case
    if (str.size() <= 1) {
        return 0;
    }

    // Stores the count
    int minChanges = 0;

    // Iterate over the string
    for (int i = 0; i < str.size() - 1; i++) {

        // Palindromic Substring of Length 2
        if (str[i] == str[i + 1]) {

            // Replace the next character
            str[i + 1] = 'N';

            // Increment changes
            minChanges += 1;
        }
        // Palindromic Substring of Length 3
        else if (i > 0 && str[i - 1] == str[i + 1]) {

            // Replace the next character
            str[i + 1] = 'N';
            // Increment changes
            minChanges += 1;
        }
    }

    return minChanges;
}

// Driver Code
int main()
{
    string str = "bbbbbbb";
    cout << maxChange(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to count the changes required such
// that no palindromic subString of length
// exceeding 1 is present in the String
static int maxChange(char []str)
{

    // Base Case
    if (str.length <= 1)
    {
        return 0;
    }

    // Stores the count
    int minChanges = 0;

    // Iterate over the String
    for (int i = 0; i < str.length - 1; i++)
    {

        // Palindromic SubString of Length 2
        if (str[i] == str[i + 1])
        {

            // Replace the next character
            str[i + 1] = 'N';

            // Increment changes
            minChanges += 1;
        }

        // Palindromic SubString of Length 3
        else if (i > 0 && str[i - 1] == str[i + 1])
        {

            // Replace the next character
            str[i + 1] = 'N';

            // Increment changes
            minChanges += 1;
        }
    }
    return minChanges;
}

// Driver Code
public static void main(String[] args)
{
    String str = "bbbbbbb";
    System.out.print(maxChange(str.toCharArray()));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to count the changes required such
# that no palindromic subof length
# exceeding 1 is present in the string
def maxChange(str):
    str = [i for i in str]
    if (len(str) <= 1):
        return 0

    # Stores the count
    minChanges = 0

    # Iterate over the string
    for i in range(len(str) - 1):

        # Palindromic Subof Length 2
        if (str[i] == str[i + 1]):

            # Replace the next character
            str[i + 1] = 'N'

            # Increment changes
            minChanges += 1

        # Palindromic Subof Length 3
        elif (i > 0 and str[i - 1] == str[i + 1]):

            # Replace the next character
            str[i + 1] = 'N'

            # Increment changes
            minChanges += 1
    return minChanges

# Driver Code
if __name__ == '__main__':
    str = "bbbbbbb"
    print (maxChange(str))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# Program to implement
// the above approach
using System;

public class GFG
{

// Function to count the changes required such
// that no palindromic subString of length
// exceeding 1 is present in the String
static int maxChange(char []str)
{

    // Base Case
    if (str.Length <= 1)
    {
        return 0;
    }

    // Stores the count
    int minChanges = 0;

    // Iterate over the String
    for (int i = 0; i < str.Length - 1; i++)
    {

        // Palindromic SubString of Length 2
        if (str[i] == str[i + 1])
        {

            // Replace the next character
            str[i + 1] = 'N';

            // Increment changes
            minChanges += 1;
        }

        // Palindromic SubString of Length 3
        else if (i > 0 && str[i - 1] == str[i + 1])
        {

            // Replace the next character
            str[i + 1] = 'N';

            // Increment changes
            minChanges += 1;
        }
    }
    return minChanges;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "bbbbbbb";
    Console.Write(maxChange(str.ToCharArray()));
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript Program to implement
      // the above approach
      // Function to count the changes required such
      // that no palindromic subString of length
      // exceeding 1 is present in the String
      function maxChange(str) {
        // Base Case
        if (str.length <= 1) {
          return 0;
        }

        // Stores the count
        var minChanges = 0;

        // Iterate over the String
        for (var i = 0; i < str.length - 1; i++) {
          // Palindromic SubString of Length 2
          if (str[i] === str[i + 1]) {
            // Replace the next character
            str[i + 1] = "N";

            // Increment changes
            minChanges += 1;
          }

          // Palindromic SubString of Length 3
          else if (i > 0 && str[i - 1] === str[i + 1]) {
            // Replace the next character
            str[i + 1] = "N";

            // Increment changes
            minChanges += 1;
          }
        }
        return minChanges;
      }

      // Driver Code
      var str = "bbbbbbb";
      document.write(maxChange(str.split("")));
    </script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)