# 检查一个字符串是否可以拆分成两个子字符串，使得一个子字符串是另一个子字符串的子字符串

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-split-in-two-substring-so-one-substring-of-other/](https://www.geeksforgeeks.org/check-if-a-string-can-be-split-into-two-substrings-such-that-one-substring-is-a-substring-of-the-other/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是检查一个字符串是否可以分成两个子字符串，比如说 **A** 和 **B** ，这样 **B** 就是 **A** 的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)。如果不可能，打印**否**。否则，打印**是**。

**示例:**

> **输入:**S =“abcdab”
> T3】输出:是
> **说明:**考虑到两个拆分为 A =“ABCD”和 B =“ab”，B 是 A 的子串
> 
> **输入:**S = " ABCD "
> T3】输出:否

**天真方法:**解决问题最简单的方法是在每个可能的索引处拆分字符串 **S** ，然后[检查右边的子串是否是左边子串](https://www.geeksforgeeks.org/check-string-substring-another/)的子串。如果任何分割满足条件，打印**“是**”。否则，打印**“否**”。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，思路是检查字符串 **S** 的最后一个[字符是否存在于剩余字符串中。按照以下步骤解决问题:](https://www.geeksforgeeks.org/how-to-find-the-first-and-last-character-of-a-string-in-java/)

*   将 **S** 的最后一个字符存储在 **c** 中。
*   [检查子串](https://www.geeksforgeeks.org/string-find-in-cpp/)**S【0，N-2】**中是否存在 **c** 。
*   如果发现是真的，打印**“是”**。否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a string can be
// divided into two substrings such that
// one substring is substring of the other
void splitString(string S, int N)
{
    // Store the last character of S
    char c = S[N - 1];

    int f = 0;

    // Traverse the characters at indices [0, N-2]
    for (int i = 0; i < N - 1; i++) {

        // Check if the current character is
        // equal to the last character
        if (S[i] == c) {

            // If true, set f = 1
            f = 1;

            // Break out of the loop
            break;
        }
    }

    if (f)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    // Given string, S
    string S = "abcdab";

    // Store the size of S
    int N = S.size();

    // Function Call
    splitString(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to check if a String can be
// divided into two subStrings such that
// one subString is subString of the other
static void splitString(String S, int N)
{

    // Store the last character of S
    char c = S.charAt(N - 1);
    int f = 0;

    // Traverse the characters at indices [0, N-2]
    for (int i = 0; i < N - 1; i++)
    {

        // Check if the current character is
        // equal to the last character
        if (S.charAt(i) == c)
        {

            // If true, set f = 1
            f = 1;

            // Break out of the loop
            break;
        }
    }

    if (f > 0)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver Code
public static void main(String[] args)
{

    // Given String, S
    String S = "abcdab";

    // Store the size of S
    int N = S.length();

    // Function Call
    splitString(S, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a can be
# divided into two substrings such that
# one subis subof the other
def splitString(S, N):

    # Store the last character of S
    c = S[N - 1]

    f = 0

    # Traverse the characters at indices [0, N-2]
    for i in range(N - 1):

        # Check if the current character is
        # equal to the last character
        if (S[i] == c):

            # If true, set f = 1
            f = 1

            # Break out of the loop
            break

    if (f):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    # Given string, S
    S = "abcdab"

    # Store the size of S
    N = len(S)

    # Function Call
    splitString(S, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG{

// Function to check if a string can be
// divided into two substrings such that
// one substring is substring of the other
static void splitString(string S, int N)
{
    // Store the last character of S
    char c = S[N - 1];
    int f = 0;

    // Traverse the characters at indices [0, N-2]
    for (int i = 0; i < N - 1; i++)
    {

        // Check if the current character is
        // equal to the last character
        if (S[i] == c)
        {

            // If true, set f = 1
            f = 1;

            // Break out of the loop
            break;
        }
    }

    if (f != 0)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main()
{
    // Given string, S
    string S = "abcdab";

    // Store the size of S
    int N = S.Length;

    // Function Call
    splitString(S, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach
// Function to check if a String can be
// divided into two subStrings such that
// one subString is subString of the other
function splitString(S , N)
{

    // Store the last character of S
    var c = S.charAt(N - 1);
    var f = 0;

    // Traverse the characters at indices [0, N-2]
    for (var i = 0; i < N - 1; i++)
    {

        // Check if the current character is
        // equal to the last character
        if (S.charAt(i) == c)
        {

            // If true, set f = 1
            f = 1;

            // Break out of the loop
            break;
        }
    }

    if (f > 0)
        document.write("Yes");
    else
        document.write("No");
}

// Driver Code

//Given String, S
var S = "abcdab";

// Store the size of S
var N = S.length;

// Function Call
splitString(S, N);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)