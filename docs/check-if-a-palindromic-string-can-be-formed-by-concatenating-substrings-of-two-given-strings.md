# 检查是否可以通过连接两个给定字符串的子字符串来形成回文字符串

> 原文:[https://www . geeksforgeeks . org/check-if-a-回文字符串可以通过串联两个给定字符串的子字符串来形成/](https://www.geeksforgeeks.org/check-if-a-palindromic-string-can-be-formed-by-concatenating-substrings-of-two-given-strings/)

给定两个字符串 **str1** 和 **str2** ，任务是检查是否有可能通过将 **str1** 和 **str2** 的两个子字符串串联起来形成[回文字符串](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。

**示例:**

> **输入:**str1 =“ABCD”，str2 =“acba”
> **输出:**是
> **解释:**
> 有五种可能的情况，来自 str 1 和 str 2 的两个子串的串联给出回文串:
> “ab”+“a”=“ABA”
> “ab”+“ba”=“ABBA”
> “BC”+“CB”=“bccb”
> “BC”+“b”=“BCB”【t1b】
> 
> **输入:**str 1 =“pqrs”，str 2 =“ABCD”
> **输出:**否
> **解释:**
> 给定字符串的子字符串不可能串联在一起，从而产生回文字符串。

**天真方法:**
解决问题最简单的方法是[生成 **str1** 和 **str2** 的每一个可能的子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，并将它们组合起来生成所有可能的串联。对于每个连接，检查它是否是回文。如发现属实，打印**“是”**。否则，打印**“否”**。
***时间复杂度:**O(N<sup>2</sup>* M<sup>2</sup>*(N+M))，其中 N 和 M 分别为 str1 和 str2 的长度。*
***辅助空间:** O(1)*

**高效方法:**
要优化上述方法，需要进行以下观察:

> 如果给定的字符串拥有至少一个公共字符，那么它们将总是在两个字符串的公共字符的连接上形成一个回文字符串。
> **图解:**
> str 1 =**a**BC，str 2 =【f**a**d】
> 由于**a’**在两个字符串中都很常见，因此可以得到回文字符串“ **aa** ”。

按照以下步骤解决问题:

*   初始化一个布尔数组来标记两个字符串中每个字母的存在。
*   遍历 **str1** 并将索引**(str 1[I]–‘a’)**标记为真。
*   现在，遍历 **str2** 并检查是否有任何索引**(str 2[I]–‘a’)**已经标记为**真**，打印**“是”**。
*   完成遍历 **str2** 后，如果没有找到常用字符，则打印**“否”。**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a palindromic
// string can be formed from the
// substring of given strings
bool check(string str1, string str2)
{
    // Boolean array to mark
    // presence of characters
    vector<bool> mark(26, false);

    int n = str1.size(),
        m = str2.size();

    for (int i = 0; i < n; i++) {

        mark[str1[i] - 'a'] = true;
    }

    // Check if any of the character
    // of str2 is already marked
    for (int i = 0; i < m; i++) {

        // If a common character
        // is found
        if (mark[str2[i] - 'a'])
            return true;
    }

    // If no common character
    // is found
    return false;
}

// Driver Code
int main()
{

    string str1 = "abca",
        str2 = "efad";

    if (check(str1, str2))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.Arrays;

class GFG{

// Function to check if a palindromic
// string can be formed from the
// substring of given strings
public static boolean check(String str1,
                            String str2)
{

    // Boolean array to mark
    // presence of characters
    boolean[] mark = new boolean[26];
    Arrays.fill(mark, false);

    int n = str1.length(),
        m = str2.length();

    for(int i = 0; i < n; i++)
    {
        mark[str1.charAt(i) - 'a'] = true;
    }

    // Check if any of the character
    // of str2 is already marked
    for(int i = 0; i < m; i++)
    {

        // If a common character
        // is found
        if (mark[str2.charAt(i) - 'a'])
            return true;
    }

    // If no common character
    // is found
    return false;
}

// Driver code
public static void main(String[] args)
{
    String str1 = "abca",
    str2 = "efad";

    if (check(str1, str2))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a palindromic
# string can be formed from the
# substring of given strings
def check(str1, str2):

    # Boolean array to mark
    # presence of characters
    mark = [False for i in range(26)]

    n = len(str1)
    m = len(str2)

    for i in range(n):
        mark[ord(str1[i]) - ord('a')] = True

    # Check if any of the character
    # of str2 is already marked
    for i in range(m):

        # If a common character
        # is found
        if (mark[ord(str2[i]) - ord('a')]):
            return True;

    # If no common character
    # is found
    return False

# Driver code
if __name__=="__main__":

    str1 = "abca"
    str2 = "efad"

    if (check(str1, str2)):
        print("Yes");
    else:
        print("No");

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if a palindromic
// string can be formed from the
// substring of given strings
public static bool check(String str1,
                        String str2)
{

    // Boolean array to mark
    // presence of characters
    bool[] mark = new bool[26];

    int n = str1.Length,
        m = str2.Length;

    for(int i = 0; i < n; i++)
    {
        mark[str1[i] - 'a'] = true;
    }

    // Check if any of the character
    // of str2 is already marked
    for(int i = 0; i < m; i++)
    {

        // If a common character
        // is found
        if (mark[str2[i] - 'a'])
            return true;
    }

    // If no common character
    // is found
    return false;
}

// Driver code
public static void Main(String[] args)
{
    String str1 = "abca",
    str2 = "efad";

    if (check(str1, str2))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to check if a palindromic
// string can be formed from the
// substring of given strings
function check(str1, str2)
{
    // Boolean array to mark
    // presence of characters
    var mark = Array(26).fill(false);

    var n = str1.length,
        m = str2.length;

    for (var i = 0; i < n; i++) {

        mark[str1[i] - 'a'] = true;
    }

    // Check if any of the character
    // of str2 is already marked
    for (var i = 0; i < m; i++) {

        // If a common character
        // is found
        if (mark[str2[i] - 'a'])
            return true;
    }

    // If no common character
    // is found
    return false;
}

// Driver Code
var str1 = "abca",
    str2 = "efad";
if (check(str1, str2))
    document.write( "Yes");
else
    document.write( "No");

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(max(N，M))，其中 N 和 M 分别是 str1 和 str2 的长度。*
***辅助空间:** O(1)*