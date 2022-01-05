# 以任意顺序连接字符串，获得“AB”的最大数量

> 原文:[https://www . geesforgeks . org/concatenate-strings-in-any-order-get-max-number-of-ab/](https://www.geeksforgeeks.org/concatenate-strings-in-any-order-to-get-maximum-number-of-ab/)

给定一个长度为 N 的字符串数组，允许以任何顺序连接它们。在结果字符串中找到“AB”的最大可能出现次数。

**示例:**

> **输入:** N = 4，arr = {“BCA”、“BGGGA”、“JKA”、“BALB”}
> **输出:** 3
> 按 JKA + BGGA + BCA + BALB 的顺序串联，会变成 JK**AB**GG**AB**C**AB**ALB，有 3 次出现‘AB’。
> 
> **输入:** N = 3，arr = {“ABCA”、“BOOK”、“BAND”}
> **输出:** 2

**方法:**
预先计算每根弦内的 ABs 数量。当重新排列琴弦时，集中注意延伸超过两个琴弦的 ABs 数量的变化。每个字符串中唯一重要的字符是它的第一个和最后一个字符。
能够为答案做出贡献的字符串有:

1.  以 B 开头，以 a 结尾的字符串。
2.  以 B 开头但不以 a 结尾的字符串。
3.  不以 B 开头但以 a 结尾的字符串。

假设 c1、c2 和 c3 分别是类别 1、2 和 3 的字符串数。

*   如果 c1 = 0，那么答案是 min(c2，c3)，因为只要两者都可用，我们就可以取两者并连接。
*   如果 c1 > 0，c2 + c3 = 0，那么答案是 C1–1，因为我们将它们以串行顺序逐个连接。
*   如果 c1 > 0 和 c2 + c3 > 0，取 min(c2，c3) = p，首先逐个连接类别 1 字符串和额外的 C1–1“AB ”,然后如果类别 2 和 3 都可用，则在当前结果字符串的开头添加类别 3，在当前结果字符串的结尾添加类别 2。
*   有 C1–1+2 = C1+1 个额外的‘AB’，现在 c2 和 c3 减少 1，p 变成 p–1，现在取两个
    类别 2 和 3，只要两个都可用，就把它们相加，现在我们总共得到 C1+1+(p–1)= C1+p 个额外的‘AB’。这意味着 c1 + min(c2，c3)。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum number of ABs
int maxCountAB(string s[], int n)
{
    // variable A, B, AB for count strings that
    // end with 'A' but not end with 'B', 'B' but
    // does not end with 'A' and 'B' and ends
    // with 'A' respectively.
    int A = 0, B = 0, BA = 0, ans = 0;

    for (int i = 0; i < n; i++) {
        string S = s[i];
        int L = S.size();
        for (int j = 0; j < L - 1; j++) {

            // 'AB' is already present in string
            // before concatenate them
            if (S.at(j) == 'A' &&
                           S.at(j + 1) == 'B') {
                ans++;
            }
        }

        // count of strings that begins
        // with 'B' and ends with 'A
        if (S.at(0) == 'B' && S.at(L - 1) == 'A')
            BA++;

        // count of strings that begins
        // with 'B' but does not end with 'A'
        else if (S.at(0) == 'B')
            B++;

        // count of strings that ends with
        // 'A' but not end with 'B'
        else if (S.at(L - 1) == 'A')
            A++;
    }

    // updating the value of ans and
    // add extra count of 'AB'
    if (BA == 0)
        ans += min(B, A);
    else if (A + B == 0)
        ans += BA - 1;
    else
        ans += BA + min(B, A);

    return ans;
}

// Driver Code
int main()
{

    string s[] = { "ABCA", "BOOK", "BAND" };

    int n = sizeof(s) / sizeof(s[0]);

    cout << maxCountAB(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

// Function to find maximum number of ABs
static int maxCountAB(String s[], int n)
{
    // variable A, B, AB for count strings that
    // end with 'A' but not end with 'B', 'B' but
    // does not end with 'A' and 'B' and ends
    // with 'A' respectively.
    int A = 0, B = 0, BA = 0, ans = 0;

    for (int i = 0; i < n; i++)
    {
        String S = s[i];
        int L = S.length();
        for (int j = 0; j < L - 1; j++)
        {

            // 'AB' is already present in string
            // before concatenate them
            if (S.charAt(j) == 'A' &&
                        S.charAt(j + 1) == 'B')
            {
                ans++;
            }
        }

        // count of strings that begins
        // with 'B' and ends with 'A
        if (S.charAt(0) == 'B' && S.charAt(L - 1) == 'A')
            BA++;

        // count of strings that begins
        // with 'B' but does not end with 'A'
        else if (S.charAt(0) == 'B')
            B++;

        // count of strings that ends with
        // 'A' but not end with 'B'
        else if (S.charAt(L - 1) == 'A')
            A++;
    }

    // updating the value of ans and
    // add extra count of 'AB'
    if (BA == 0)
        ans += Math.min(B, A);
    else if (A + B == 0)
        ans += BA - 1;
    else
        ans += BA + Math.min(B, A);

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String s[] = { "ABCA", "BOOK", "BAND" };

    int n = s.length;

    System.out.println(maxCountAB(s, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to find maximum number of ABs
def maxCountAB(s,n):
    # variable A, B, AB for count strings that
    # end with 'A' but not end with 'B', 'B' but
    # does not end with 'A' and 'B' and ends
    # with 'A' respectively.
    A = 0
    B = 0
    BA = 0
    ans = 0

    for i in range(n):
        S = s[i]
        L = len(S)
        for j in range(L-1):
            # 'AB' is already present in string
            # before concatenate them
            if (S[j] == 'A' and S[j + 1] == 'B'):
                ans += 1

        # count of strings that begins
        # with 'B' and ends with 'A
        if (S[0] == 'B' and S[L - 1] == 'A'):
            BA += 1

        # count of strings that begins
        # with 'B' but does not end with 'A'
        elif (S[0] == 'B'):
            B += 1

        # count of strings that ends with
        # 'A' but not end with 'B'
        elif (S[L - 1] == 'A'):
            A += 1

    # updating the value of ans and
    # add extra count of 'AB'
    if (BA == 0):
        ans += min(B, A)
    elif (A + B == 0):
        ans += BA - 1
    else:
        ans += BA + min(B, A)
    return ans

# Driver Code
if __name__ == '__main__':
    s = ["ABCA", "BOOK", "BAND"]

    n = len(s)

    print(maxCountAB(s, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to find maximum number of ABs
    static int maxCountAB(string []s, int n)
    {
        // variable A, B, AB for count strings that
        // end with 'A' but not end with 'B', 'B' but
        // does not end with 'A' and 'B' and ends
        // with 'A' respectively.
        int A = 0, B = 0, BA = 0, ans = 0;

        for (int i = 0; i < n; i++)
        {
            string S = s[i];
            int L = S.Length;
            for (int j = 0; j < L - 1; j++)
            {

                // 'AB' is already present in string
                // before concatenate them
                if (S[j] == 'A' &&
                            S[j + 1] == 'B')
                {
                    ans++;
                }
            }

            // count of strings that begins
            // with 'B' and ends with 'A
            if (S[0] == 'B' && S[L - 1] == 'A')
                BA++;

            // count of strings that begins
            // with 'B' but does not end with 'A'
            else if (S[0] == 'B')
                B++;

            // count of strings that ends with
            // 'A' but not end with 'B'
            else if (S[L - 1] == 'A')
                A++;
        }

        // updating the value of ans and
        // add extra count of 'AB'
        if (BA == 0)
            ans += Math.Min(B, A);

        else if (A + B == 0)
            ans += BA - 1;
        else
            ans += BA + Math.Min(B, A);

        return ans;
    }

    // Driver Code
    public static void Main()
    {
        string []s = { "ABCA", "BOOK", "BAND" };

        int n = s.Length;

        Console.WriteLine(maxCountAB(s, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to find maximum number of ABs
function maxCountAB(s, n)
{
    // variable A, B, AB for count strings that
    // end with 'A' but not end with 'B', 'B' but
    // does not end with 'A' and 'B' and ends
    // with 'A' respectively.
    var A = 0, B = 0, BA = 0, ans = 0;

    for (var i = 0; i < n; i++) {
        var S = s[i];
        var L = S.length;
        for (var j = 0; j < L - 1; j++) {

            // 'AB' is already present in string
            // before concatenate them
            if (S[j] == 'A' &&
                           S[j + 1] == 'B') {
                ans++;
            }
        }

        // count of strings that begins
        // with 'B' and ends with 'A
        if (S[0] == 'B' && S[L - 1] == 'A')
            BA++;

        // count of strings that begins
        // with 'B' but does not end with 'A'
        else if (S[0] == 'B')
            B++;

        // count of strings that ends with
        // 'A' but not end with 'B'
        else if (S[L - 1] == 'A')
            A++;
    }

    // updating the value of ans and
    // add extra count of 'AB'
    if (BA == 0)
        ans += Math.min(B, A);
    else if (A + B == 0)
        ans += BA - 1;
    else
        ans += BA + Math.min(B, A);

    return ans;
}

// Driver Code
var s = ["ABCA", "BOOK", "BAND"];
var n = s.length;
document.write( maxCountAB(s, n));

</script>
```

**Output:** 

```
2
```