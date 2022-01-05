# 也是给定字符串后缀的所有前缀的长度

> 原文:[https://www . geeksforgeeks . org/所有前缀长度也是给定字符串的后缀/](https://www.geeksforgeeks.org/length-of-all-prefixes-that-are-also-suffixes-of-given-string/)

给定一个由 **N** 字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找出给定字符串 **S** 的所有[前缀的长度，这些前缀也是同一字符串](https://www.geeksforgeeks.org/count-of-strings-whose-prefix-match-with-the-given-string-to-a-given-length-k/) **S** 的[后缀。](https://www.geeksforgeeks.org/check-if-a-string-is-suffix-of-another/)

**示例:**

> **输入:**S = " ababababab "
> T3】输出:2 4 6 8
> T6】说明:T8】S 的前缀也是它的后缀是:
> 
> 1.  长度为 2 的“ab”
> 2.  长度为 4 的“abab”
> 3.  长度为 6 的“ababab”
> 4.  长度= 8 的“abababab”
> 
> **输入:** S =【极客暴走族】
> T3】输出: 5

**天真法:**解决给定问题最简单的方法是[从开始遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)、 **S** ，在每次迭代中，将当前字符添加到前缀字符串中，[检查前缀字符串是否与相同长度的后缀相同](https://www.geeksforgeeks.org/longest-prefix-also-suffix/)。如果发现**为真**，则打印前缀字符串的长度。否则，检查下一个前缀。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to  find the length of all
// prefixes of the given string that
// are also suffixes of the same string
void countSamePrefixSuffix(string s, int n)
{
    // Stores the prefix string
    string prefix = "";

    // Traverse the string S
    for (int i = 0; i < n - 1; i++) {

        // Add the current character
        // to the prefix string
        prefix += s[i];

        // Store the suffix string
        string suffix = s.substr(
            n - 1 - i, n - 1);

        // Check if both the strings
        // are equal or not
        if (prefix == suffix) {
           cout << prefix.size() << " ";
        }
    }
}

// Driver Code
int main()
{
    string S = "ababababab";
    int N = S.size();
    countSamePrefixSuffix(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to  find the length of all
// prefixes of the given string that
// are also suffixes of the same string
static void countSamePrefixSuffix(String s, int n)
{

    // Stores the prefix string
    String prefix = "";

    // Traverse the string S
    for(int i = 0; i < n - 1; i++)
    {

        // Add the current character
        // to the prefix string
        prefix += s.charAt(i);

        // Store the suffix string
        String suffix = s.substring(n - 1 - i, n);

        // Check if both the strings
        // are equal or not
        if (prefix.equals(suffix))
        {
            System.out.print(prefix.length() + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    String S = "ababababab";
    int N = S.length();

    countSamePrefixSuffix(S, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to  find the length of all
# prefixes of the given that
# are also suffixes of the same string
def countSamePrefixSuffix(s, n):

    # Stores the prefix string
    prefix = ""

    # Traverse the S
    for i in range(n - 1):

        # Add the current character
        # to the prefix string
        prefix += s[i]

        # Store the suffix string
        suffix = s[n - 1 - i: 2 * n - 2 - i]

        # Check if both the strings
        # are equal or not
        if (prefix == suffix):
            print(len(prefix), end = " ")

# Driver Code
if __name__ == '__main__':

    S = "ababababab"
    N = len(S)

    countSamePrefixSuffix(S, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

 // Function to  find the length of all
// prefixes of the given string that
// are also suffixes of the same string
static void countSamePrefixSuffix(string s, int n)
{
    // Stores the prefix string
    string prefix = "";

    // Traverse the string S
    for (int i = 0; i < n - 1; i++) {

        // Add the current character
        // to the prefix string
        prefix += s[i];

        // Store the suffix string
        string suffix = s.Substring(n - 1 - i, i+1);

        // Check if both the strings
        // are equal or not
        if (prefix == suffix) {
           Console.Write(prefix.Length + " ");
        }
    }
}

// Driver Code
public static void Main()
{
    string S = "ababababab";
    int N = S.Length;
    countSamePrefixSuffix(S, N);   
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the length of all
// prefixes of the given string that
// are also suffixes of the same string
function countSamePrefixSuffix( s,  n)
{

    // Stores the prefix string
    var prefix = "";

    // Traverse the string S
    for(let i = 0; i < n - 1; i++)
    {

        // Add the current character
        // to the prefix string
        prefix += s.charAt(i);

        // Store the suffix string
        var suffix = s.substring(n - 1 - i, n);

        // Check if both the strings
        // are equal or not
        if (prefix==suffix)
        {
            document.write(prefix.length + " ");
        }
    }
}

// Driver Code

let S = "ababababab";
let N = S.length;

countSamePrefixSuffix(S, N);

</script>
```

**Output:** 

```
2 4 6 8
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)

**高效方法:**上述方法也可以通过使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)来存储给定字符串的前缀来进行优化。然后，遍历所有后缀并检查它们是否存在于哈希映射中。按照以下步骤解决问题:

*   初始化两个[德清](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)，说**前缀**和**后缀**来存储 **S** 的前缀串和后缀串。
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-pairs-in-c/) ，比如说 **M** 来存储 **S** 的所有前缀。
*   [使用变量 **i** 在范围**【0，N–2】**内遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) S
    *   在**前缀**和**后缀**的后面推当前字符。
    *   在散列表 **M** 中将前缀标记为 **true** 。
*   循环结束后，添加字符串的最后一个字符，在**后缀**上加上**S[N–1]**。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–2】**并执行以下步骤:
    *   删除**后缀**的前字符。
    *   现在，检查哈希表 **M** 中是否存在当前的数据。如果发现是**真**的话，那就打印[的德格](https://www.geeksforgeeks.org/dequeempty-dequesize-c-stl/)的尺寸。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to  find the length of all
// prefixes of the  given string that
// are also suffixes of the same string
void countSamePrefixSuffix(string s, int n)
{
    // Stores the prefixes of the string
    map<deque<char>, int> cnt;

    // Stores the prefix & suffix strings
    deque<char> prefix, suffix;

    // Iterate in the range [0, n - 2]
    for (int i = 0; i < n - 1; i++) {

        // Add the current character to
        // the prefix and suffix strings
        prefix.push_back(s[i]);
        suffix.push_back(s[i]);

        // Mark the prefix as 1 in
        // the HashMap
        cnt[prefix] = 1;
    }

    // Add the last character to
    // the suffix
    suffix.push_back(s[n - 1]);
    int index = n - 1;

    // Iterate in the range [0, n - 2]
    for (int i = 0; i < n - 1; i++) {

        // Remove the character from
        // the front of suffix deque
        // to get the suffix string
        suffix.pop_front();

        // Check if the suffix is
        // present in HashMap or not
        if (cnt[suffix] == 1) {
            cout << index << " ";
        }

        index--;
    }
}

// Driver Code
int main()
{
    string S = "ababababab";
    int N = S.size();
    countSamePrefixSuffix(S, N);

    return 0;
}
```

**Output:** 

```
8 6 4 2
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(N)