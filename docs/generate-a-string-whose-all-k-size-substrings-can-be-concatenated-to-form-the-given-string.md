# 生成一个字符串，它的所有 K 大小的子字符串可以连接起来形成给定的字符串

> 原文:[https://www . geeksforgeeks . org/generate-a-string-what-all-k-size-substrings-可以串联形成给定的字符串/](https://www.geeksforgeeks.org/generate-a-string-whose-all-k-size-substrings-can-be-concatenated-to-form-the-given-string/)

给定一个大小为 **N** 的字符串 **str** 和一个整数 **K** ，任务是生成一个字符串，其大小为 **K** 的子字符串可以连接起来形成给定的字符串。
**举例:**

> **输入:**str = " abbaa " K = 2
> **输出:** abaa
> **解释:**
> 父串“abaa”大小为 2 的所有子串都是“ab”、“ba”和“aa”。在连接所有这些子字符串之后，可以获得给定的字符串“abbaaa”。
> **输入:**str = " abbcscsesed " K = 3
> **输出:**abcssesd
> **说明:**
> 父串“abcssesd”大小为 3 的所有子串都是“abc”、“bcs”、“cse”、“ses”和“esd”。在连接所有这些子字符串之后，可以获得给定的字符串“abcbcscsesesesd”。

**进场:**
按照以下步骤解决问题:

1.  我们可以清楚地观察到，通过串联长度为 **K** 的子串，除了第一个字符，任何子串的剩余 **K-1** 字符也出现在下一个子串中。
2.  因此，遍历字符串并将每个子字符串的第一个字符附加到**和**上，然后忽略下一个 **K-1** 字符。
3.  对除最后一个子字符串以外的所有子字符串重复此过程。
4.  将最后一个子串的所有字符追加到**和**中。
5.  返回 ans 作为所需的解码字符串。

以下是上述方法的实现:

## C++

```
// C++ program to generate a
// string whose substrings of
// length K concatenates to
// form given strings

#include <bits/stdc++.h>
using namespace std;

// Function to return the required
// required string
void decode_String(string str,
int K)
{
    string ans = "";
    // Iterate the given string
    for (int i = 0; i < str.size();
    i += K)
        // Append the first
        // character of every
        // substring of length K
        ans += str[i];

    // Consider all characters
    // from the last substring
    for(int i = str.size() - (K - 1);
    i < str.size(); i++)
        ans += str[i];

    cout << ans << endl;
}

// Driver Program
int main()
{
    int K = 3;
    string str = "abcbcscsesesesd";
    decode_String(str, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate a
// string whose substrings of
// length K concatenates to
// form given strings
class GFG{

// Function to return the required
// required string
public static void decode_String(String str,
                                 int K)
{
    String ans = "";

    // Iterate the given string
    for(int i = 0;
            i < str.length(); i += K)

       // Append the first
       // character of every
       // substring of length K
       ans += str.charAt(i);

    // Consider all characters
    // from the last substring
    for(int i = str.length() - (K - 1);
            i < str.length(); i++)
       ans += str.charAt(i);

    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{
    int K = 3;
    String str = "abcbcscsesesesd"; 

    decode_String(str, K);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to generate a
# string whose substrings of
# length K concatenates to
# form given strings

# Function to return the required
# required string
def decode_String(st, K):

    ans = ""

    # Iterate the given string
    for i in range(0, len(st), K):

        # Append the first
        # character of every
        # substring of length K
        ans += st[i]

    # Consider all characters
    # from the last substring
    for i in range(len(st) - (K - 1), len(st)):
        ans += st[i]

    print(ans)

# Driver code
if __name__ == "__main__":

    K = 3
    st = "abcbcscsesesesd"

    decode_String(st, K)

# This code is contributed by chitranayal
```

## C#

```
// C# program to generate a string
// whose substrings of length K
// concatenates to form given strings
using System;

class GFG{

// Function to return the required
// required string
public static void decode_String(String str,
                                 int K)
{
    String ans = "";

    // Iterate the given string
    for(int i = 0;
            i < str.Length; i += K)

        // Append the first
        // character of every
        // substring of length K
        ans += str[i];

    // Consider all characters
    // from the last substring
    for(int i = str.Length - (K - 1);
            i < str.Length; i++)
        ans += str[i];

    Console.WriteLine(ans);
}

// Driver code
public static void Main(String[] args)
{
    int K = 3;
    String str = "abcbcscsesesesd";

    decode_String(str, K);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to return the required
// required string
function decode_String(str, K)
{
    let ans = "";

    // Iterate the given string
    for(let i = 0;
            i < str.length; i += K)

        // Append the first
        // character of every
        // substring of length K
        ans += str[i];

    // Consider all characters
    // from the last substring
    for(let i = str.length - (K - 1);
            i < str.length; i++)
        ans += str[i];

    document.write(ans);
}

// Driver code
    let K = 3;
    let str = "abcbcscsesesesd"; 

    decode_String(str, K);

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
abcsesd
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*