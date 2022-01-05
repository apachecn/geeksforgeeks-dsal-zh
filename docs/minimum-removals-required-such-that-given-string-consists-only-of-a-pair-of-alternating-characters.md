# 要求的最小删除量，使得给定字符串仅由一对交替字符组成

> 原文:[https://www . geesforgeks . org/minimum-removes-required-so-给定字符串仅由一对交替字符组成/](https://www.geeksforgeeks.org/minimum-removals-required-such-that-given-string-consists-only-of-a-pair-of-alternating-characters/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到所需的最小字符移除量，使得字符串 **S** 仅由两个交替的字符组成。

**示例:**

> **输入:**S =*adebbeaebd“*
> T5】输出: 7
> **解释:**移除所有出现的‘b’和‘e’将字符串修改为“adad”，由交替出现的‘a’和‘d’组成。
> 
> **输入:**S =*abccd“*
> T5】输出: 3
> **解释:**去掉所有出现的‘c’和‘d’将字符串修改为“ab”，由交替出现的‘a’和‘b’组成。

**方法:**通过生成所有可能的**26<sup>2</sup>T5】对英文字母，并在字符串 **S** 中找到交替出现的最大长度的一对，比如 **len** 就可以解决这个问题。然后，通过从 **N** 中减去 **len** 来打印需要删除的字符数。**

按照以下步骤解决给定的问题:

1.  初始化一个变量，比如 **len，**来存储一对字符交替出现的最大长度。
2.  遍历每一对可能的英文字母，并对每一对执行以下操作:
    *   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，找到字符串 **S** 中两个字符交替出现的长度，比如**纽伦**。
    *   检查**透镜**是否小于**纽伦**。如果发现是真的，那么更新 **len = newlen** 。
3.  最后，打印**N–len**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// length of alternating occurrences
// of a pair of characters in a string s
int findLength(string s, char i, char j)
{
    // Stores the next character
    // for alternating sequence
    char required = i;

    // Stores the length of alternating
    // occurrences of a pair of characters
    int length = 0;

    // Traverse the given string
    for (char curr : s) {

        // If current character is same
        // as the required character
        if (curr == required) {

            // Increase length by 1
            length += 1;

            // Reset required character
            if (required == i)
                required = j;
            else
                required = i;
        }
    }

    // Return the length
    return length;
}

// Function to find minimum characters
// required to be deleted from S to
// obtain an alternating sequence
int minimumDeletions(string S)
{

    // Stores maximum length
    // of alternating sequence
    // of two characters
    int len = 0;

    // Stores length of the string
    int n = S.length();

    // Generate every pair
    // of English alphabets
    for (char i = 'a'; i <= 'z'; i++) {
        for (char j = i + 1; j <= 'z'; j++) {

            // Function call to find length
            // of alternating sequence for
            // current pair of characters
            int newLen = findLength(S, i, j);

            // Update len to store the maximum
            // of len and newLen in len
            len = max(len, newLen);
        }
    }

    // Return n - len as the final result
    return n - len;
}

// Driver Code
int main()
{
    // Given Input
    string S = "adebbeeaebd";

    // Function call to find minimum
    // characters required to be removed
    // from S to make it an alternating
    // sequence of a pair of characters
    cout << minimumDeletions(S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the maximum
// length of alternating occurrences
// of a pair of characters in a string s
static int findLength(String s, char i, char j)
{

    // Stores the next character
    // for alternating sequence
    char required = i;

    // Stores the length of alternating
    // occurrences of a pair of characters
    int length = 0;

    // Traverse the given string
    for(int k = 0; k < s.length(); k++)
    {
        char curr = s.charAt(k);

        // If current character is same
        // as the required character
        if (curr == required)
        {

            // Increase length by 1
            length += 1;

            // Reset required character
            if (required == i)
                required = j;
            else
                required = i;
        }
    }

    // Return the length
    return length;
}

// Function to find minimum characters
// required to be deleted from S to
// obtain an alternating sequence
static int minimumDeletions(String S)
{

    // Stores maximum length
    // of alternating sequence
    // of two characters
    int len = 0;

    // Stores length of the string
    int n = S.length();

    // Generate every pair
    // of English alphabets
    for(int i = 0; i < 26; i++)
    {
        for(int j = i + 1; j < 26; j++)
        {

            // Function call to find length
            // of alternating sequence for
            // current pair of characters
            int newLen = findLength(S, (char)(i + 97),
                                       (char)(j + 97));

            // Update len to store the maximum
            // of len and newLen in len
            len = Math.max(len, newLen);
        }
    }

    // Return n - len as the final result
    return n - len;
}

// Driver Code
public static void main (String[] args)
{

    // Given Input
    String S = "adebbeeaebd";

    // Function call to find minimum
    // characters required to be removed
    // from S to make it an alternating
    // sequence of a pair of characters
    System.out.print(minimumDeletions(S));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum
# length of alternating occurrences
# of a pair of characters in a string s
def findLength(s, i, j):

    # Stores the next character
    # for alternating sequence
    required = i

    # Stores the length of alternating
    # occurrences of a pair of characters
    length = 0

    # Traverse the given string
    for curr in s:

        # If current character is same
        # as the required character
        if (curr == required):

            # Increase length by 1
            length += 1

            # Reset required character
            if (required == i):
                required = j
            else:
                required = i

    # Return the length
    return length

# Function to find minimum characters
# required to be deleted from S to
# obtain an alternating sequence
def minimumDeletions(S):

    # Stores maximum length
    # of alternating sequence
    # of two characters
    len1 = 0

    # Stores length of the string
    n = len(S)

    # Generate every pair
    # of English alphabets
    for i in range(0, 26, 1):
        for j in range(i + 1, 26, 1):

            # Function call to find length
            # of alternating sequence for
            # current pair of characters
            newLen = findLength(S, chr(i + 97),
                                   chr(j + 97))

            # Update len to store the maximum
            # of len and newLen in len
            len1 = max(len1, newLen)

    # Return n - len as the final result
    return n - len1

# Driver Code
if __name__ == '__main__':

    # Given Input
    S = "adebbeeaebd"

    # Function call to find minimum
    # characters required to be removed
    # from S to make it an alternating
    # sequence of a pair of characters
    print(minimumDeletions(S))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum
// length of alternating occurrences
// of a pair of characters in a string s
static int findLength(string s, char i, char j)
{

    // Stores the next character
    // for alternating sequence
    char required = i;

    // Stores the length of alternating
    // occurrences of a pair of characters
    int length = 0;

    // Traverse the given string
    for(int k = 0; k < s.Length; k++)
    {
        char curr = s[k];

        // If current character is same
        // as the required character
        if (curr == required)
        {

            // Increase length by 1
            length += 1;

            // Reset required character
            if (required == i)
                required = j;
            else
                required = i;
        }
    }

    // Return the length
    return length;
}

// Function to find minimum characters
// required to be deleted from S to
// obtain an alternating sequence
static int minimumDeletions(string S)
{

    // Stores maximum length
    // of alternating sequence
    // of two characters
    int len = 0;

    // Stores length of the string
    int n = S.Length;

    // Generate every pair
    // of English alphabets
    for(int i = 0; i < 26; i++)
    {
        for(int j = i + 1; j < 26; j++)
        {

            // Function call to find length
            // of alternating sequence for
            // current pair of characters
            int newLen = findLength(S, (char)(i + 97),
                                       (char)(j + 97));

            // Update len to store the maximum
            // of len and newLen in len
            len = Math.Max(len, newLen);
        }
    }

    // Return n - len as the final result
    return n - len;
}

// Driver Code
public static void Main(string[] args)
{

    // Given Input
    string S = "adebbeeaebd";

    // Function call to find minimum
    // characters required to be removed
    // from S to make it an alternating
    // sequence of a pair of characters
    Console.WriteLine(minimumDeletions(S));
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum
// length of alternating occurrences
// of a pair of characters in a string s
function findLength( s,  i,  j)
{

    // Stores the next character
    // for alternating sequence
    var required = i;

    // Stores the length of alternating
    // occurrences of a pair of characters
    let length = 0;

    // Traverse the given string
    for(let k = 0; k < s.length; k++)
    {
        var curr = s.charAt(k);

        // If current character is same
        // as the required character
        if (curr == required)
        {

            // Increase length by 1
            length += 1;

            // Reset required character
            if (required == i)
                required = j;
            else
                required = i;
        }
    }

    // Return the length
    return length;
}

// Function to find minimum characters
// required to be deleted from S to
// obtain an alternating sequence
function minimumDeletions( S)
{

    // Stores maximum length
    // of alternating sequence
    // of two characters
    let len = 0;

    // Stores length of the string
    let n = S.length;

    // Generate every pair
    // of English alphabets
    for(let i = 0; i < 26; i++)
    {
        for(let j = i + 1; j < 26; j++)
        {

            // Function call to find length
            // of alternating sequence for
            // current pair of characters
            let newLen =
            findLength(S, String.fromCharCode(i + 97),
                          String.fromCharCode(j + 97));

            // Update len to store the maximum
            // of len and newLen in len
            len = Math.max(len, newLen);
        }
    }

    // Return n - len as the final result
    return n - len;
}

// Driver Code

// Given Input
let S = "adebbeeaebd";

// Function call to find minimum
// characters required to be removed
// from S to make it an alternating
// sequence of a pair of characters
document.write(minimumDeletions(S));

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)