# 重复删除回文子串后删除字符串的最少步骤

> 原文:[https://www . geeksforgeeks . org/重复删除回文子字符串后删除字符串的最少步骤/](https://www.geeksforgeeks.org/minimum-steps-to-delete-a-string-after-repeated-deletion-of-palindrome-substrings/)

给定一个只包含整数字符的字符串。我们需要在最少的步骤中删除这个字符串的所有字符，其中一步我们可以删除作为回文的子字符串。删除子串后，剩下的部分被连接起来。

**示例:**

```
Input : s = “2553432”
Output : 2
We can delete all character of above string in
2 steps, first deleting the substring s[3, 5] “343”  
and then remaining string completely  s[0, 3] “2552”

Input : s = “1234”
Output : 4
We can delete all character of above string in 4 
steps only because each character need to be deleted 
separately. No substring of length 2 is a palindrome 
in above string.
```

我们可以用动态规划来解决这个问题。让 dp[i][j]表示删除子串 s[i，j]所需的步骤数。每个字符将被单独删除或作为某个子串的一部分删除，因此在第一种情况下，我们将删除字符本身并调用子问题(i+1，j)。在第二种情况下，我们将迭代右侧当前字符的全部出现，如果 K 是一个这样的出现的索引，那么问题将减少到两个子问题(i+1，K–1)和(K+1，j)。我们可以到达这个子问题(i+1，K-1)，因为我们可以删除相同的字符并调用中间子串。我们需要处理前两个字符相同的情况，在这种情况下，我们可以直接简化为子问题(i+2，j)。
那么在上面讨论了子问题之间的关系之后，我们可以把 dp 关系写成如下:

```
dp[i][j] = min(1 + dp[i+1][j],
          dp[i+1][K-1] + dp[K+1][j],  where s[i] == s[K]
          1 + dp[i+2][j] )
```

上述解决方案的总时间复杂度是 O(n^3)

## C++

```
//  C++ program to find minimum step to delete a string
#include <bits/stdc++.h>
using namespace std;

/* method returns minimum step for deleting the string,
   where in one step a palindrome is removed */
int minStepToDeleteString(string str)
{
    int N = str.length();

    //  declare dp array and initialize it with 0s
    int dp[N + 1][N + 1];
    for (int i = 0; i <= N; i++)
        for (int j = 0; j <= N; j++)
            dp[i][j] = 0;

    // loop for substring length we are considering
    for (int len = 1; len <= N; len++)
    {
        // loop with two variables i and j, denoting
        // starting and ending of substrings
        for (int i = 0, j = len - 1; j < N; i++, j++)
        {
            // If substring length is 1, then 1 step
            // will be needed
            if (len == 1)
                dp[i][j] = 1;
            else
            {
                // delete the ith char individually
                // and assign result for subproblem (i+1,j)
                dp[i][j] = 1 + dp[i + 1][j];

                // if current and next char are same,
                // choose min from current and subproblem
                // (i+2,j)
                if (str[i] == str[i + 1])
                    dp[i][j] = min(1 + dp[i + 2][j], dp[i][j]);

                /*  loop over all right characters and suppose
                    Kth char is same as ith character then
                    choose minimum from current and two
                    substring after ignoring ith and Kth char */
                for (int K = i + 2; K <= j; K++)
                    if (str[i] == str[K])
                        dp[i][j] = min(dp[i+1][K-1] + dp[K+1][j],
                                                       dp[i][j]);
            }
        }
    }

    /* Uncomment below snippet to print actual dp tablex
    for (int i = 0; i < N; i++, cout << endl)
        for (int j = 0; j < N; j++)
            cout << dp[i][j] << " ";    */

    return dp[0][N - 1];
}

//  Driver code to test above methods
int main()
{
    string str = "2553432";
    cout << minStepToDeleteString(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum step to
// delete a string
public class GFG
{                           
    /* method returns minimum step for deleting
       the string, where in one step a
       palindrome is removed
     */
    static int minStepToDeleteString(String str) {
        int N = str.length();

        // declare dp array and initialize it with 0s
        int[][] dp = new int[N + 1][N + 1];
        for (int i = 0; i <= N; i++)
            for (int j = 0; j <= N; j++)
                dp[i][j] = 0;

        // loop for substring length we are considering
        for (int len = 1; len <= N; len++) {

            // loop with two variables i and j, denoting
            // starting and ending of substrings
            for (int i = 0, j = len - 1; j < N; i++, j++) {

                // If substring length is 1, then 1 step
                // will be needed
                if (len == 1)
                    dp[i][j] = 1;

                else {
                    // delete the ith char individually
                    // and assign result for
                    // subproblem (i+1,j)
                    dp[i][j] = 1 + dp[i + 1][j];

                    // if current and next char are same,
                    // choose min from current and
                    // subproblem (i+2, j)
                    if (str.charAt(i) == str.charAt(i + 1))
                        dp[i][j] = Math.min(1 + dp[i + 2][j],
                                               dp[i][j]);

                    /* loop over all right characters and
                      suppose Kth char is same as ith
                      character then choose minimum from
                      current and two substring after
                      ignoring ith and Kth char
                     */
                    for (int K = i + 2; K <= j; K++)
                        if (str.charAt(i) == str.charAt(K))
                            dp[i][j] = Math.min(
                                         dp[i + 1][K - 1] +
                                        dp[K + 1][j], dp[i][j]);
                }
            }
        }

        /* Uncomment below snippet to print actual dp tablex

           for (int i = 0; i < N; i++){
           System.out.println();
           for (int j = 0; j < N; j++)
           System.out.print(dp[i][j] + " ");
           }
            */

        return dp[0][N - 1];
    }

    // Driver code to test above methods
    public static void main(String args[]) {
        String str = "2553432";
        System.out.println(minStepToDeleteString(str));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to find minimum
# step to delete a string

# method returns minimum step for
# deleting the string, where in one
# step a palindrome is removed
def minStepToDeleteString(str):

    N = len(str)

    # declare dp array and initialize
    # it with 0s
    dp = [[0 for x in range(N + 1)]
             for y in range(N + 1)]

    # loop for substring length
    # we are considering
    for l in range(1, N + 1):

        # loop with two variables i and j, denoting
        # starting and ending of substrings
        i = 0
        j = l - 1
        while j < N:

            # If substring length is 1,
            # then 1 step will be needed
            if (l == 1):
                dp[i][j] = 1
            else:

                # delete the ith char individually
                # and assign result for subproblem (i+1,j)
                dp[i][j] = 1 + dp[i + 1][j]

                # if current and next char are
                # same, choose min from current
                # and subproblem (i+2,j)
                if (str[i] == str[i + 1]):
                    dp[i][j] = min(1 + dp[i + 2][j], dp[i][j])

                ''' loop over all right characters and suppose
                    Kth char is same as ith character then
                    choose minimum from current and two
                    substring after ignoring ith and Kth char '''
                for K in range(i + 2, j + 1):
                    if (str[i] == str[K]):
                        dp[i][j] = min(dp[i + 1][K - 1] +
                                       dp[K + 1][j], dp[i][j])

            i += 1
            j += 1

    # Uncomment below snippet to print
    # actual dp tablex
    # for (int i = 0; i < N; i++, cout << endl)
    # for (int j = 0; j < N; j++)
    #     cout << dp[i][j] << " ";

    return dp[0][N - 1]

# Driver Code
if __name__ == "__main__":
    str = "2553432"
    print( minStepToDeleteString(str))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to find minimum step to
// delete a string
using System;

class GFG {   

    /* method returns minimum step for deleting
    the string, where in one step a
    palindrome is removed */
    static int minStepToDeleteString(string str)
    {
        int N = str.Length;

        // declare dp array and initialize it
        // with 0s
        int [,]dp = new int[N + 1,N + 1];

        for (int i = 0; i <= N; i++)
            for (int j = 0; j <= N; j++)
                dp[i,j] = 0;

        // loop for substring length we are
        // considering
        for (int len = 1; len <= N; len++) {

            // loop with two variables i and j,
            // denoting starting and ending of
            // substrings
            for (int i = 0, j = len - 1; j < N; i++, j++)
            {

                // If substring length is 1, then 1
                // step will be needed
                if (len == 1)
                    dp[i,j] = 1;

                else
                {
                    // delete the ith char individually
                    // and assign result for
                    // subproblem (i+1,j)
                    dp[i,j] = 1 + dp[i + 1,j];

                    // if current and next char are same,
                    // choose min from current and
                    // subproblem (i+2, j)
                    if (str[i] == str[i + 1])
                        dp[i,j] = Math.Min(1 + dp[i + 2,j],
                                                  dp[i,j]);

                    /* loop over all right characters and
                    suppose Kth char is same as ith
                    character then choose minimum from
                    current and two substring after
                    ignoring ith and Kth char
                    */
                    for (int K = i + 2; K <= j; K++)
                        if (str[i] == str[K])
                            dp[i,j] = Math.Min(
                                        dp[i + 1,K - 1] +
                                     dp[K + 1,j], dp[i,j]);
                }
            }
        }

        /* Uncomment below snippet to print actual dp tablex

        for (int i = 0; i < N; i++){
        System.out.println();
        for (int j = 0; j < N; j++)
        System.out.print(dp[i][j] + " ");
        } */

        return dp[0,N - 1];
    }

    // Driver code to test above methods
    public static void Main()
    {
        string str = "2553432";
        Console.Write(minStepToDeleteString(str));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum step
// to delete a string

// method returns minimum step for
// deleting the string, where in one
// step a palindrome is removed */
function minStepToDeleteString($str)
{
    $N = strlen($str);

    // declare dp array and initialize
    // it with 0s
    $dp[$N + 1][$N + 1] = array(array());
    for ($i = 0; $i <= $N; $i++)
        for ($j = 0; $j <= $N; $j++)
            $dp[$i][$j] = 0;

    // loop for substring length we
    // are considering
    for ($len = 1; $len <= $N; $len++)
    {
        // loop with two variables i and j, denoting
        // starting and ending of substrings
        for ($i = 0, $j = $len - 1;
                     $j < $N; $i++, $j++)
        {
            // If substring length is 1, then
            // 1 step will be needed
            if ($len == 1)
                $dp[$i][$j] = 1;
            else
            {
                // delete the ith char individually
                // and assign result for subproblem (i+1,j)
                $dp[$i][$j] = 1 + $dp[$i + 1][$j];

                // if current and next char are same,
                // choose min from current and subproblem
                // (i+2,j)
                if ($str[$i] == $str[$i + 1])
                    $dp[$i][$j] = min(1 + $dp[$i + 2][$j],
                                          $dp[$i][$j]);

                /* loop over all right characters and suppose
                    Kth char is same as ith character then
                    choose minimum from current and two
                    substring after ignoring ith and Kth char */
                for ($K = $i + 2; $K <= $j; $K++)
                    if ($str[$i] == $str[$K])
                        $dp[$i][$j] = min($dp[$i + 1][$K - 1] +
                                          $dp[$K + 1][$j],
                                          $dp[$i][$j]);
            }
        }
    }

    /* Uncomment below snippet to print actual dp tablex
    for (int i = 0; i < N; i++, cout << endl)
        for (int j = 0; j < N; j++)
            cout << dp[i][j] << " "; */

    return $dp[0][$N - 1];
}

// Driver code
$str = "2553432";
echo minStepToDeleteString($str), "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// Java Script program to find minimum step to
// delete a string

    /* method returns minimum step for deleting
       the string, where in one step a
       palindrome is removed
     */
    function minStepToDeleteString(str)
    {
        let N = str.length;

        // declare dp array and initialize it with 0s
        let dp = new Array(N + 1);
        for (let i = 0; i <= N; i++)
        {
            dp[i]=new Array(N+1);
            for (let j = 0; j <= N; j++)
                dp[i][j] = 0;
          }
        // loop for substring length we are considering
        for (let len = 1; len <= N; len++) {

            // loop with two variables i and j, denoting
            // starting and ending of substrings
            for (let i = 0, j = len - 1; j < N; i++, j++) {

                // If substring length is 1, then 1 step
                // will be needed
                if (len == 1)
                    dp[i][j] = 1;

                else {
                    // delete the ith char individually
                    // and assign result for
                    // subproblem (i+1,j)
                    dp[i][j] = 1 + dp[i + 1][j];

                    // if current and next char are same,
                    // choose min from current and
                    // subproblem (i+2, j)
                    if (str[i] == str[i+1])
                        dp[i][j] = Math.min(1 + dp[i + 2][j],
                                               dp[i][j]);

                    /* loop over all right characters and
                      suppose Kth char is same as ith
                      character then choose minimum from
                      current and two substring after
                      ignoring ith and Kth char
                     */
                    for (let K = i + 2; K <= j; K++)
                        if (str[i] == str[K])
                            dp[i][j] = Math.min(
                                         dp[i + 1][K - 1] +
                                        dp[K + 1][j], dp[i][j]);
                }
            }
        }

        /* Uncomment below snippet to print actual dp tablex

           for (int i = 0; i < N; i++){
           System.out.println();
           for (int j = 0; j < N; j++)
           System.out.print(dp[i][j] + " ");
           }
            */

        return dp[0][N - 1];
    }

    // Driver code to test above methods
    let str = "2553432";
    document.write(minStepToDeleteString(str));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
2
```