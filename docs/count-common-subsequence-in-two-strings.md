# 计算两个字符串中的公共子序列

> 原文:[https://www . geesforgeks . org/count-common-subsequence-in-two-string/](https://www.geeksforgeeks.org/count-common-subsequence-in-two-strings/)

给定两根弦 **S** 和 **Q** 。任务是统计 S 和 t 中公共子序列的个数。

**示例:**

> 输入:S = "ajblqcpdz "，T = "aefcnbtdi"
> 输出:11
> 常见的子序列有:{“a”、“b”、“c”、“d”、“ab”、“bd”、“ad”、“ac”、“cd”、“abd”、“ACD”}
> 
> 输入:S =“a”，T =“ab”
> 输出:1

为了找到两个字符串(比如 S 和 T)中公共子序列的数量，我们通过定义一个 2D 数组 **dp[][]** ，使用动态编程，其中 dp[i][j]是字符串 S[0…i-1]和 T[0…]中公共子序列的数量。j-1]。
现在，我们可以将 dp[i][j]定义为
= dp[i][j-1] + dp[i-1][j] + 1，当 S[i-1]等于 T[j-1]
时，这是因为当 S[i-1] == S[j-1]时，利用上述事实，所有先前的公共子序列在被追加一个字符时会加倍。dp[i][j-1]和 dp[i-1][j]都包含 dp[i-1][j-1],因此在我们的递归中它被添加了两次，这使得所有先前的公共子序列的计数加倍。递归中加 1 是为了最新的字符匹配:由 s1[i-1]和 s2[j-1]
组成的公共子序列= dp[i-1][j]+dp[i][j-1]–dp[i-1][j-1]，当 S[i-1]不等于 T[j-1]
时，这里我们减去 DP[I-1][j-1]一次，因为它同时存在于 DP[I][j-1]和 DP[I-1][j]中，并且被加了两次。

下面是该方法的实现:

## C++

