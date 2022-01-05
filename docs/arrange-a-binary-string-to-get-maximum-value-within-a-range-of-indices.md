# 排列一个二进制字符串，得到一个索引范围内的最大值

> 原文:[https://www . geeksforgeeks . org/arrange-a-binary-string-to-get-a-range-a-indexes 中的最大值/](https://www.geeksforgeeks.org/arrange-a-binary-string-to-get-maximum-value-within-a-range-of-indices/)

给定一个仅由 0 和 1 组成的字符串。现在给你 N 个不相交的范围 L，R(L)<= R), more specifically [L1, R1], [L2, R2], …, [LN, RN], No two of these intervals overlap — formally, for each valid i, j such that i!=j, either Ri<lj or="" rj="">任务是找到一个同时满足以下两个条件的有效排列:</lj>

1.  所有 N 个给定范围之间的数字总和将是最大值。
2.  该字符串在字典中最大。字符串 1100 在字典上大于字符串 1001。

**示例:**

> **输入**
> 11100
> 2
> 2 3
> 5 5
> **输出**
> 01101
> 首先我们把 1 放在位置 2 和 3，然后在位置 5 因为
> 没有 1 了，形成的字符串是 01101。
> **输入**
> 0000111 *2
> 1 1
> 1 2
> **输出**
> 1110000
> 在上面的例子中，我们，首先把 1 放在第 1 和第 2 个位置，然后我们还有另一个‘1’剩下，
> 所以，我们用它来最大化字符串的字典顺序，我们把它放在第 3 个位置和*

***接近***

*   *首先优先考虑的是使所有 l 和 r 之间的 1 的计数最大。我们计算数组中 1 的数量，并将它们存储在一个变量中。*
*   *在接受输入后，我们将每个 l 和 r 的范围更新 1，以便只标记首先用 1 填充的位置。*
*   *然后，我们取数组的前缀和，这样我们就得到先固定 1 的位置。然后我们在左边的前缀和数组中运行一个循环。如果我们得到任何一个大于 1 的位置，这意味着我们在那个指数中有一个 l-r。我们继续将 1 放入这些索引中，直到 1 的计数变为零。*
*   *现在，在最大化操作完成之后，如果还剩下一些 1，那么我们开始字典式最大化。我们再次从前缀和数组的左边开始循环。如果我们找到一个值为 0 的索引，这表明没有 l-r 具有该索引，那么我们在该索引中放一个 1，从而继续，直到所有剩余的 1 都被填充。*

*下面是上述方法的实现:*

## *C++*

```
*// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

void arrange(string s)
{
    int cc = 0;

    // Storing the count of 1's in the string
    for (int i = 0; i < s.length(); i++)
    {
        if (s[i] == '1') cc++;
    }

    int a[s.length() + 1] = {0};

    // Query of l and r
    int qq[][2] = {{2, 3}, {5, 5}};

    int n = sizeof(qq) / sizeof(qq[0]);
    for (int i = 0; i < n; i++)
    {
        int l = qq[i][0], r = qq[i][1];
        l--, r--;
        a[l]++;

        // Applying range update technique.
        a[r + 1]--;
    }

    int len_a = sizeof(a) / sizeof(a[0]);
    for (int i = 1; i < len_a; i++)
    {
        // Taking prefix sum to get the range update values
        a[i] += a[i - 1];
    }

    // Final array which will store the arranged string
    int zz[s.length()] = {0};

    for (int i = 0; i < len_a - 1; i++)
    {
        if (a[i] > 0)
        {
            if (cc > 0)
            {
                zz[i] = 1;
                cc--;
            }
            else
                break;
        }

        if (cc == 0) break;
    }

    // if after maximizing the ranges any 1 is left
    // then we maximize the string lexicographically.
    if (cc > 0)
    {
        for (int i = 0; i < s.length(); i++)
        {
            if (zz[i] == 0)
            {
                zz[i] = 1;
                cc--;
            }
            if (cc == 0) break;
        }
    }

    for (int i = 0; i < s.length(); i++)
        cout << zz[i];
    cout << endl;
}

// Driver Code
int main()
{
    string str = "11100";
    arrange(str);
    return 0;
}

// This code is contributed by
// sanjeev2552*
```

## *Java 语言(一种计算机语言，尤用于创建网站)*

```
*// Java implementation of the approach
class GFG
{

static void arrange(String s)
{
    int cc = 0;

    // Storing the count of 1's in the String
    for (int i = 0; i < s.length(); i++)
    {
        if (s.charAt(i) == '1') cc++;
    }

    int []a = new int[s.length() + 1];

    // Query of l and r
    int qq[][] = {{2, 3}, {5, 5}};

    int n = qq.length;
    for (int i = 0; i < n; i++)
    {
        int l = qq[i][0], r = qq[i][1];
        l--; r--;
        a[l]++;

        // Applying range update technique.
        a[r + 1]--;
    }

    int len_a = a.length;
    for (int i = 1; i < len_a; i++)
    {
        // Taking prefix sum to get the range update values
        a[i] += a[i - 1];
    }

    // Final array which will store the arranged String
    int []zz = new int[s.length()];

    for (int i = 0; i < len_a - 1; i++)
    {
        if (a[i] > 0)
        {
            if (cc > 0)
            {
                zz[i] = 1;
                cc--;
            }
            else
                break;
        }

        if (cc == 0) break;
    }

    // if after maximizing the ranges any 1 is left
    // then we maximize the String lexicographically.
    if (cc > 0)
    {
        for (int i = 0; i < s.length(); i++)
        {
            if (zz[i] == 0)
            {
                zz[i] = 1;
                cc--;
            }
            if (cc == 0) break;
        }
    }
    for (int i = 0; i < s.length(); i++)
        System.out.print(zz[i]);
    System.out.println();
}

// Driver Code
public static void main(String[] args)
{
    String str = "11100";
    arrange(str);
}
}

// This code is contributed by Rajput-Ji*
```

