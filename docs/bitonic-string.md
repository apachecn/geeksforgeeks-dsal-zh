# 双音弦

> 原文:[https://www.geeksforgeeks.org/bitonic-string/](https://www.geeksforgeeks.org/bitonic-string/)

给定一个字符串**字符串**，任务是检查该字符串是否是一个[双音素](https://www.geeksforgeeks.org/bitonic-sort/)字符串。如果字符串**字符串**是双音素字符串，则打印**“是”**否则打印**“否”**。

> 二进制字符串是一种字符串，其中字符按升序排列，然后按 ASCII 值的降序排列。

**例:**

> **输入:**str = " abcdfcba "
> **输出:** YES
> **解释:**
> 在上面的字符串中，ASCII 值先增加{a，b，c，d，f，g}，然后减少{g，c，b，a}。
> **输入:** str = "abcdwef"
> **输出:**否

**方法:**
要解决这个问题，我们只需要遍历字符串并检查字符串字符的 ASCII 值是否遵循以下任何模式:

*   严格增加。
*   严格递减。
*   严格增加后严格减少。

按照以下步骤解决问题:

1.  开始遍历字符串，并继续检查下一个字符的 ASCII 值是否大于当前字符的 ASCII 值。
2.  如果在任何时候，下一个字符的 ASCII 值不大于当前字符的 ASCII 值，则中断循环。
3.  再次从上面的中断索引开始遍历，检查下一个字符的 ASCII 值是否小于当前字符的 ASCII 值。
4.  如果在到达数组末尾之前，下一个字符的 ASCII 值不小于当前字符的 ASCII 值，则打印**“否”**并中断循环。
5.  如果成功到达数组末尾，打印**“是”**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the given
// string is bitonic
int checkBitonic(string s)
{
    int i, j;

    // Check for increasing sequence
    for (i = 1; i < s.size(); i++) {
        if (s[i] > s[i - 1])
            continue;

        if (s[i] <= s[i - 1])
            break;
    }

    // If end of string has been reached
    if (i == s.size() - 1)
        return 1;

    // Check for decreasing sequence
    for (j = i + 1; j < s.size();
         j++) {
        if (s[j] < s[j - 1])
            continue;

        if (s[j] >= s[j - 1])
            break;
    }

    i = j;

    // If the end of string hasn't
    // been reached
    if (i != s.size())
        return 0;

    // Return true if bitonic
    return 1;
}

// Driver Code
int main()
{
    // Given string
    string s = "abcdfgcba";

    // Function Call
    (checkBitonic(s) == 1)
        ? cout << "YES"
        : cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if the given
// String is bitonic
static int checkBitonic(char []s)
{
    int i, j;

    // Check for increasing sequence
    for(i = 1; i < s.length; i++)
    {
        if (s[i] > s[i - 1])
            continue;

        if (s[i] <= s[i - 1])
            break;
    }

    // If end of String has been reached
    if (i == s.length - 1)
        return 1;

    // Check for decreasing sequence
    for(j = i + 1; j < s.length; j++)
    {
        if (s[j] < s[j - 1])
            continue;

        if (s[j] >= s[j - 1])
            break;
    }
    i = j;

    // If the end of String hasn't
    // been reached
    if (i != s.length)
        return 0;

    // Return true if bitonic
    return 1;
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String s = "abcdfgcba";

    // Function Call
    System.out.print((checkBitonic(
        s.toCharArray()) == 1) ? "YES" : "NO");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the given
# string is bitonic
def checkBitonic(s):

    i = 0
    j = 0

    # Check for increasing sequence
    for i in range(1, len(s)):
        if (s[i] > s[i - 1]):
            continue;

        if (s[i] <= s[i - 1]):
            break;

    # If end of string has been reached
    if (i == (len(s) - 1)):
        return True;

    # Check for decreasing sequence
    for j in range(i + 1, len(s)):
        if (s[j] < s[j - 1]):
            continue;

        if (s[j] >= s[j - 1]):
            break;
    i = j;

    # If the end of string hasn't
    # been reached
    if (i != len(s) - 1):
        return False;

    # Return true if bitonic
    return True;

# Driver code

# Given string
s = "abcdfgcba"

# Function Call
if(checkBitonic(s)):
    print("YES")
else:
    print("NO")

# This code is contributed by grand_master
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the given
// String is bitonic
static int checkBitonic(char []s)
{
    int i, j;

    // Check for increasing sequence
    for(i = 1; i < s.Length; i++)
    {
        if (s[i] > s[i - 1])
            continue;

        if (s[i] <= s[i - 1])
            break;
    }

    // If end of String has been reached
    if (i == s.Length - 1)
        return 1;

    // Check for decreasing sequence
    for(j = i + 1; j < s.Length; j++)
    {
        if (s[j] < s[j - 1])
            continue;

        if (s[j] >= s[j - 1])
            break;
    }
    i = j;

    // If the end of String hasn't
    // been reached
    if (i != s.Length)
        return 0;

    // Return true if bitonic
    return 1;
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    String s = "abcdfgcba";

    // Function call
    Console.Write((checkBitonic(
        s.ToCharArray()) == 1) ? "YES" : "NO");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if the given
// string is bitonic
function checkBitonic(s)
{
    var i, j;

    // Check for increasing sequence
    for (i = 1; i < s.length; i++) {
        if (s[i] > s[i - 1])
            continue;

        if (s[i] <= s[i - 1])
            break;
    }

    // If end of string has been reached
    if (i == s.length - 1)
        return 1;

    // Check for decreasing sequence
    for (j = i + 1; j < s.length;
         j++) {
        if (s[j] < s[j - 1])
            continue;

        if (s[j] >= s[j - 1])
            break;
    }

    i = j;

    // If the end of string hasn't
    // been reached
    if (i != s.length)
        return 0;

    // Return true if bitonic
    return 1;
}

// Driver Code

// Given string
var s = "abcdfgcba";

// Function Call
(checkBitonic(s) == 1)
    ? document.write( "YES")
    : document.write( "NO");

// This code is contributed by itsok.
</script>
```

**Output:** 

```
YES
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*