# 平衡括号的成本

> 原文:[https://www.geeksforgeeks.org/cost-balance-parantheses/](https://www.geeksforgeeks.org/cost-balance-parantheses/)

当每个左大括号都有一个右大括号，如“()()”或“()””或“()())”等时，括号被认为是平衡的。不正确的平衡包括()(“或”)((“等。这里的任务是纠正括号的顺序，以最小的成本完成。括号移动超过一个括号的代价是 1。如果括号不能平衡，那么打印-1。
**例:**

> 输入:()
> 输出:0
> **说明:**已经平衡
> 输入:)(
> 输出:4
> **说明:**首先，)在位置 1 <sup>st</sup> 走到最后一个位置，成本 3，所以我们得到()()。然后，)在位置 1 <sup>st</sup> 转到 2 <sup>nd</sup> 位置成本 1。所以，最后我们得到()()。因此，总成本为 4。

**算法:**

1.  将大括号存储为字符串。
2.  运行一个字符串大小的循环来存储左大括号和右大括号的计数。
3.  检查左大括号的数量是否等于右大括号的数量。
4.  如果大括号不相等，则打印-1，表示字符串无法平衡。否则继续。
5.  首先，在第 0 <sup>个</sup>索引处检查字符串是包含左大括号还是右大括号。如果我们得到一个左大括号，那么在数组中的索引 0 处存储+1，否则如果有右大括号，那么将-1 放在 0 <sup>第</sup>个索引处。
6.  现在运行一个从 1 <sup>st</sup> 索引到数组长度的循环。
    *   如果索引 I 处存在左大括号，则将+1 加到先前索引处的值，即 i-1，并将总和存储在索引 I 处。
    *   如果索引 I 处有右大括号，则将-1 加到先前索引处的值上，即 i-1，并将总和存储在索引 I 处。
    *   如果索引 I 处的值为负，即小于 0，则将数组[i]的绝对值添加到变量中(下面程序中的 ans)。
7.  最后得到可变 ans 中的最小成本。

下面是上述方法的实现:

## C++

