# 检查一个字符串是否是另一个给定字符串的串联

> 原文:[https://www . geesforgeks . org/check-if-a-string-is-concation-of-other-given-string/](https://www.geeksforgeeks.org/check-if-a-string-is-concatenation-of-another-given-string/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **str1** 和 **str2** ，任务是检查字符串 **str1** 是否可以通过[重复连接字符串](https://www.geeksforgeeks.org/methods-to-concatenate-string-in-c-c-with-examples/) **str2** 形成。

**示例:**

> **输入:**str 1 =“ABC ABC ABC”，str2 =“ABC”
> **输出:**是
> **解释:**
> 三次串联字符串 str 2 生成字符串(“ABC”+“ABC”+“ABC”=)“ABC ABC ABC”。
> 因此，要求的输出为是。
> 
> **输入:**str 1 =“ABC abcab”，str 2 =“ABC”
> T3】输出:否

**方法:**按照以下步骤解决问题:

*   [穿越琴弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)T2str 1**str 2**。
*   对于 **str1** 和 **str2** 的每个字符，检查 **str1[i] == str2[i % M]** 是否存在。
*   如果发现任何字符为假，打印**“否”**。
*   否则，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a string is
// concatenation of another string
bool checkConcat(string str1,
                 string str2)
{

    // Stores the length of str2
    int N = str1.length();

    // Stores the length of str1
    int M = str2.length();

    // If M is not multiple of N
    if (N % M != 0) {
        return false;
    }

    // Traverse both the strings
    for (int i = 0; i < N; i++) {

        // If str1 is not concatenation
        // of str2
        if (str1[i] != str2[i % M]) {
            return false;
        }
    }
    return true;
}

// Driver Code
int main()
{
    string str1 = "abcabcabc";
    string str2 = "abc";

    if (checkConcat(str1, str2)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if a String is
// concatenation of another String
static boolean checkConcat(String str1,
                           String str2)
{

    // Stores the length of str2
    int N = str1.length();

    // Stores the length of str1
    int M = str2.length();

    // If M is not multiple of N
    if (N % M != 0)
    {
        return false;
    }

    // Traverse both the Strings
    for(int i = 0; i < N; i++)
    {

        // If str1 is not concatenation
        // of str2
        if (str1.charAt(i) !=
            str2.charAt(i % M))
        {
            return false;
        }
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    String str1 = "abcabcabc";
    String str2 = "abc";

    if (checkConcat(str1, str2))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a is
# concatenation of another string
def checkConcat(str1, str2):

    # Stores the length of str2
    N = len(str1)

    # Stores the length of str1
    M = len(str2)

    # If M is not multiple of N
    if (N % M != 0):
        return False

    # Traverse both the strings
    for i in range(N):

        # If str1 is not concatenation
        # of str2
        if (str1[i] != str2[i % M]):
            return False

    return True

# Driver Code
if __name__ == '__main__':

    str1 = "abcabcabc"
    str2 = "abc"

    if (checkConcat(str1, str2)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to check if a String is
// concatenation of another String
static bool checkConcat(String str1,
                        String str2)
{
  // Stores the length
  // of str2
  int N = str1.Length;

  // Stores the length
  // of str1
  int M = str2.Length;

  // If M is not multiple
  // of N
  if (N % M != 0)
  {
    return false;
  }

  // Traverse both the Strings
  for(int i = 0; i < N; i++)
  {
    // If str1 is not
    // concatenation of str2
    if (str1[i] !=
        str2[i % M])
    {
      return false;
    }
  }
  return true;
}

// Driver Code
public static void Main(String[] args)
{
  String str1 = "abcabcabc";
  String str2 = "abc";

  if (checkConcat(str1, str2))
  {
    Console.Write("Yes");
  }
  else
  {
    Console.Write("No");
  }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to check if a String is
// concatenation of another String
function checkConcat(str1, str2)
{

    // Stores the length of str2
    let N = str1.length;

    // Stores the length of str1
    let M = str2.length;

    // If M is not multiple of N
    if (N % M != 0)
    {
        return false;
    }

    // Traverse both the Strings
    for(let i = 0; i < N; i++)
    {

        // If str1 is not concatenation
        // of str2
        if (str1[i] !=
            str2[i % M])
        {
            return false;
        }
    }
    return true;
}

// Driver Code

    let str1 = "abcabcabc";
    let str2 = "abc";

    if (checkConcat(str1, str2))
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }

</script>
```

**Output**

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)