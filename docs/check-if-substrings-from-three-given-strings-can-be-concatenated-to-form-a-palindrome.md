# 检查三个给定字符串的子串是否可以连接起来形成回文

> 原文:[https://www . geeksforgeeks . org/check-if-substrings-from-this-给定-string-can-concated-form-a-回文/](https://www.geeksforgeeks.org/check-if-substrings-from-three-given-strings-can-be-concatenated-to-form-a-palindrome/)

https://write.geeksforgeeks.org/internshipGiven 三个[字符串](https://www.geeksforgeeks.org/string-data-structure/)**S1****S2**和 **S3** 的长度分别为**L****M**和 **N** ，任务是检查是否有可能从 **S1、S2** 和 **S3** 中选择一些非空的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)，使得它们的[串联](https://www.geeksforgeeks.org/python-string-concatenation/)如果发现是真的，打印**“是”**。否则，打印**“否”。**

**示例:**

> **输入:**S1 =“adcb”，S2 =“bcdb”，S3 =“ace”
> **输出:** YES
> **解释:**
> 可能的方法之一如下:
> 从字符串 S1 中选择子字符串“ad”，从字符串 S2 中选择“d”，从字符串 S3 中选择“a”。因此，结果字符串是 S =“adda”，这是一个回文。因此，输出应该是“是”。
> 
> **输入:**S1 =“a”，S2 =“BC”，S3 =“c”
> T3】输出:否

**方法:**想法是观察如果 **S1** 和 **S3** 至少有一个共同的字符，总有可能找到这样的 **a** 、 **b** 和 **c** 使得 **a+b+c** 成为回文。按照以下步骤解决问题:

1.  初始化两个变量，比如 **maskA** 和 **maskC** ，分别用于屏蔽字符串 **S1** 和 **S3** 中的字符。
2.  [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**【S1】**的字符，并在 **maskA** 中设置**(I-a)**位，表示字符串 **S1** 中存在相应的字符。
3.  [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**【S3】**的字符，并在 **maskC** 中设置 **(i-'a') <sup>第</sup>** 位，表示相应的字符出现在字符串 **S3** 中。
4.  如果 **maskA** 和 **maskC** 的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)大于零，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if substrings from
// three given strings can be concatenated
// to form a palindrome
string make_palindrome(
    string S1, string S2, string S3)
{
    // Mask for S1 and S2
    int maskA = 0, maskC = 0;

    // Set (i-'a')th bit in maskA
    for (char i : S1)
        maskA |= (1 << (i - 'a'));

    // Set (i-'a')th bit in maskC
    for (char i : S3)
        maskC |= (1 << (i - 'a'));

    // If the bitwise AND is > 0
    if ((maskA & maskC) > 0)
        return "YES";

    return "NO";
}

// Driver Code
int main()
{
    string S1 = "adcb", S2 = "bcdb", S3 = "abe";
    cout << make_palindrome(S1, S2, S3);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to check if subStrings from
// three given Strings can be concatenated
// to form a palindrome
static String make_palindrome(
    String S1, String S2, String S3)
{

    // Mask for S1 and S2
    int maskA = 0, maskC = 0;

    // Set (i-'a')th bit in maskA
    for (char i : S1.toCharArray())
        maskA |= (1 << (i - 'a'));

    // Set (i-'a')th bit in maskC
    for (char i : S3.toCharArray())
        maskC |= (1 << (i - 'a'));

    // If the bitwise AND is > 0
    if ((maskA & maskC) > 0)
        return "YES";
    return "NO";
}

// Driver Code
public static void main(String[] args)
{
    String S1 = "adcb", S2 = "bcdb", S3 = "abe";
    System.out.print(make_palindrome(S1, S2, S3));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if substrings from
# three given strings can be concatenated
# to form a palindrome
def make_palindrome(S1, S2, S3):

    # Mask for S1 and S2
    maskA, maskC = 0, 0

    # Set (i-'a')th bit in maskA
    for i in S1:
        maskA |= (1 << (ord(i) - ord('a')))

    # Set (i-'a')th bit in maskC
    for i in S3:
        maskC |= (1 << (ord(i) - ord('a')))

    # If the bitwise AND is > 0
    if ((maskA & maskC) > 0):
        return "YES"

    return "NO"

# Driver Code
if __name__ == '__main__':
    S1,S2,S3 = "adcb", "bcdb", "abe"
    print (make_palindrome(S1, S2, S3))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to check if subStrings from
// three given Strings can be concatenated
// to form a palindrome
static String make_palindrome(
    String S1, String S2, String S3)
{

    // Mask for S1 and S2
    int maskA = 0, maskC = 0;

    // Set (i-'a')th bit in maskA
    foreach (char i in S1.ToCharArray())
        maskA |= (1 << (i - 'a'));

    // Set (i-'a')th bit in maskC
    foreach (char i in S3.ToCharArray())
        maskC |= (1 << (i - 'a'));

    // If the bitwise AND is > 0
    if ((maskA & maskC) > 0)
        return "YES";
    return "NO";
}

// Driver Code
public static void Main(String[] args)
{
    String S1 = "adcb", S2 = "bcdb", S3 = "abe";
    Console.Write(make_palindrome(S1, S2, S3));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if subStrings from
// three given Strings can be concatenated
// to form a palindrome
function make_palindrome(S1,S2,S3)
{
    // Mask for S1 and S2
    let maskA = 0, maskC = 0;

    // Set (i-'a')th bit in maskA
    for (let i=0;i< S1.length;i++)
        maskA |= (1 << (S1[i].charCodeAt(0) - 'a'.charCodeAt(0)));

    // Set (i-'a')th bit in maskC
    for (let i=0;i< S3.length;i++)
        maskC |= (1 << (S3[i].charCodeAt(0) - 'a'.charCodeAt(0)));

    // If the bitwise AND is > 0
    if ((maskA & maskC) > 0)
        return "YES";
    return "NO";
}

// Driver Code
let S1 = "adcb", S2 = "bcdb", S3 = "abe";
document.write(make_palindrome(S1, S2, S3));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(L + N)*
***辅助空间:** O(L + M + N)*