```
// C++ program to count common subsequence in two strings
#include <bits/stdc++.h>
using namespace std;

// return the number of common subsequence in
// two strings
int CommomSubsequencesCount(string s, string t)
{
    int n1 = s.length();
    int n2 = t.length();
    int dp[n1+1][n2+1];

    for (int i = 0; i <= n1; i++) {
        for (int j = 0; j <= n2; j++) {
            dp[i][j] = 0;
        }
    }

    // for each character of S
    for (int i = 1; i <= n1; i++) {

        // for each character in T
        for (int j = 1; j <= n2; j++) {

            // if character are same in both
            // the string
            if (s[i - 1] == t[j - 1])
                dp[i][j] = 1 + dp[i][j - 1] + dp[i - 1][j];           
            else
                dp[i][j] = dp[i][j - 1] + dp[i - 1][j] -
                                        dp[i - 1][j - 1];           
        }
    }

    return dp[n1][n2];
}

// Driver Program
int main()
{
    string s = "ajblqcpdz";
    string t = "aefcnbtdi";

    cout << CommomSubsequencesCount(s, t) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count common subsequence in two strings
public class GFG {

    // return the number of common subsequence in
    // two strings
    static int CommomSubsequencesCount(String s, String t)
    {
        int n1 = s.length();
        int n2 = t.length();
        int dp[][] = new int [n1+1][n2+1];
        char ch1,ch2 ;

        for (int i = 0; i <= n1; i++) {
            for (int j = 0; j <= n2; j++) {
                dp[i][j] = 0;
            }
        }

        // for each character of S
        for (int i = 1; i <= n1; i++) {

            // for each character in T
            for (int j = 1; j <= n2; j++) {

                ch1 = s.charAt(i - 1);
                ch2 = t.charAt(j - 1);

                // if character are same in both 
                // the string                
                if (ch1 == ch2) 
                    dp[i][j] = 1 + dp[i][j - 1] + dp[i - 1][j];            
                else
                    dp[i][j] = dp[i][j - 1] + dp[i - 1][j] - 
                                            dp[i - 1][j - 1];            
            }
        }

        return dp[n1][n2];
    }
    // Driver code
    public static void main (String args[]){

          String s = "ajblqcpdz";
          String t = "aefcnbtdi";

        System.out.println(CommomSubsequencesCount(s, t));

    }

// This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 program to count common
# subsequence in two strings

# return the number of common subsequence
# in two strings
def CommomSubsequencesCount(s, t):

    n1 = len(s)
    n2 = len(t)
    dp = [[0 for i in range(n2 + 1)]
             for i in range(n1 + 1)]

    # for each character of S
    for i in range(1, n1 + 1):

        # for each character in T
        for j in range(1, n2 + 1):

            # if character are same in both
            # the string
            if (s[i - 1] == t[j - 1]):
                dp[i][j] = (1 + dp[i][j - 1] +
                                dp[i - 1][j])        
            else:
                dp[i][j] = (dp[i][j - 1] + dp[i - 1][j] -
                            dp[i - 1][j - 1])        

    return dp[n1][n2]

# Driver Code
s = "ajblqcpdz"
t = "aefcnbtdi"

print(CommomSubsequencesCount(s, t))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to count common
// subsequence in two strings
using System;

class GFG
{

// return the number of common
// subsequence in two strings
static int CommomSubsequencesCount(string s,
                                   string t)
{
    int n1 = s.Length;
    int n2 = t.Length;
    int[,] dp = new int [n1 + 1, n2 + 1];

    for (int i = 0; i <= n1; i++)
    {
        for (int j = 0; j <= n2; j++)
        {
            dp[i, j] = 0;
        }
    }

    // for each character of S
    for (int i = 1; i <= n1; i++)
    {

        // for each character in T
        for (int j = 1; j <= n2; j++)
        {

            // if character are same in
            // both the string                
            if (s[i - 1] == t[j - 1])
                dp[i, j] = 1 + dp[i, j - 1] +
                               dp[i - 1, j];            
            else
                dp[i, j] = dp[i, j - 1] +
                           dp[i - 1, j] -
                           dp[i - 1, j - 1];            
        }
    }

    return dp[n1, n2];
}

// Driver code
public static void Main ()
{
    string s = "ajblqcpdz";
    string t = "aefcnbtdi";

    Console.Write(CommomSubsequencesCount(s, t));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count common subsequence
// in two strings

// return the number of common subsequence
// in two strings
function CommomSubsequencesCount($s, $t)
{
    $n1 = strlen($s);
    $n2 = strlen($t);
    $dp = array();

    for ($i = 0; $i <= $n1; $i++)
    {
        for ($j = 0; $j <= $n2; $j++)
        {
            $dp[$i][$j] = 0;
        }
    }

    // for each character of S
    for ($i = 1; $i <= $n1; $i++)
    {

        // for each character in T
        for ($j = 1; $j <= $n2; $j++)
        {

            // if character are same in both
            // the string
            if ($s[$i - 1] == $t[$j - 1])
                $dp[$i][$j] = 1 + $dp[$i][$j - 1] +
                                  $dp[$i - 1][$j];    
            else
                $dp[$i][$j] = $dp[$i][$j - 1] +
                              $dp[$i - 1][$j] -
                              $dp[$i - 1][$j - 1];    
        }
    }

    return $dp[$n1][$n2];
}

// Driver Code
$s = "ajblqcpdz";
$t = "aefcnbtdi";

echo CommomSubsequencesCount($s, $t) ."\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to count common subsequence in two strings

// return the number of common subsequence in
// two strings
function CommomSubsequencesCount(s, t)
{
    var n1 = s.length;
    var n2 = t.length;
    var dp = Array.from(Array(n1+1), ()=> Array(n2+1));

    for (var i = 0; i <= n1; i++) {
        for (var j = 0; j <= n2; j++) {
            dp[i][j] = 0;
        }
    }

    // for each character of S
    for (var i = 1; i <= n1; i++) {

        // for each character in T
        for (var j = 1; j <= n2; j++) {

            // if character are same in both
            // the string
            if (s[i - 1] == t[j - 1])
                dp[i][j] = 1 + dp[i][j - 1] + dp[i - 1][j];           
            else
                dp[i][j] = dp[i][j - 1] + dp[i - 1][j] -
                                        dp[i - 1][j - 1];           
        }
    }

    return dp[n1][n2];
}

// Driver Program
var s = "ajblqcpdz";
var t = "aefcnbtdi";
document.write( CommomSubsequencesCount(s, t));

</script>
```

**Output:** 

```
11
```

**时间复杂度:**O(n1 * N2)
T3】辅助空间: O(n1 * n2)
**来源:** [StackOverflow](https://stackoverflow.com/questions/31065929/number-of-common-sub-sequences-of-two-strings)