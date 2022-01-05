# 检查是否可以将一个字符串转换成另一个

> 原文:[https://www . geesforgeks . org/check-可能-transform-one-string-other/](https://www.geeksforgeeks.org/check-possible-transform-one-string-another/)

给定两个字符串 s1 和 s2(大写字母)。通过执行以下操作，检查是否可以将 s1 转换为 s2。

> 1.把一些小写字母变成大写。
> 2。删除所有小写字母。

**示例:**

```
Input : s1 = daBcd s2 = ABC 
Output : yes
Explanation : daBcd -> dABCd -> ABC  
Convert a and b at index 1 and 3 to 
upper case, delete the rest those are 
lowercase. We get the string s2\. 

Input : s1 = argaju    s2 = RAJ
Output : yes 
Explanation : argaju -> aRgAJu -> RAJ  
convert index 1, 3 and 4 to uppercase 
and then delete. All lowercase letters

Input : s1 = ABcd s2= BCD 
Output : NO
```

**方法:**
如果可以将 s1 的 1st i 字符转换为 s2 的 j 字符，则让 DP <sub>i，j</sub> 为 1，否则 DP <sub>i，j</sub> =0。近距离观察给了我们两个需要处理的条件。
最初 DP <sub>0，0</sub> =1，如果 DP <sub>i，j</sub> =1，则可以使用以下条件检查下一组。
**1。**如果大写的 s1[i]等于 s2[j]，则可以将 s1 的 i+1 个字符转换为 s2 的 j+1 个字符，因此 **DP <sub>i+1，j+1</sub> =1。**
**2。**如果 s1[i]是小写，则可以删除该元素，因此 i+1 个字符可以转换为 s2 的 j 个字符。因此 **DP <sub>i+1，j</sub> =1。**
如果 **DP <sub>n，m</sub> =1，**则可以通过以下**条件将 s1 转换为 s2。**

以下是上述方法的 CPP 说明。

## C++

```
// cpp program to check if a string can
// be converted to another string by
// performing operations
#include <bits/stdc++.h>
using namespace std;

// function to check if a string can be
// converted to  another string by
// performing following operations
bool check(string s1, string s2)
{
    // calculates length
    int n = s1.length();
    int m = s2.length();

    bool dp[n + 1][m + 1];
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= m; j++) {
            dp[i][j] = false;
        }
    }
    // mark 1st position as true
    dp[0][0] = true;

    // traverse for all DPi, j
    for (int i = 0; i < s1.length(); i++) {
        for (int j = 0; j <= s2.length(); j++) {

            // if possible for to convert i
            // characters of s1 to j characters
            // of s2
            if (dp[i][j]) {

                // if upper_case(s1[i])==s2[j]
                // is same
                if (j < s2.length() &&
                    (toupper(s1[i]) == s2[j]))
                    dp[i + 1][j + 1] = true;

                // if not upper then deletion is
                // possible
                if (!isupper(s1[i]))
                    dp[i + 1][j] = true;
            }
        }
    }

    return (dp[n][m]);
}

// driver code
int main()
{
    string s1 = "daBcd";
    string s2 = "ABC";

    if (check(s1, s2))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string can
// be converted to another string by
// performing operations
import java.io.*;

class GFG {

    // function to check if a string can be
    // converted to another string by
    // performing following operations
    static boolean check(String s1, String s2)
    {
        // calculates length
        int n = s1.length();
        int m = s2.length();

        boolean dp[][]=new boolean[n + 1][m + 1];
        for (int i = 0; i <= n; i++)
        {
            for (int j = 0; j <= m; j++)
            {
                dp[i][j] = false;
            }
        }
        // mark 1st position as true
        dp[0][0] = true;

        // traverse for all DPi, j
        for (int i = 0; i < s1.length(); i++)
        {
            for (int j = 0; j <= s2.length(); j++)
            {

                // if possible for to convert i
                // characters of s1 to j characters
                // of s2
                if (dp[i][j]) {

                    // if upper_case(s1[i])==s2[j]
                    // is same
                    if (j < s2.length() &&
                        (Character.toUpperCase(s1.charAt(i)) == s2.charAt(j)))
                        dp[i + 1][j + 1] = true;

                    // if not upper then deletion is
                    // possible
                    if (!Character.isUpperCase(s1.charAt(i)))
                        dp[i + 1][j] = true;
                }
            }
        }

        return (dp[n][m]);
    }

    // driver code
    public static void main(String args[])
    {
        String s1 = "daBcd";
        String s2 = "ABC";

        if (check(s1, s2))
            System.out.println("YES");
        else
            System.out.println("NO");

    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to check if a string can
# be converted to another string by
# performing operations

# function to check if a string can be
# converted to another string by
# performing following operations
def check(s1,s2):

    # calculates length
    n = len(s1)
    m = len(s2)
    dp=([[False for i in range(m+1)]
       for i in range(n+1)])

    # mark 1st position as true
    dp[0][0] = True

    # traverse for all DPi, j
    for i in range(len(s1)):
        for j in range(len(s2)+1):

            # if possible for to convert i
            # characters of s1 to j characters
            # of s2
            if (dp[i][j]):

                # if upper_case(s1[i])==s2[j]
                # is same
                if ((j < len(s2) and
                   (s1[i].upper()== s2[j]))):
                    dp[i + 1][j + 1] = True

                # if not upper then deletion is
                # possible
                if (s1[i].isupper()==False):
                    dp[i + 1][j] = True
    return (dp[n][m])

# driver code
if __name__=='__main__':

    s1 = "daBcd"
    s2 = "ABC"
    if (check(s1, s2)):
        print("YES")
    else:
        print("NO")

# this code is contributed by
# sahilshelangia
```

## C#

```
// C# program to check if a string can
// be converted to another string by
// performing operations
using System;

class GFG
{

// function to check if a string can be
// converted to another string by
// performing following operations
static bool check(string s1, string s2)
{
    // calculates length
    int n = s1.Length;
    int m = s2.Length;

    bool[,] dp = new bool[n + 1, m + 1];
    for (int i = 0; i <= n; i++)
    {
        for (int j = 0; j <= m; j++)
        {
            dp[i, j] = false;
        }
    }

    // mark 1st position as true
    dp[0, 0] = true;

    // traverse for all DPi, j
    for (int i = 0; i < s1.Length; i++)
    {
        for (int j = 0; j <= s2.Length; j++)
        {

            // if possible for to convert i
            // characters of s1 to j characters
            // of s2
            if (dp[i, j])
            {

                // if upper_case(s1[i])==s2[j]
                // is same
                if (j < s2.Length &&
                    (Char.ToUpper(s1[i]) == s2[j]))
                    dp[i + 1, j + 1] = true;

                // if not upper then deletion is
                // possible
                if (!Char.IsUpper(s1[i]))
                    dp[i + 1, j] = true;
            }
        }
    }

    return (dp[n, m]);
}

// Driver Code
public static void Main()
{
    string s1 = "daBcd";
    string s2 = "ABC";

    if (check(s1, s2))
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

// This code is contributed
// by ChitraNayal
```

## java 描述语言

```
<script>
// Javascript program to check if a string can
// be converted to another string by
// performing operations

    // function to check if a string can be
    // converted to another string by
    // performing following operations
    function check(s1,s2)
    {
        // calculates length
        let n = s1.length;
        let m = s2.length;

        let dp=new Array(n + 1);
        for (let i = 0; i <= n; i++)
        {
            dp[i]=new Array(m+1);
            for (let j = 0; j <= m; j++)
            {
                dp[i][j] = false;
            }
        }
        // mark 1st position as true
        dp[0][0] = true;

        // traverse for all DPi, j
        for (let i = 0; i < s1.length; i++)
        {
            for (let j = 0; j <= s2.length; j++)
            {   

                // if possible for to convert i
                // characters of s1 to j characters
                // of s2
                if (dp[i][j]) {

                    // if upper_case(s1[i])==s2[j]
                    // is same
                    if (j < s2.length &&
                        (s1[i].toUpperCase() == s2[j]))
                        dp[i + 1][j + 1] = true;

                    // if not upper then deletion is
                    // possible

                    if (!(s1[i] == s1[i].toUpperCase()))
                        dp[i + 1][j] = true;
                }
            }
        }

        return (dp[n][m]);
    }

    // driver code
    let s1 = "daBcd";
    let s2 = "ABC";
    if (check(s1, s2))
        document.write("YES");
    else
        document.write("NO");

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
YES
```