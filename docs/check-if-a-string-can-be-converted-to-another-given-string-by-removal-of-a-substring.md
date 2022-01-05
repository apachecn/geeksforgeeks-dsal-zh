# 检查一个字符串是否可以通过删除一个子字符串

转换成另一个给定的字符串

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-transformed-to-other-给定的字符串通过移除子字符串/](https://www.geeksforgeeks.org/check-if-a-string-can-be-converted-to-another-given-string-by-removal-of-a-substring/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **T** ，任务是通过最多移除字符串 **S** 的一个[子字符串来检查字符串 **S** 是否可以转换为字符串 **T** 。如果发现是真的，则打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/program-print-substrings-given-string/)

**示例:**

> **输入:** S = "abcdef "，T = "abc"
> **输出:** YES
> **解释:**
> 去掉子串{ S[3]，…，S[5] }将 S 修改为“abc”。
> 由于字符串 S 等于 T，所以需要的输出为“是”。
> 
> **输入:**S =“aabbb”，T =“ab”
> **输出:** YES
> **解释:**
> 去掉子串{ S[1]，…，S[4] }将 S 修饰为“ab”。
> 由于字符串 S 等于 T，所以需要的输出为“是”。

**天真方法:**解决这个问题最简单的方法是[生成字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **S** 的所有可能的子串，对于每个子串，检查其移除是否使字符串 **S** 等于字符串 **T** 。如果发现任何字符串为真，则打印**“是”**。否则，打印**“否”**。
***时间复杂度:**O(N<sup>2</sup>* M)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 如果子串 **{ S[0]，…，S[I]}+{ S[N –( M–I)]，…，S[N–1]}**等于 **T** ，只有这样，串 **S** 才能转换为串 **T** 。

按照以下步骤解决问题:

*   迭代范围 **[0，M]** ，检查[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **{ S[0]，…，S[I]}+{ S[N –( M–I)]，…，S[N–1]}**是否等于到 **T** 。如果发现是真的，则打印**“是”**。
*   否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if S can be converted to T
// by removing at most one substring from S
string make_string_S_to_T(string S, string T)
{
    // Check if S can be converted to T by
    // removing at most one substring from S
    bool possible = false;

    // Stores length of string T
    int M = T.length();

    // Stores length of string S
    int N = S.length();

    // Iterate over the range [0, M - 1]
    for (int i = 0; i <= M; i++) {

        // Stores Length of the substring
        // { S[0], ..., S[i] }
        int prefix_length = i;

        // Stores Length of the substring
        // { S[0], ..., S[i] }
        int suffix_length = M - i;

        // Stores prefix substring
        string prefix
            = S.substr(0, prefix_length);

        // Stores suffix substring
        string suffix
            = S.substr(N - suffix_length,
                       suffix_length);

        // Checking if prefix+suffix == T
        if (prefix + suffix == T) {
            possible = true;
            break;
        }
    }

    if (possible)
        return "YES";
    else
        return "NO";
}

// Driver Code
int main()
{
    // Given String S and T
    string S = "ababcdcd";
    string T = "abcd";

    // Function call
    cout << make_string_S_to_T(S, T);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to check if S can be converted to T
// by removing at most one subString from S
static String make_String_S_to_T(String S, String T)
{

    // Check if S can be converted to T by
    // removing at most one subString from S
    boolean possible = false;

    // Stores length of String T
    int M = T.length();

    // Stores length of String S
    int N = S.length();

    // Iterate over the range [0, M - 1]
    for (int i = 0; i <= M; i++)
    {

        // Stores Length of the subString
        // { S[0], ..., S[i] }
        int prefix_length = i;

        // Stores Length of the subString
        // { S[0], ..., S[i] }
        int suffix_length = M - i;

        // Stores prefix subString
        String prefix
            = S.substring(0, prefix_length);

        // Stores suffix subString
        String suffix
            = S.substring(N - suffix_length,
                       N);

        // Checking if prefix+suffix == T
        if ((prefix + suffix).equals(T))
        {
            possible = true;
            break;
        }
    }
    if (possible)
        return "YES";
    else
        return "NO";
}

// Driver Code
public static void main(String[] args)
{

    // Given String S and T
    String S = "ababcdcd";
    String T = "abcd";

    // Function call
    System.out.print(make_String_S_to_T(S, T));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if S can be converted to T
# by removing at most one substring from S
def make_string_S_to_T(S, T):

    # Check if S can be converted to T by
    # removing at most one substring from S
    possible = False

    # Stores length of string T
    M = len(T)

    # Stores length of string S
    N = len(S)

    # Iterate over the range [0, M - 1]
    for i in range(0,M+1):

        # Stores Length of the substring
        #  S[0], ..., S[i]
        prefix_length = i

        # Stores Length of the substring
        #  S[0], ..., S[i]
        suffix_length = M - i

        # Stores prefix substring
        prefix = S[:prefix_length]

        # Stores suffix substring
        suffix = S[N - suffix_length:N]

        # Checking if prefix+suffix == T
        if (prefix + suffix == T):
            possible = True
            break

    if (possible):
        return "YES"
    else:
        return "NO"

# Driver Code

# Given String S and T
S = "ababcdcd"
T = "abcd"

# Function call
print(make_string_S_to_T(S, T))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

// Function to check if S can be converted to T
// by removing at most one subString from S
static String make_String_S_to_T(String S, String T)
{

    // Check if S can be converted to T by
    // removing at most one subString from S
    bool possible = false;

    // Stores length of String T
    int M = T.Length;

    // Stores length of String S
    int N = S.Length;

    // Iterate over the range [0, M - 1]
    for (int i = 0; i <= M; i++)
    {

        // Stores Length of the subString
        // { S[0], ..., S[i] }
        int prefix_length = i;

        // Stores Length of the subString
        // { S[0], ..., S[i] }
        int suffix_length = M - i;

        // Stores prefix subString
        String prefix
            = S.Substring(0, prefix_length);

        // Stores suffix subString
        String suffix
            = S.Substring(N-suffix_length,
                       suffix_length);

        // Checking if prefix+suffix == T
        if ((prefix + suffix).Equals(T))
        {
            possible = true;
            break;
        }
    }
    if (possible)
        return "YES";
    else
        return "NO";
}

// Driver Code
public static void Main(String[] args)
{

    // Given String S and T
    String S = "ababcdcd";
    String T = "abcd";

    // Function call
    Console.Write(make_String_S_to_T(S, T));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to check if S can be converted to T
    // by removing at most one subString from S
     function make_String_S_to_T( S,  T) {

        // Check if S can be converted to T by
        // removing at most one subString from S
        var possible = false;

        // Stores length of String T
        var M = T.length;

        // Stores length of String S
        var N = S.length;

        // Iterate over the range [0, M - 1]
        for (i = 0; i <= M; i++) {

            // Stores Length of the subString
            // { S[0], ..., S[i] }
            var prefix_length = i;

            // Stores Length of the subString
            // { S[0], ..., S[i] }
            var suffix_length = M - i;

            // Stores prefix subString
            var prefix = S.substring(0, prefix_length);

            // Stores suffix subString
            var suffix = S.substring(N - suffix_length, N);

            // Checking if prefix+suffix == T
            if ((prefix + suffix)==(T)) {
                possible = true;
                break;
            }
        }
        if (possible)
            return "YES";
        else
            return "NO";
    }

    // Driver Code

        // Given String S and T
        var S = "ababcdcd";
        var T = "abcd";

        // Function call
        document.write(make_String_S_to_T(S, T));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(M<sup>2</sup>)*
***辅助空间:** O(M)*