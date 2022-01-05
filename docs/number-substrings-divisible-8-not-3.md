# 可被 8 整除但不能被 3 整除的子串数量

> 原文:[https://www . geesforgeks . org/number-substrings-除尽-8-not-3/](https://www.geeksforgeeks.org/number-substrings-divisible-8-not-3/)

给定一串数字“0-9”。任务是找出可被 8 整除但不能被 3 整除的子串的数量。

**示例:**

```
Input : str = "888"
Output : 5
Substring indexes : (1, 1), (1, 2), (2, 2), 
                            (2, 3), (3, 3).

Input : str = "6564525600"
Output : 15

```

如果一个数的总和能被 3 整除，这个数就能被 3 整除。如果最后三个数字能被 8 整除，这个数就能被 8 整除。

现在，想法是存储字符串的前缀和，即前缀计数，使得前缀模 3 的数字之和为 0、1、2。接下来，我们遍历字符串，对于每个位置 I，计算以 I 结尾且可被 8 整除的子字符串的数量。从这个值中，我们减去以 I 结尾并可被 3 整除的子串的数量。

我们定义一个|S| X 3 大小的 2D 数组，|S|是字符串的大小，比如 dp[i][j]。
dp[i][j]可以被定义为在任何索引 I 处，当来自索引 0 数字被加到索引 I 并取模 3 时，从索引 0 开始到具有输出 j 的索引 I 的子串的数目
。因此 0 < = j < = 2，因为取模 3。

现在，我们将遍历字符串，检查每个可被 8 整除的一位数、两位数和三位数。

对于一个数字，只需检查索引处的字符是否为 8。
两位数，检查是否能被 8 整除，不能被 3 整除。
三位数字，组成数字，检查是否能被 8 整除。如果这个数可以被整除，那么最后三个数字必须能被 8 整除。所以在这个索引处结束的所有子串必须能被 8 整除，即(i-3)个子串。
但是它也将包含那些可被 3 整除的子串，所以简单地用 dp[i][j]移除它们。

## C/C++

```
// CPP Program to count substrings which are
// divisible by 8 but not by 3
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000

// Returns count of substrings divisible by 8
// but not by 3.
int count(char s[], int len)
{
    int cur = 0, dig = 0;
    int sum[MAX], dp[MAX][3];

    memset(sum, 0, sizeof(sum));
    memset(dp, 0, sizeof(dp));

    dp[0][0] = 1;

    // Iterating the string.
    for (int i = 1; i <= len; i++)
    {
        dig = int(s[i-1])-48;
        cur += dig;
        cur %= 3;

        sum[i] = cur;

        // Prefix sum of number of substrings whose
        // sum of digits mudolo 3 is 0, 1, 2.
        dp[i][0] = dp[i-1][0];
        dp[i][1] = dp[i-1][1];
        dp[i][2] = dp[i-1][2];

        dp[i][sum[i]]++;
    }

    int ans = 0, dprev = 0, value = 0, dprev2 = 0;

    // Iterating the string.
    for (int i = 1; i <= len; i++)
    {
        dig = int(s[i-1])-48;

        // Since single digit 8 is divisible
        // by 8 and not by 3.
        if (dig == 8)
            ans++;

        // Taking two digit number.
        if (i-2 >= 0)
        {
            dprev = int(s[i-2])-48;  // 10th position
            value = dprev*10 + dig;  // Complete 2 digit
                                     // number

            if ((value%8 == 0) && (value%3 != 0))
                ans++;
        }

        // Taking 3 digit number.
        if (i-3 >= 0)
        {
            dprev2 = int(s[i-3])-48; // 100th position
            dprev  = int(s[i-2])-48;  // 10th position

            // Complete 3 digit number.
            value = dprev2*100 + dprev*10 + dig;

            if (value%8 != 0)
                continue;

            // If number formed is divisible by 8 then
            // last 3 digits are  also divisible by 8.
            // Then all the substring ending at this
            // index is divisible.
            ans += (i-2);

            // But those substring also contain number
            // which are not divisible by 3 so
            // remove them.
            ans -= (dp[i-3][sum[i]]);
        }
    }

    return ans;
}

// Driven Program
int main()
{
    char str[] = "6564525600";
    int len = strlen(str);
    cout << count(str, len) <<endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count substrings which are
// divisible by 8 but not by 3
import java.io.*;

class GFG 
{
    // Function that returns count of substrings divisible by 8
    // but not by 3
    static int count(String s, int len)
    {
        int MAX = 1000;
        int cur = 0, dig = 0;
        int[] sum = new int[MAX];
        int[][] dp = new int[MAX][3];

        dp[0][0] = 1;

        // Iterating the string.
        for (int i = 1; i <= len; i++)
        {
            dig = (int)(s.charAt(i-1)) - 48;
            cur += dig;
            cur %= 3;

            sum[i] = cur;

            // Prefix sum of number of substrings whose
            // sum of digits mudolo 3 is 0, 1, 2.
            dp[i][0] = dp[i-1][0];
            dp[i][1] = dp[i-1][1];
            dp[i][2] = dp[i-1][2];

            dp[i][sum[i]]++;
        }

        int ans = 0, dprev = 0, value = 0, dprev2 = 0;

        // Iterating the string.
        for (int i = 1; i <= len; i++)
        {
            dig = (int)(s.charAt(i-1)) - 48;

            // Since single digit 8 is divisible
            // by 8 and not by 3.
            if (dig == 8)
                ans++;

            // Taking two digit number.
            if (i-2 >= 0)
            {
                dprev = (int)(s.charAt(i-2)) - 48;  // 10th position
                value = dprev*10 + dig;  // Complete 2 digit
                                     // number

                if ((value%8 == 0) && (value%3 != 0))
                    ans++;
            }

            // Taking 3 digit number.
            if (i-3 >= 0)
            {
                dprev2 = (int)(s.charAt(i-3)) - 48; // 100th position
                dprev  = (int)(s.charAt(i-2)) - 48;  // 10th position

                // Complete 3 digit number.
                value = dprev2*100 + dprev*10 + dig;

                if (value%8 != 0)
                    continue;

                // If number formed is divisible by 8 then
                // last 3 digits are  also divisible by 8.
                // Then all the substring ending at this
                // index is divisible.
                ans += (i-2);

                // But those substring also contain number
                // which are not divisible by 3 so
                // remove them.
                ans -= (dp[i-3][sum[i]]);
            }
        }

        return ans;
    }

    // driver program
    public static void main (String[] args) 
    {
        String str = "6564525600";
        int len = str.length();
        System.out.println(count(str, len));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 Program to count substrings 
# which are divisible by 8 but not by 3 

# Returns count of substrings 
# divisible by 8 but not by 3. 
def count(s, Len):
    global MAX
    cur = 0
    dig = 0
    Sum = [0] * MAX
    dp = [[0, 0, 0] for i in range(MAX)] 

    dp[0][0] = 1

    # Iterating the string.
    for i in range(1, Len + 1):
        dig = int(s[i - 1]) - 48
        cur += dig 
        cur %= 3

        Sum[i] = cur 

        # Prefix sum of number of substrings 
        # whose sum of digits mudolo 3 is
        # 0, 1, 2. 
        dp[i][0] = dp[i - 1][0] 
        dp[i][1] = dp[i - 1][1] 
        dp[i][2] = dp[i - 1][2] 

        dp[i][Sum[i]] += 1

    ans = 0
    dprev = 0
    value = 0
    dprev2 = 0

    # Iterating the string. 
    for i in range(1, Len + 1):
        dig = int(s[i - 1]) - 48

        # Since single digit 8 is 
        # divisible by 8 and not by 3. 
        if dig == 8: 
            ans += 1

        # Taking two digit number. 
        if i - 2 >= 0:
            dprev = int(s[i - 2]) - 48 # 10th position 
            value = dprev * 10 + dig   # Complete 2 digit 
                                       # number 

            if (value % 8 == 0) and (value % 3 != 0): 
                ans += 1

        # Taking 3 digit number. 
        if i - 3 >= 0:
            dprev2 = int(s[i - 3]) - 48 # 100th position 
            dprev = int(s[i - 2]) - 48 # 10th position 

            # Complete 3 digit number. 
            value = (dprev2 * 100 +
                     dprev * 10 + dig)

            if value % 8 != 0:
                continue

            # If number formed is divisible by 8 
            # then last 3 digits are also divisible 
            # by 8\. Then all the substring ending 
            # at this index are divisible. 
            ans += (i - 2) 

            # But those substring also contain 
            # number which are not divisible 
            # by 3 so remove them. 
            ans -= (dp[i - 3][Sum[i]])

    return ans

# Driver Code 
MAX = 1000
Str = "6564525600"
Len = len(Str) 
print(count(Str, Len))

# This code is contributed 
# by PranchalK
```

## C#

```
// C# program to count substrings which are
// divisible by 8 but not by 3
using System;

class GFG 
{
    // Function that returns count of substrings 
    // divisible by 8 but not by 3
    static int count(String s, int len)
    {
        int MAX = 1000;
        int cur = 0, dig = 0;
        int[] sum = new int[MAX];
        int[,] dp = new int[MAX,3];

        dp[0, 0] = 1;

        // Iterating the string.
        for (int i = 1; i <= len; i++)
        {
            dig = (int)(s[i-1]) - 48;
            cur += dig;
            cur %= 3;

            sum[i] = cur;

            // Prefix sum of number of substrings whose
            // sum of digits mudolo 3 is 0, 1, 2.
            dp[i, 0] = dp[i-1, 0];
            dp[i, 1] = dp[i-1, 1];
            dp[i, 2] = dp[i-1, 2];

            dp[i, sum[i]]++;
        }

        int ans = 0, dprev = 0, value = 0, dprev2 = 0;

        // Iterating the string.
        for (int i = 1; i <= len; i++)
        {
            dig = (int)(s[i-1]) - 48;

            // Since single digit 8 is divisible
            // by 8 and not by 3.
            if (dig == 8)
                ans++;

            // Taking two digit number.
            if (i-2 >= 0)
            {
                dprev = (int)(s[i-2]) - 48; // 10th position
                value = dprev*10 + dig;     // Complete 2 digit number

                if ((value % 8 == 0) && (value % 3 != 0))
                    ans++;
            }

            // Taking 3 digit number.
            if (i - 3 >= 0)
            {
                dprev2 = (int)(s[i-3]) - 48; // 100th position
                dprev = (int)(s[i-2]) - 48; // 10th position

                // Complete 3 digit number.
                value = dprev2 * 100 + dprev * 10 + dig;

                if (value % 8 != 0)
                    continue;

                // If number formed is divisible by 8 then
                // last 3 digits are also divisible by 8.
                // Then all the substring ending at this
                // index is divisible.
                ans += (i - 2);

                // But those substring also contain number
                // which are not divisible by 3 so
                // remove them.
                ans -= (dp[i - 3,sum[i]]);
            }
        }

        return ans;
    }

    // driver program
    public static void Main (String[] args) 
    {
        String str = "6564525600";
        int len = str.Length;
        Console.Write(count(str, len));
    }
}

// This code is contributed by parashar.
```

输出:

```
15

```

本文由供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。