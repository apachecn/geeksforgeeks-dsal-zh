# 检查字符串是否相隔 k 距离

> 原文:[https://www . geesforgeks . org/check-when-strings-k-distance-not/](https://www.geeksforgeeks.org/check-whether-strings-k-distance-apart-not/)

给定两个字符串，任务是找出它们之间的编辑距离是否仅小于或等于 k。这意味着当只有 k 个不匹配时，字符串之间只有 k 个编辑距离。
如果有小于或等于 k 的不匹配，则打印是，否则打印否
此外，如果两个字符串已经相同，则打印是。

**示例:**

```
Input :  str1 = "geeksforgeeks"    
         str2 = "geeksforgeek" 
         k = 1
Output :  Yes
Explanation: Only one character is mismatched 
             or to be removed i.e. s at last 

Input :  str1 = "nishant"  
         str2 = "nisha"   
         k = 1
Output :  No     
Explanation: 2 characters need to be removed
             i.e. n and t 

Input :  str1 = "practice"    
         str2 = "prac" 
         k = 3
Output :  No
Explanation: 4 characters are mismatched or to
             be removed i.e. t, i, c, e at last i.e. > k

Input :  str1 = "Ping"  str2 = "Paging"   k = 2
Output :  Yes   
Explanation: 2 characters need to be removed or 
            mismatched i.e. a and g in paging 
```

**算法:**
1-检查两个字符串的长度差是否大于 k，如果是，返回 false。
2-找到两个字符串的[编辑距离](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/)。如果编辑距离小于或等于 k，则返回 true。否则返回 false。

## C++

```
// A Dynamic Programming based C++ program to
// find minimum number operations is less than
// or equal to k or not to convert str1 to str2
#include <bits/stdc++.h>
using namespace std;

// Utility function to find minimum of three numbers
int min(int x, int y, int z)
{
    return min(min(x, y), z);
}

int editDistDP(string str1, string str2, int m, int n)
{
    // Create a table to store results of subproblems
    int dp[m + 1][n + 1];

    // Fill d[][] in bottom up manner
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            // If first string is empty, only option is to
            // insert all characters of second string
            if (i == 0)
                dp[i][j] = j; // Min. operations = j

            // If second string is empty, only option is to
            // remove all characters of second string
            else if (j == 0)
                dp[i][j] = i; // Min. operations = i

            // If last characters are same, ignore last char
            // and recur for remaining string
            else if (str1[i - 1] == str2[j - 1])
                dp[i][j] = dp[i - 1][j - 1];

            // If last character are different, consider all
            // possibilities and find minimum
            else
                dp[i][j] = 1 + min(dp[i][j - 1], // Insert
                                   dp[i - 1][j], // Remove
                                   dp[i - 1][j - 1]); // Replace
        }
    }

    return dp[m][n];
}

// Returns true if str1 and str2 are k edit distance apart,
// else false.
bool areKDistant(string str1, string str2, int k)
{
    int m = str1.length();
    int n = str2.length();

    if (abs(m - n) > k)
        return false;

    return (editDistDP(str1, str2, m, n) <= k);
}

// Driver program
int main()
{
    // your code goes here
    string str1 = "geek";
    string str2 = "gks";
    int k = 3;

    areKDistant(str1, str2, k) ? cout << "Yes" : cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based Java program to
// find minimum number operations is less than
// or equal to k or not to convert str1 to str2
class GFG {

    // Utility function to find minimum
    // of three numbers
    static int min(int x, int y, int z)
    {
        return Math.min(Math.min(x, y), z);
    }

    static int editDistDP(String str1, String str2,
                          int m, int n)
    {
        // Create a table to store
        // results of subproblems
        int dp[][] = new int[m + 1][n + 1];

        // Fill d[][] in bottom up manner
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                // If first string is empty,
                // only option is to insert
                // all characters of second string
                if (i == 0)
                    dp[i][j] = j; // Min. operations = j

                // If second string is empty,
                // only option is to remove
                // all characters of second string
                else if (j == 0)
                    dp[i][j] = i; // Min. operations = i

                // If last characters are same,
                // ignore last char and recur
                // for remaining string
                else if (str1.charAt(i - 1) == str2.charAt(j - 1))
                    dp[i][j] = dp[i - 1][j - 1];

                // If last character are different,
                // consider all possibilities
                // and find minimum
                else
                    dp[i][j] = 1 + min(dp[i][j - 1], // Insert
                                       dp[i - 1][j], // Remove
                                       dp[i - 1][j - 1]); // Replace
            }
        }

        return dp[m][n];
    }

    // Returns true if str1 and str2 are
    // k edit distance apart, else false.
    static boolean areKDistant(String str1, String str2,
                               int k)
    {
        int m = str1.length();
        int n = str2.length();

        if (Math.abs(m - n) > k)
            return false;

        return (editDistDP(str1, str2, m, n) <= k);
    }

    // driver code
    public static void main(String[] args)
    {
        String str1 = "geek";
        String str2 = "gks";
        int k = 3;

        if (areKDistant(str1, str2, k))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# A Dynamic Programming based Python3 program to
# find minimum number operations is less than
# or equal to k or not to convert str1 to str2

# Utility function to find minimum
# of three numbers
def minn(x, y, z) :

    return min(min(x, y), z)

def editDistDP(str1, str2, m, n) :

    # Create a table to store results
    # of subproblems
    dp = [[0 for i in range(n + 1)]
             for j in range(m + 1)]

    # Fill d[][] in bottom up manner
    for i in range(m + 1):
        for j in range(n + 1):

            # If first is empty, only option is
            # to insert all characters of second
            if (i == 0) :
                dp[i][j] = j # Min. operations = j

            # If second is empty, only option is
            # to remove all characters of second
            elif (j == 0):
                dp[i][j] = i # Min. operations = i

            # If last characters are same,
            # ignore last char and recur
            # for remaining
            elif (str1[i - 1] == str2[j - 1]):
                dp[i][j] = dp[i - 1][j - 1]

            # If last character are different,
            # consider all possibilities and
            # find minimum
            else:
                dp[i][j] = 1 + minn(dp[i][j - 1], # Insert
                                    dp[i - 1][j], # Remove
                                    dp[i - 1][j - 1]) # Replace

    return dp[m][n]

# Returns true if str1 and str2 are
# k edit distance apart, else false.
def areKDistant(str1, str2, k):

    m = len(str1)
    n = len(str2)

    if (abs(m - n) > k) :
        return False

    return (editDistDP(str1, str2,
                       m, n) <= k)

# Driver Code
if __name__ == '__main__':

    str1 = "geek"
    str2 = "gks"
    k = 3
    if areKDistant(str1, str2, k):
        print("Yes") 
    else:
        print("No")

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// A Dynamic Programming based C#
// program to find minimum number
// operations is less than or equal
// to k or not to convert str1 to str2
using System;

class GFG
{

// Utility function to find minimum
// of three numbers
static int min(int x, int y, int z)
{
    return Math.Min(Math.Min(x, y), z);
}

static int editDistDP(string str1, string str2,
                      int m, int n)
{

    // Create a table to store
    // results of subproblems
    int [,]dp = new int[m + 1, n + 1];

    // Fill d[][] in bottom up manner
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {

            // If first string is empty,
            // only option is to insert
            // all characters of second string
            if (i == 0)

                // Min. operations = j
                dp[i, j] = j;

            // If second string is empty,
            // only option is to remove
            // all characters of second string
            else if (j == 0)

                 // Min. operations = i
                dp[i, j] = i;

            // If last characters are same,
            // ignore last char and recur
            // for remaining string
            else if (str1[i - 1] == str2[j - 1])
                dp[i, j] = dp[i - 1,j - 1];

            // If last character are different,
            // consider all possibilities
            // and find minimum
            else
                dp[i, j] = 1 + min(dp[i, j - 1], // Insert
                                    dp[i - 1, j], // Remove
                                   dp[i - 1, j - 1]); // Replace
        }
    }

    return dp[m, n];
}

// Returns true if str1 and str2 are
// k edit distance apart, else false.
static bool areKDistant(string str1, string str2,
                        int k)
{
    int m = str1.Length;
    int n = str2.Length;

    if (Math.Abs(m - n) > k)
        return false;

    return (editDistDP(str1, str2, m, n) <= k);
}

// Driver Code
public static void Main ()
{
    string str1 = "geek";
    string str2 = "gks";
    int k = 3;

    if(areKDistant(str1, str2, k))
    Console.WriteLine("Yes");
    else
    Console.WriteLine("No");
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming based
// PHP program to find minimum
// number operations is less
// than or equal to k or not
// to convert str1 to str2

// Utility function to find
// minimum of three numbers
function minn($x, $y, $z)
{
    return min(minn($x, $y), $z);
}

function editDistDP($str1, $str2, $m, $n)
{
    // Create a table to store
    // results of subproblems
    $dp[$m + 1][$n + 1] = 0;

    // Fill d[][] in bottom up manner
    for ($i = 0; $i <= $m; $i++)
    {
        for ($j = 0; $j <= $n; $j++)
        {
            // If first string is empty,
            // only option is to insert
            // all characters of second string
            if ($i == 0)

                // Min. operations = j
                $dp[$i][$j] = $j;

            // If second string is empty,
            // only option is to remove all
            // characters of second string
            else if ($j == 0)

                // Min. operations = i
                $dp[$i][$j] = $i;

            // If last characters are same,
            // ignore last char and recur
            // for remaining string
            else if ($str1[$i - 1] == $str2[$j - 1])
                $dp[$i][$j] = $dp[$i - 1][$j - 1];

            // If last character are different,
            // consider all possibilities and
            // find minimum
            else
                                // Insert        
                $dp[$i][$j] = 1 + min($dp[$i][$j - 1],
                                // Remove
                                $dp[$i - 1][$j],
                                // Replace
                                $dp[$i - 1][$j - 1]);
        }
    }

    return $dp[$m][$n];
}

// Returns true if str1 and
// str2 are k edit distance
// apart, else false.
function areKDistant($str1, $str2, $k)
{
    $m = strlen($str1);
    $n = strlen($str2);

    if (abs($m - $n) > $k)
        return false;

    return (editDistDP($str1, $str2,
                       $m, $n) <= $k);
}

// Driver Code
$str1 = "geek";
$str2 = "gks";
$k = 3;

if(areKDistant($str1, $str2, $k))
echo"Yes" ;
else
echo "No";

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // A Dynamic Programming based Javascript program to
    // find minimum number operations is less than
    // or equal to k or not to convert str1 to str2

    // Utility function to find minimum
    // of three numbers
    function min(x, y, z)
    {
        return Math.min(Math.min(x, y), z);
    }

    function editDistDP(str1, str2, m, n)
    {
        // Create a table to store
        // results of subproblems
        let dp = new Array(m + 1);

        // Fill d[][] in bottom up manner
        for (let i = 0; i <= m; i++) {
            dp[i] = new Array(n + 1);
            for (let j = 0; j <= n; j++) {
                // If first string is empty,
                // only option is to insert
                // all characters of second string
                if (i == 0)
                    dp[i][j] = j; // Min. operations = j

                // If second string is empty,
                // only option is to remove
                // all characters of second string
                else if (j == 0)
                    dp[i][j] = i; // Min. operations = i

                // If last characters are same,
                // ignore last char and recur
                // for remaining string
                else if (str1[i - 1] == str2[j - 1])
                    dp[i][j] = dp[i - 1][j - 1];

                // If last character are different,
                // consider all possibilities
                // and find minimum
                else
                    dp[i][j] = 1 + min(dp[i][j - 1], // Insert
                                       dp[i - 1][j], // Remove
                                       dp[i - 1][j - 1]); // Replace
            }
        }

        return dp[m][n];
    }

    // Returns true if str1 and str2 are
    // k edit distance apart, else false.
    function areKDistant(str1, str2, k)
    {
        let m = str1.length;
        let n = str2.length;

        if (Math.abs(m - n) > k)
            return false;

        return (editDistDP(str1, str2, m, n) <= k);
    }

    let str1 = "geek";
    let str2 = "gks";
    let k = 3;

    if (areKDistant(str1, str2, k))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**输出:**

```
Yes
```

本文由 [**萨希尔·查布拉(akku)**](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。