# 求长度为 N 的二进制字符串中至少有 3 个连续 1 的个数

> 原文:[https://www . geesforgeks . org/find-长度为 n 的二进制字符串的数量，至少有 3 个连续的 1/](https://www.geeksforgeeks.org/find-the-number-of-binary-strings-of-length-n-with-at-least-3-consecutive-1s/)

给定一个整数 **N** 。任务是找出长度为 **N** 的所有可能的不同二进制字符串的数量，这些字符串至少有 3 个连续的 1。
**例:**

> **输入:** N = 3
> **输出:** 1
> 唯一可能长度为 3 的字符串是“111”。
> **输入:** N = 4
> **输出:** 3
> 这 3 个字符串分别是“1110”、“0111”和“1111”。

**天真的做法:**考虑所有可能的字符串。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if s contains
// three consecutive 1's
bool check(string& s)
{
    int n = s.length();
    for (int i = 2; i < n; i++) {
        if (s[i] == '1' && s[i - 1] == '1' && s[i - 2] == '1')
            return 1;
    }
    return 0;
}

// Function to return the count
// of required strings
int countStr(int i, string& s)
{
    if (i < 0) {
        if (check(s))
            return 1;
        return 0;
    }
    s[i] = '0';
    int ans = countStr(i - 1, s);
    s[i] = '1';
    ans += countStr(i - 1, s);
    s[i] = '0';
    return ans;
}

// Driver code
int main()
{
    int N = 4;
    string s(N, '0');
    cout << countStr(N - 1, s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if s contains
// three consecutive 1's
static boolean check(String s)
{
    int n = s.length();
    for (int i = 2; i < n; i++)
    {
        if (s.charAt(i) == '1' &&
          s.charAt(i-1) == '1' &&
          s.charAt(i-2) == '1')
            return true;
    }
    return false;
}

// Function to return the count
// of required strings
static int countStr(int i, String s)
{
    if (i < 0)
    {
        if (check(s))
            return 1;
        return 0;
    }
    char[] myNameChars = s.toCharArray();
    myNameChars[i] = '0';
    s = String.valueOf(myNameChars);

    int ans = countStr(i - 1, s);
    char[] myChar = s.toCharArray();
    myChar[i] = '1';
    s = String.valueOf(myChar);

    ans += countStr(i - 1, s);
    char[]myChar1 = s.toCharArray();
    myChar1[i] = '0';
    s = String.valueOf(myChar1);

    return ans;
}

// Driver code
public static void main(String args[])
{
    int N = 4;
    String s = "0000";
    System.out.println(countStr(N - 1, s));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if s contains
# three consecutive 1's
def check(s) :
    n = len(s);
    for i in range(2, n) :
        if (s[i] == '1' and s[i - 1] == '1' and
                            s[i - 2] == '1') :
            return 1;

# Function to return the count
# of required strings
def countStr(i, s) :

    if (i < 0) :
        if (check(s)) :
            return 1;
        return 0;

    s[i] = '0';
    ans = countStr(i - 1, s);

    s[i] = '1';
    ans += countStr(i - 1, s);

    s[i] = '0';
    return ans;

# Driver code
if __name__ == "__main__" :
    N = 4;
    s = list('0' * N);

    print(countStr(N - 1, s));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
// value x
using System;

class GFG
{

// Function that returns true if s contains
// three consecutive 1's
static bool check(String s)
{
    int n = s.Length;
    for (int i = 2; i < n; i++)
    {
        if (s[i] == '1' && s[i - 1] == '1' && s[i - 2] == '1')
            return true;
    }
    return false;
}

// Function to return the count
// of required strings
static int countStr(int i, String s)
{
    if (i < 0)
    {
        if (check(s))
            return 1;
        return 0;
    }
    char[] myNameChars = s.ToCharArray();
    myNameChars[i] = '0';
    s = String.Join("", myNameChars);

    int ans = countStr(i - 1, s);
    char[] myChar = s.ToCharArray();
    myChar[i] = '1';
    s = String.Join("", myChar);

    ans += countStr(i - 1, s);
    char[]myChar1 = s.ToCharArray();
    myChar1[i] = '0';
    s = String.Join("", myChar1);

    return ans;
}

// Driver code
public static void Main(String []args)
{
    int N = 4;
    String s = "0000";
    Console.WriteLine(countStr(N - 1, s));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
// value x

// Function that returns true if s contains
// three consecutive 1's
function check(s)
{
    let n = s.length;
    for (let i = 2; i < n; i++)
    {
        if (s[i] == '1' &&
          s[i-1] == '1' &&
          s[i-2] == '1')
            return true;
    }
    return false;
}

// Function to return the count
// of required strings
function countStr(i,s)
{
    if (i < 0)
    {
        if (check(s))
            return 1;
        return 0;
    }
    let myNameChars = s.split("");
    myNameChars[i] = '0';
    s = (myNameChars).join("");

    let ans = countStr(i - 1, s);
    let myChar = s.split("");
    myChar[i] = '1';
    s = (myChar).join("");

    ans += countStr(i - 1, s);
    let myChar1 = s.split("");
    myChar1[i] = '0';
    s = (myChar1).join("");

    return ans;
}

// Driver code
let N = 4;
let s = "0000";
document.write(countStr(N - 1, s));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(2<sup>N</sup>)
T5】空间复杂度: O(N)因为递归栈空间。
**高效方法:**我们使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来计算字符串的数量。
**DP 的状态:** dp(i，x):表示长度为 I 且在 i + 1 到 i + x 位置有 x 个连续 1 的字符串的数量。
**递归:** dp(i，x)= DP(I–1，0)+DP(I–1，x + 1)
递归是基于字符串在 I 位置可以有“0”或“1”的事实。

1.  如果它在 I 位置有一个' 0 '，那么对于 x = 0 的第(i-1)个位置值。
2.  如果它在 I 位置有一个' 1 '，则 x 的第(i-1)个位置值= x 在 i + 1 位置的值。

**基础条件:** dp(i，3) = 2 <sup>i</sup> 。因为一旦你有 3 个连续的 1，你就不在乎字符串的 1，2…i 位置有什么字符，因为所有的字符串都是有效的。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int n;

// Function to return the count
// of required strings
int solve(int i, int x, int dp[][4])
{
    if (i < 0)
        return x == 3;
    if (dp[i][x] != -1)
        return dp[i][x];

    // '0' at ith position
    dp[i][x] = solve(i - 1, 0, dp);

    // '1' at ith position
    dp[i][x] += solve(i - 1, x + 1, dp);
    return dp[i][x];
}

// Driver code
int main()
{
    n = 4;
    int dp[n][4];

    for (int i = 0; i < n; i++)
        for (int j = 0; j < 4; j++)
            dp[i][j] = -1;

    for (int i = 0; i < n; i++) {

        // Base condition:
        // 2^(i+1) because of 0 indexing
        dp[i][3] = (1 << (i + 1));
    }
    cout << solve(n - 1, 0, dp);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    static int n;

    // Function to return the count
    // of required strings
    static int solve(int i, int x, int dp[][])
    {
        if (i < 0)
        {
            return x == 3 ? 1 : 0;
        }
        if (dp[i][x] != -1)
        {
            return dp[i][x];
        }

        // '0' at ith position
        dp[i][x] = solve(i - 1, 0, dp);

        // '1' at ith position
        dp[i][x] += solve(i - 1, x + 1, dp);
        return dp[i][x];
    }

    // Driver code
    public static void main(String[] args)
    {
        n = 4;
        int dp[][] = new int[n][4];

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < 4; j++)
            {
                dp[i][j] = -1;
            }
        }

        for (int i = 0; i < n; i++)
        {

            // Base condition:
            // 2^(i+1) because of 0 indexing
            dp[i][3] = (1 << (i + 1));
        }
        System.out.print(solve(n - 1, 0, dp));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count
# of required strings
def solve(i, x, dp):
    if (i < 0):
        return x == 3
    if (dp[i][x] != -1):
        return dp[i][x]

    # '0' at ith position
    dp[i][x] = solve(i - 1, 0, dp)

    # '1' at ith position
    dp[i][x] += solve(i - 1, x + 1, dp)
    return dp[i][x]

# Driver code
if __name__ == "__main__":

    n = 4;
    dp = [[0 for i in range(n)] for j in range(4)]

    for i in range(n):
        for j in range(4):
            dp[i][j] = -1

    for i in range(n) :

        # Base condition:
        # 2^(i+1) because of 0 indexing
        dp[i][3] = (1 << (i + 1))

    print(solve(n - 1, 0, dp))

# This code is contributed by ChitraNayal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    static int n;

    // Function to return the count
    // of required strings
    static int solve(int i, int x, int [,]dp)
    {
        if (i < 0)
        {
            return x == 3 ? 1 : 0;
        }
        if (dp[i,x] != -1)
        {
            return dp[i,x];
        }

        // '0' at ith position
        dp[i,x] = solve(i - 1, 0, dp);

        // '1' at ith position
        dp[i,x] += solve(i - 1, x + 1, dp);
        return dp[i,x];
    }

    // Driver code
    public static void Main(String[] args)
    {
        n = 4;
        int [,]dp = new int[n, 4];

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < 4; j++)
            {
                dp[i, j] = -1;
            }
        }

        for (int i = 0; i < n; i++)
        {

            // Base condition:
            // 2^(i+1) because of 0 indexing
            dp[i,3] = (1 << (i + 1));
        }
        Console.Write(solve(n - 1, 0, dp));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

    var n;

    // Function to return the count
    // of required strings
    function solve(i , x , dp)
    {
        if (i < 0) {
            return x == 3 ? 1 : 0;
        }
        if (dp[i][x] != -1) {
            return dp[i][x];
        }

        // '0' at ith position
        dp[i][x] = solve(i - 1, 0, dp);

        // '1' at ith position
        dp[i][x] += solve(i - 1, x + 1, dp);
        return dp[i][x];
    }

    // Driver code

        n = 4;
        var dp = Array(n).fill().map(()=>Array(4).fill(0));

        for (i = 0; i < n; i++) {
            for (j = 0; j < 4; j++) {
                dp[i][j] = -1;
            }
        }

        for (i = 0; i < n; i++) {

            // Base condition:
            // 2^(i+1) because of 0 indexing
            dp[i][3] = (1 << (i + 1));
        }
        document.write(solve(n - 1, 0, dp));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】空间复杂度: O(N)