```
// CPP code to calculate the minimum cost
// to make the given parentheses balanced
#include <bits/stdc++.h>
using namespace std;

int costToBalance(string s)
{
    if (s.length() == 0)
        cout << 0 << endl;

    // To store absolute count of
    // balanced and unbalanced parenthesis
    int ans = 0;

    // o(open bracket) stores count of '(' and
    // c(close bracket) stores count of ')'
    int o = 0, c = 0;

    for (int i = 0; i < s.length(); i++) {
        if (s[i] == '(')
            o++;
        if (s[i] == ')')
            c++;
    }

    if (o != c)
        return -1;

    int a[s.size()];
    if (s[0] == '(')
        a[0] = 1;
    else
        a[0] = -1;

    if (a[0] < 0)
        ans += abs(a[0]);

    for (int i = 1; i < s.length(); i++) {
        if (s[i] == '(')
            a[i] = a[i - 1] + 1;
        else
            a[i] = a[i - 1] - 1;
        if (a[i] < 0)
            ans += abs(a[i]);
    }

    return ans;
}

// Driver code
int main()
{
    string s;
    s = ")))(((";

    cout << costToBalance(s) << endl;

    s = "))((";
    cout << costToBalance(s) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to calculate the
// minimum cost to make the
// given parentheses balanced
import java.io.*;

class GFG
{
    static int costToBalance(String s)
    {
        if (s.length() == 0)
            System.out.println(0);

        // To store absolute count
        // of balanced and unbalanced
        // parenthesis
        int ans = 0;

        // o(open bracket) stores count
        // of '(' and c(close bracket)
        // stores count of ')'
        int o = 0, c = 0;

        for (int i = 0; i < s.length(); i++)
        {
            if (s.charAt(i) == '(')
                o++;
            if (s.charAt(i) == ')')
                c++;
        }

        if (o != c)
            return -1;

        int []a = new int[s.length()];
        if (s.charAt(0) == '(')
            a[0] = 1;
        else
            a[0] = -1;

        if (a[0] < 0)
            ans += Math.abs(a[0]);

        for (int i = 1; i < s.length(); i++)
        {
            if (s.charAt(i) == '(')
                a[i] = a[i - 1] + 1;
            else
                a[i] = a[i - 1] - 1;
            if (a[i] < 0)
                ans += Math.abs(a[i]);
        }

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        String s;
        s = ")))(((";

        System.out.println(costToBalance(s));

        s = "))((";
        System.out.println(costToBalance(s));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python 3 code to calculate the minimum cost
# to make the given parentheses balanced
def costToBalance(s):
    if (len(s) == 0):
        print(0)

    # To store absolute count of
    # balanced and unbalanced parenthesis
    ans = 0

    # o(open bracket) stores count of '(' and
    # c(close bracket) stores count of ')'
    o = 0
    c = 0

    for i in range(len(s)):
        if (s[i] == '('):
            o += 1
        if (s[i] == ')'):
            c += 1

    if (o != c):
        return -1

    a = [0 for i in range(len(s))]
    if (s[0] == '('):
        a[0] = 1
    else:
        a[0] = -1

    if (a[0] < 0):
        ans += abs(a[0])

    for i in range(1, len(s)):
        if (s[i] == '('):
            a[i] = a[i - 1] + 1
        else:
            a[i] = a[i - 1] - 1
        if (a[i] < 0):
            ans += abs(a[i])

    return ans

# Driver code
if __name__ == '__main__':
    s = ")))((("

    print(costToBalance(s))
    s = "))(("
    print(costToBalance(s))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# code to calculate the
// minimum cost to make the
// given parentheses balanced
using System;

class GFG
{
    static int costToBalance(string s)
    {
        if (s.Length == 0)
            Console.WriteLine(0);

        // To store absolute count
        // of balanced and unbalanced
        // parenthesis
        int ans = 0;

        // o(open bracket) stores count
        // of '(' and c(close bracket)
        // stores count of ')'
        int o = 0, c = 0;

        for (int i = 0; i < s.Length; i++)
        {
            if (s[i] == '(')
                o++;
            if (s[i] == ')')
                c++;
        }

        if (o != c)
            return -1;

        int []a = new int[s.Length];
        if (s[0] == '(')
            a[0] = 1;
        else
            a[0] = -1;

        if (a[0] < 0)
            ans += Math.Abs(a[0]);

        for (int i = 1; i < s.Length; i++)
        {
            if (s[i] == '(')
                a[i] = a[i - 1] + 1;
            else
                a[i] = a[i - 1] - 1;
            if (a[i] < 0)
                ans += Math.Abs(a[i]);
        }

        return ans;
    }

    // Driver code
    static void Main()
    {
        string s;
        s = ")))(((";

        Console.WriteLine (costToBalance(s));

        s = "))((";
        Console.WriteLine (costToBalance(s));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>

// javascript code to calculate the
// minimum cost to make the
// given parentheses balanced

    function costToBalance( s)
    {
        if (s.length == 0)
            document.write(0);

        // To store absolute count
        // of balanced and unbalanced
        // parenthesis
        var ans = 0;

        // o(open bracket) stores count
        // of '(' and c(close bracket)
        // stores count of ')'
        var o = 0, c = 0;

        for (var i = 0; i < s.length; i++)
        {
            if (s[i] == '(')
                o++;
            if (s[i] == ')')
                c++;
        }

        if (o != c)
            return -1;

        var a = new Array(s.Length);
        if (s[0] == '(')
            a[0] = 1;
        else
            a[0] = -1;

        if (a[0] < 0)
            ans += Math.abs(a[0]);

        for (var i = 1; i < s.length; i++)
        {
            if (s[i] == '(')
                a[i] = a[i - 1] + 1;
            else
                a[i] = a[i - 1] - 1;
            if (a[i] < 0)
                ans += Math.abs(a[i]);
        }

        return ans;
    }

    // Driver code
        var s;
        s = ")))(((";

        document.write(costToBalance(s) + "<br>");

        s = "))((";
        document.write(costToBalance(s) + "<br>" );

// This code is contributed by bunnyram19.
</script>
```

**Output:** 

```
9
4
```

**时间复杂度:** O(N)，N =字符串长度

**辅助空间:** O(N)