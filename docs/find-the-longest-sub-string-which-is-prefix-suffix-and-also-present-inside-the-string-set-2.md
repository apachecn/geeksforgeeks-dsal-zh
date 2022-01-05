# 找出最长的子串，它是前缀、后缀，也存在于串内|集合 2

> 原文:[https://www . geesforgeks . org/find-最长的子字符串-前缀后缀兼现字符串集-2/](https://www.geeksforgeeks.org/find-the-longest-sub-string-which-is-prefix-suffix-and-also-present-inside-the-string-set-2/)

给定弦**弦**。任务是找到最长的子字符串，它是给定字符串 str 的前缀、后缀和子字符串。如果不存在这样的字符串，则打印 **-1** 。
**例:**

> **输入:**str = " geeksisfurgecksinplatformgekers "
> **输出:**gekers
> **输入:**str = " fixeprefixsuffix "
> **输出:** fix

**注:**本文第一集附[此处为](https://www.geeksforgeeks.org/find-the-longest-sub-string-which-is-prefix-suffix-and-also-present-inside-the-string/)。
**方法:**
实现采用 BIT 和 Z 算法。从[本](https://www.geeksforgeeks.org/two-dimensional-binary-indexed-tree-or-fenwick-tree/)和[本](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)了解更多。

*   首先我们使用 [Z 算法](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)计算 Z 数组。
*   从索引 z[i]将位数组中的值更新 1。
*   使用 pref 函数查询所需的最大长度子字符串。
*   如果 len 为 0，则从给定的字符串中不可能出现这样的子字符串。

下面是实现方式:

## C++

```
// C++ program to find that
// substring which is its
// suffix prefix and also
// found somewhere in between
#include <bits/stdc++.h>
using namespace std;

// Z-algorithm function
vector<int> z_function(string s)
{
    int n = s.size();
    vector<int> z(n);
    for (int i = 1, l = 0,
             r = 0;
         i < n;
         i++) {
        if (i <= r)
            z[i] = min(r - i + 1,
                       z[i - l]);

        while (i + z[i] < n
               && s[z[i]] == s[i + z[i]])
            z[i]++;

        if (i + z[i] - 1 > r)
            l = i, r = i + z[i] - 1;
    }
    return z;
}

int n, len = 0;

// BIT array
int bit[1000005];

string s;
vector<int> z;
map<int, int> m;

// bit update function which
// updates values from index
// "idx" to last by value "val"
void update(int idx, int val)
{
    if (idx == 0)
        return;
    while (idx <= n) {
        bit[idx] += val;
        idx += (idx & -idx);
    }
}

// Query function in bit
int pref(int idx)
{
    int ans = 0;
    while (idx > 0) {
        ans += bit[idx];
        idx -= (idx & -idx);
    }
    return ans;
}

// Driver Code
int main()
{
    s = "geeksisforgeeksinplatformgeeks";
    n = s.size();

    // Making the z array
    z = z_function(s);

    // update in the bit array from
    // index z[i] by increment of 1
    for (int i = 1; i < n; i++) {
        update(z[i], 1);
    }

    for (int i = n - 1; i > 1; i--) {
        // if the value in z[i] is
        // not equal to (n-i) then no
        // need to move further
        if (z[i] != (n - i))
            continue;

        // queryng for the maximum
        // length substring from
        // bit array
        if (pref(n) - pref(z[i] - 1) >= 2) {
            len = max(len, z[i]);
        }
    }

    if (!len)
        cout << "-1";
    else
        cout << s.substr(0, len);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find that
// substring which is its
// suffix prefix and also
// found somewhere in between
class GFG
{

// Z-algorithm function
static int[] z_function(char []s)
{
    int n = s.length;
    int []z = new int[n];
    for (int i = 1, l = 0, r = 0;
             i < n; i++)
    {
        if (i <= r)
            z[i] = Math.min(r - i + 1,
                            z[i - l]);

        while (i + z[i] < n &&
                 s[z[i]] == s[i + z[i]])
            z[i]++;

        if (i + z[i] - 1 > r)
        {
            l = i; r = i + z[i] - 1;
        }
    }
    return z;
}

static int n, len = 0;

// BIT array
static int []bit = new int[1000005];

static String s;
static int[] z;

// bit update function which
// updates values from index
// "idx" to last by value "val"
static void update(int idx, int val)
{
    if (idx == 0)
        return;
    while (idx <= n)
    {
        bit[idx] += val;
        idx += (idx & -idx);
    }
}

// Query function in bit
static int pref(int idx)
{
    int ans = 0;
    while (idx > 0)
    {
        ans += bit[idx];
        idx -= (idx & -idx);
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    s = "geeksisforgeeksinplatformgeeks";
    z = new int[s.length()];
    n = s.length();

    // Making the z array
    z = z_function(s.toCharArray());

    // update in the bit array from
    // index z[i] by increment of 1
    for (int i = 1; i < n; i++)
    {
        update(z[i], 1);
    }

    for (int i = n - 1; i > 1; i--)
    {
        // if the value in z[i] is
        // not equal to (n-i) then no
        // need to move further
        if (z[i] != (n - i))
            continue;

        // queryng for the maximum
        // length substring from
        // bit array
        if (pref(n) - pref(z[i] - 1) >= 2)
        {
            len = Math.max(len, z[i]);
        }
    }

    if (len == 0)
        System.out.println("-1");
    else
        System.out.println(s.substring(0, len));
}
}

// This code is contributed
// by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find that
# substring which is its
# suffix prefix and also
# found somewhere in between

# Z-algorithm function
def z_function(s):
    global z, n
    n = len(s)
    z = [0] * n
    l, r = 0, 0
    for i in range(1, n):
        if i <= r:
            z[i] = min(r - i + 1, z[i - 1])

        while (i + z[i] < n and s[z[i]] == s[i + z[i]]):
            z[i] += 1

        if (i + z[i] - 1 > r):
            l = i
            r = i + z[i] - 1
    return z

# bit update function which
# updates values from index
# "idx" to last by value "val"
def update(idx, val):
    global bit
    if idx == 0:
        return
    while idx <= n:
        bit[idx] += val
        idx += (idx & -idx)

# Query function in bit
def pref(idx):
    global bit
    ans = 0
    while idx > 0:
        ans += bit[idx]
        idx -= (idx & -idx)

    return ans

# Driver Code
if __name__ == "__main__":
    n = 0
    length = 0

    # BIT array
    bit = [0] * 1000005
    z = []
    m = dict()

    s = "geeksisforgeeksinplatformgeeks"

    # Making the z array
    z = z_function(s)

    # update in the bit array from
    # index z[i] by increment of 1
    for i in range(1, n):
        update(z[i], 1)

    for i in range(n - 1, 1, -1):

        # if the value in z[i] is
        # not equal to (n-i) then no
        # need to move further
        if z[i] != n - i:
            continue

        # queryng for the maximum
        # length substring from
        # bit array
        if (pref(n) - pref(z[i] - 1)) >= 2:
            length = max(length, z[i])

    if not length:
        print(-1)
    else:
        print(s[:length])

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find that
// substring which is its
// suffix prefix and also
// found somewhere in between
using System;

class GFG
{

// Z-algorithm function
static int[] z_function(char []s)
{
    int n = s.Length;
    int []z = new int[n];
    for (int i = 1, l = 0, r = 0;
             i < n; i++)
    {
        if (i <= r)
            z[i] = Math.Min(r - i + 1,
                            z[i - l]);

        while (i + z[i] < n &&
                 s[z[i]] == s[i + z[i]])
            z[i]++;

        if (i + z[i] - 1 > r)
        {
            l = i; r = i + z[i] - 1;
        }
    }
    return z;
}

static int n, len = 0;

// BIT array
static int []bit = new int[1000005];
static String s;
static int[] z;

// bit update function which
// updates values from index
// "idx" to last by value "val"
static void update(int idx, int val)
{
    if (idx == 0)
        return;
    while (idx <= n)
    {
        bit[idx] += val;
        idx += (idx & -idx);
    }
}

// Query function in bit
static int pref(int idx)
{
    int ans = 0;
    while (idx > 0)
    {
        ans += bit[idx];
        idx -= (idx & -idx);
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    s = "geeksisforgeeksinplatformgeeks";
    z = new int[s.Length];
    n = s.Length;

    // Making the z array
    z = z_function(s.ToCharArray());

    // update in the bit array from
    // index z[i] by increment of 1
    for (int i = 1; i < n; i++)
    {
        update(z[i], 1);
    }

    for (int i = n - 1; i > 1; i--)
    {
        // if the value in z[i] is
        // not equal to (n-i) then no
        // need to move further
        if (z[i] != (n - i))
            continue;

        // queryng for the maximum
        // length substring from
        // bit array
        if (pref(n) - pref(z[i] - 1) >= 2)
        {
            len = Math.Max(len, z[i]);
        }
    }

    if (len == 0)
        Console.WriteLine("-1");
    else
        Console.WriteLine(s.Substring(0, len));
}
}

// This code is contributed by PrinciRaj1992
```

**Output:** 

```
geeks
```

**时间复杂度:** O(N)