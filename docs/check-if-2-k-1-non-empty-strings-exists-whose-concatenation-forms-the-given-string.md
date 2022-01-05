# 检查是否存在 2 * K + 1 个非空字符串，其连接形成给定的字符串

> 原文:[https://www . geeksforgeeks . org/check-if-2-k-1-非空字符串-存在-其串联形成给定字符串/](https://www.geeksforgeeks.org/check-if-2-k-1-non-empty-strings-exists-whose-concatenation-forms-the-given-string/)

给定一个由 **N** 字符和正整数 **K** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是检查是否存在 **(K + 1)** 字符串，即**A<sub>1</sub>T13】、**A<sub>2</sub>T17】、**A<sub>3</sub>T21】、…、**A ****A <sub>(K + 1)</sub>** 使得串的串接 **A <sub>1</sub>** 、**A<sub>2</sub>T37】、**A<sub>3</sub>T41】、…、**A<sub>K</sub>T45】和**A<sub>(K+1)</sub>T49】以及串的串接 **A<sub>(K–2)</sub>**，…， **A <sub>1</sub>** ， **A <sub>0</sub>** 为弦 **S** 。 如果发现是真的，则打印**“是”**。否则，打印**“否”**。******************

**示例:**

> **输入:** S = "qwqwq "，K = 1
> **输出:**是
> **说明:**
> 将字符串**A<sub>1</sub>T12】视为“qw”，将**A<sub>2</sub>T16】视为“q”。现在 **A <sub>1</sub>** 、 **A <sub>2</sub>** 的串联，与 **A <sub>1</sub>** 的反向为“qwqwq”，与给定的字符串 s 相同****
> 
> **输入:** S = "qwqwa "，K = 2
> **输出:**否

**方法:**给定问题可以基于这样的观察来解决:对于满足给定条件的字符串 **S** ，第一个 **K** 字符必须等于给定字符串的最后一个 **K** 字符。按照以下步骤解决问题:

*   如果( **2*K + 1)** 的值大于 **N** ，则打印**“否”**[从功能](https://www.geeksforgeeks.org/return-statement-in-c-cpp-with-examples/)返回。
*   否则，将大小为 **K** 的前缀即**S【0，…，K】**存储在一个字符串 **A** 中，大小为 **K** 的后缀即**S【N–K，…，N–1】**存储在一个字符串 **B** 中。
*   [反转弦](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/) **B** 检查 **A** 是否等于 **B** 。如果发现属实，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the string S
// can be obtained by (K + 1) non-empty
// substrings whose concatenation and
// concatenation of the reverse
// of these K strings
void checkString(string s, int k)
{
    // Stores the size of the string
    int n = s.size();

    // If n is less than 2*k+1
    if (2 * k + 1 > n) {
        cout << "No";
        return;
    }

    // Stores the first K characters
    string a = s.substr(0, k);

    // Stores the last K characters
    string b = s.substr(n - k, k);

    // Reverse the string
    reverse(b.begin(), b.end());

    // If both the strings are equal
    if (a == b)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    string S = "qwqwq";
    int K = 1;
    checkString(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

      // Function to check if the string S
    // can be obtained by (K + 1) non-empty
    // substrings whose concatenation and
    // concatenation of the reverse
    // of these K strings
    static void checkString(String s, int k)
    {

        // Stores the size of the string
        int n = s.length();

        // If n is less than 2*k+1
        if (2 * k + 1 > n) {
            System.out.println("No");
            return;
        }

        // Stores the first K characters
        String a = s.substring(0, k);

        // Stores the last K characters
        String b = s.substring(n - k, n);

        // Reverse the string
        StringBuffer str = new StringBuffer(b);
        // To reverse the string
        str.reverse();
        b = str.toString();     

        // If both the strings are equal
        if (a.equals(b))
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    // Driver Code
    public static void main (String[] args)
    {
        String S = "qwqwq";
        int K = 1;
        checkString(S, K);
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the S
# can be obtained by (K + 1) non-empty
# substrings whose concatenation and
# concatenation of the reverse
# of these K strings
def checkString(s, k):

    # Stores the size of the string
    n = len(s)

    # If n is less than 2*k+1
    if (2 * k + 1 > n):
        print("No")
        return

    # Stores the first K characters
    a = s[0:k]

    # Stores the last K characters
    b = s[n - k:n]

    # Reverse the string
    b = b[::-1]

    # If both the strings are equal
    if (a == b):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    S = "qwqwq"
    K = 1
    checkString(S, K)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to check if the string S
    // can be obtained by (K + 1) non-empty
    // substrings whose concatenation and
    // concatenation of the reverse
    // of these K strings
    static void checkString(string s, int k)
    {

        // Stores the size of the string
        int n = s.Length;

        // If n is less than 2*k+1
        if (2 * k + 1 > n) {
            Console.Write("No");
            return;
        }

        // Stores the first K characters
        string a = s.Substring(0, k);

        // Stores the last K characters
        string b = s.Substring(n - k, k);

        // Reverse the string
        char[] arr = b.ToCharArray();
        Array.Reverse(arr);
        b = new String(arr);

        // If both the strings are equal
        if (a == b)
            Console.Write("Yes");
        else
            Console.Write("No");
    }

    // Driver Code
    public static void Main()
    {
        string S = "qwqwq";
        int K = 1;
        checkString(S, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if the string S
// can be obtained by (K + 1) non-empty
// substrings whose concatenation and
// concatenation of the reverse
// of these K strings
function checkString(s, k)
{
    // Stores the size of the string
    let n = s.length;

    // If n is less than 2*k+1
    if (2 * k + 1 > n) {
        document.write("No");
        return;
    }

    // Stores the first K characters
    let a = s.substr(0, k);

    // Stores the last K characters
    let b = s.substr(n - k, k);

    // Reverse the string
    b.split("").reverse().join("")

    // If both the strings are equal
    if (a == b)
        document.write("Yes");
    else
        document.write("No");
}

// Driver Code
    let S = "qwqwq";
    let K = 1;
    checkString(S, K);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)