## *蟒蛇 3*

```
*# Python implementation of the approach
def arrange(s):
    cc = 0

    # Storing the count of 1's in the string
    for i in range(len(s)):
        if(s[i]=="1"):
            cc+= 1
    a =[0]*(len(s)+1)

    # Query of l and r
    qq =[(2, 3), (5, 5)]

    n = len(qq)
    for i in range(n):
        l, r = qq[i][0], qq[i][1]
        l-= 1
        r-= 1
        a[l]+= 1

        # Applying range update technique.
        a[r + 1]-= 1

    for i in range(1, len(a)):

        # Taking prefix sum to get the range update values
        a[i]= a[i]+a[i-1]

    # Final array which will store the arranged string
    zz =[0]*len(s)

    for i in range(len(a)-1):
        if(a[i]>0):
            if(cc>0):
                zz[i]= 1
                cc-= 1
            else:
                break
        if(cc == 0):
            break

    # if after maximizing the ranges any 1 is left
    # then we maximize the string lexicographically.
    if(cc>0):

        for i in range(len(s)):
            if(zz[i]== 0):
                zz[i]= 1
                cc-= 1
            if(cc == 0):
                break
    print(*zz, sep ="")

str = "11100"
arrange(str)*
```

## *C#*

```
*// C# implementation of the approach
using System;

class GFG
{

static void arrange(String s)
{
    int cc = 0;

    // Storing the count of 1's in the String
    for (int i = 0; i < s.Length; i++)
    {
        if (s[i] == '1') cc++;
    }

    int []a = new int[s.Length + 1];

    // Query of l and r
    int [,]qq = {{2, 3}, {5, 5}};

    int n = qq.GetLength(0);
    for (int i = 0; i < n; i++)
    {
        int l = qq[i, 0], r = qq[i, 1];
        l--; r--;
        a[l]++;

        // Applying range update technique.
        a[r + 1]--;
    }

    int len_a = a.Length;
    for (int i = 1; i < len_a; i++)
    {
        // Taking prefix sum to get the range update values
        a[i] += a[i - 1];
    }

    // Final array which will store the arranged String
    int []zz = new int[s.Length];

    for (int i = 0; i < len_a - 1; i++)
    {
        if (a[i] > 0)
        {
            if (cc > 0)
            {
                zz[i] = 1;
                cc--;
            }
            else
                break;
        }

        if (cc == 0) break;
    }

    // if after maximizing the ranges any 1 is left
    // then we maximize the String lexicographically.
    if (cc > 0)
    {
        for (int i = 0; i < s.Length; i++)
        {
            if (zz[i] == 0)
            {
                zz[i] = 1;
                cc--;
            }
            if (cc == 0) break;
        }
    }
    for (int i = 0; i < s.Length; i++)
        Console.Write(zz[i]);
    Console.WriteLine();
}

// Driver Code
public static void Main(String[] args)
{
    String str = "11100";
    arrange(str);
}
}

// This code is contributed by PrinciRaj1992*
```

## *java 描述语言*

```
*<script>

// Javascript implementation of the approach

function arrange(s)
{
    var cc = 0;

    // Storing the count of 1's in the string
    for(var i = 0; i < s.length; i++)
    {
        if (s[i] == '1') cc++;
    }

    var a = Array(s.length+1).fill(0);

    // Query of l and r
    var qq = [[2, 3], [5, 5]];

    var n = qq.length;
    for (var i = 0; i < n; i++)
    {
        var l = qq[i][0], r = qq[i][1];
        l--, r--;
        a[l]++;

        // Applying range update technique.
        a[r + 1]--;
    }

    var len_a = a.length;
    for (var i = 1; i < len_a; i++)
    {
        // Taking prefix sum to get the range update values
        a[i] += a[i - 1];
    }

    // Final array which will store the arranged string
    var zz = Array(s.length).fill(0);

    for (var i = 0; i < len_a - 1; i++)
    {
        if (a[i] > 0)
        {
            if (cc > 0)
            {
                zz[i] = 1;
                cc--;
            }
            else
                break;
        }

        if (cc == 0) break;
    }

    // if after maximizing the ranges any 1 is left
    // then we maximize the string lexicographically.
    if (cc > 0)
    {
        for (var i = 0; i < s.length; i++)
        {
            if (zz[i] == 0)
            {
                zz[i] = 1;
                cc--;
            }
            if (cc == 0) break;
        }
    }

    for (var i = 0; i < s.length; i++)
        document.write( zz[i]);
    document.write("<br>");
}

// Driver Code
var str = "11100";
arrange(str);

</script>*
```

***Output:** 

```
01101
```*