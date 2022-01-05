# 检查给定的字符串是否为反向双音素字符串

> 原文:[https://www . geeksforgeeks . org/check-if-a-给定字符串是-reverse-bitonic-string-or-not/](https://www.geeksforgeeks.org/check-if-a-given-string-is-a-reverse-bitonic-string-or-not/)

给定一个字符串**字符串**，任务是检查该字符串是否是[反向双音素](https://www.geeksforgeeks.org/bitonic-sort/)字符串。如果字符串**字符串**是反向双音素字符串，则打印**“是”**。否则，打印**“否”**。

> 一个**反向双音素字符串**是一个字符串，其中字符按降序排列，然后按 ASCII 值的升序排列。

**示例:**

> **输入:** str = "zyxbcd"
> **输出:** YES
> **解释:**
> 在上面的字符串中，ASCII 值先减少{z，y，x}，然后增加{b，c，d}。
> 
> **输入:**输出:否

**方法:**
要解决这个问题，遍历字符串并检查字符串字符的 ASCII 值是否遵循以下任何模式:

*   严格增加。
*   严格递减。
*   严格减少，然后严格增加。

按照以下步骤解决问题:

1.  遍历字符串，检查每个字符的下一个字符的 ASCII 值是否小于当前字符的 ASCII 值。
2.  如果在任何时候，下一个字符的 ASCII 值大于当前字符的 ASCII 值，则中断循环。
3.  现在从索引开始遍历，对于每个字符，检查下一个字符 ASCII 值是否大于当前字符的 ASCII 值。
4.  如果在到达数组末尾之前，下一个字符的 ASCII 值小于当前字符的 ASCII 值，则打印**“否”**并中断循环。
5.  如果整个字符串遍历成功，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given
// string is reverse bitonic
int checkReverseBitonic(string s)
{
    int i, j;

    // Check for decreasing sequence
    for (i = 1; i < s.size(); i++) {
        if (s[i] < s[i - 1])
            continue;

        if (s[i] >= s[i - 1])
            break;
    }

    // If end of string has
    // been reached
    if (i == s.size() - 1)
        return 1;

    // Check for increasing sequence
    for (j = i + 1; j < s.size();
         j++) {
        if (s[j] > s[j - 1])
            continue;

        if (s[j] <= s[j - 1])
            break;
    }

    i = j;

    // If the end of string
    // hasn't been reached
    if (i != s.size())
        return 0;

    // If the string is
    // reverse bitonic
    return 1;
}

// Driver Code
int main()
{
    string s = "abcdwef";

    (checkReverseBitonic(s) == 1)
        ? cout << "YES"
        : cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to check if the given
// string is reverse bitonic
static int checkReverseBitonic(String s)
{
    int i, j;

    // Check for decreasing sequence
    for(i = 1; i < s.length(); i++)
    {
       if (s.charAt(i) < s.charAt(i - 1))
           continue;

       if (s.charAt(i) >= s.charAt(i - 1))
           break;
    }

    // If end of string has
    // been reached
    if (i == s.length() - 1)
        return 1;

    // Check for increasing sequence
    for(j = i + 1; j < s.length(); j++)
    {
       if (s.charAt(j) > s.charAt(j - 1))
           continue;
       if (s.charAt(j) <= s.charAt(j - 1))
           break;
    }
    i = j;

    // If the end of string
    // hasn't been reached
    if (i != s.length())
        return 0;

    // If the string is
    // reverse bitonic
    return 1;
}

// Driver Code
public static void main(String []args)
{
    String s = "abcdwef";

    if(checkReverseBitonic(s) == 1)
        System.out.println("YES");
    else
        System.out.println("NO");
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if the given
# string is reverse bitonic
def checkReverseBitonic(s):

    i = 0
    j = 0

    # Check for decreasing sequence
    for  i in range(len(s)):
        if (s[i] < s[i - 1]) :
            continue;

        if (s[i] >= s[i - 1]) :
            break;

    # If end of string has been reached
    if (i == len(s)-1) :
        return 1;

    # Check for increasing sequence
    for j in range(i + 1, len(s)):
        if (s[j] > s[j - 1]) :
            continue;

        if (s[j] <= s[j - 1]) :
            break;

    i = j;

    # If the end of string hasn't
    # been reached
    if (i != len(s)) :
        return 0;

    # If reverse bitonic
    return 1;

# Given string
s = "abcdwef"
# Function Call
if(checkReverseBitonic(s) == 1) :
    print("YES")
else:
    print("NO")
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if the given
// string is reverse bitonic
static int checkReverseBitonic(String s)
{
    int i, j;

    // Check for decreasing sequence
    for(i = 1; i < s.Length; i++)
    {
        if (s[i] < s[i - 1])
            continue;

        if (s[i] >= s[i - 1])
            break;
    }

    // If end of string has
    // been reached
    if (i == s.Length - 1)
        return 1;

    // Check for increasing sequence
    for(j = i + 1; j < s.Length; j++)
    {
        if (s[j] > s[j - 1])
            continue;
        if (s[j] <= s[j - 1])
            break;
    }
    i = j;

    // If the end of string
    // hasn't been reached
    if (i != s.Length)
        return 0;

    // If the string is
    // reverse bitonic
    return 1;
}

// Driver Code
public static void Main(String []args)
{
    String s = "abcdwef";

    if(checkReverseBitonic(s) == 1)
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if the given
// string is reverse bitonic
function checkReverseBitonic(s)
{
    var i, j;

    // Check for decreasing sequence
    for(i = 1; i < s.length; i++)
    {
        if (s[i] < s[i - 1])
            continue;

        if (s[i] >= s[i - 1])
            break;
    }

    // If end of string has
    // been reached
    if (i == s.length - 1)
        return 1;

    // Check for increasing sequence
    for(j = i + 1; j < s.length; j++)
    {
        if (s[j] > s[j - 1])
            continue;

        if (s[j] <= s[j - 1])
            break;
    }

    i = j;

    // If the end of string
    // hasn't been reached
    if (i != s.length)
        return 0;

    // If the string is
    // reverse bitonic
    return 1;
}

// Driver Code
var s = "abcdwef";
(checkReverseBitonic(s) == 1) ?
document.write("YES") :
document.write("NO");

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
NO
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*