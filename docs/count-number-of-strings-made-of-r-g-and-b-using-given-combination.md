# 使用给定的组合

计算弦的数量(由 R、G 和 B 组成)

> 原文:[https://www . geesforgeks . org/count-string-number-of-r-g-and-b-use-given-combination/](https://www.geeksforgeeks.org/count-number-of-strings-made-of-r-g-and-b-using-given-combination/)

我们需要制作一个大小为 n 的字符串，字符串的每个字符不是‘R’、‘B’就是‘G’。在最后的字符串中需要有至少 R 个‘R’，至少 B 个‘B’和至少 G 个‘G’(比如 r + g + b <= n). We need to find number of such strings possible.
**示例:**

```
Input : n = 4, r = 1, 
        b = 1, g = 1.
Output: 36 
No. of 'R' >= 1, 
No. of ‘G’ >= 1, 
No. of ‘B’ >= 1 and 
(No. of ‘R’) + (No. of ‘B’) + (No. of ‘G’) = n
then following cases are possible:
1\. RBGR and its 12 permutation
2\. RBGB and its 12 permutation
3\. RBGG and its 12 permutation
Hence answer is 36.
```

问于:[方向](https://www.geeksforgeeks.org/directi-interview-set-5-campus/)T2】

1.  因为 R、B 和 G 必须至少包含给定次数。剩余值= n -(r + b + g)。
2.  对剩余值进行所有组合。
3.  逐一考虑每个元素的剩余值，并总结所有排列。
4.  返回所有组合的排列总数。

## C++

```
// C++ program to count number of possible strings
// with n characters.
#include<bits/stdc++.h>
using namespace std;

// Function to calculate number of strings
int possibleStrings( int n, int r, int b, int g)
{
    // Store factorial of numbers up to n
    // for further computation
    int fact[n+1];
    fact[0] = 1;
    for (int i = 1; i <= n; i++)
        fact[i] = fact[i-1] * i;

    // Find the remaining values to be added
    int left = n - (r+g+b);
    int sum = 0;

    // Make all possible combinations
    // of R, B and G for the remaining value
    for (int i = 0; i <= left; i++)
    {
        for (int j = 0; j<= left-i; j++)
        {
            int k = left - (i+j);

            // Compute permutation of each combination
            // one by one and add them.
            sum = sum + fact[n] /
                       (fact[i+r]*fact[j+b]*fact[k+g]);
        }
    }

    // Return total no. of strings/permutation
    return sum;
}

// Drivers code
int main()
{
    int n = 4, r = 2;
    int b = 0, g = 1;
    cout << possibleStrings(n, r, b, g);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of possible
// strings with n characters.

class GFG{

    //Function to calculate number of strings
    static int possibleStrings( int n, int r, int b, int g)
    {
     // Store factorial of numbers up to n
     // for further computation
     int fact[] = new int[n+1];
     fact[0] = 1;
     for (int i = 1; i <= n; i++)
         fact[i] = fact[i-1] * i;

     // Find the remaining values to be added
     int left = n - (r+g+b);
     int sum = 0;

     // Make all possible combinations
     // of R, B and G for the remaining value
     for (int i = 0; i <= left; i++)
     {
         for (int j = 0; j<= left-i; j++)
         {
             int k = left - (i+j);

             // Compute permutation of each combination
             // one by one and add them.
             sum = sum + fact[n] /
                        (fact[i+r]*fact[j+b]*fact[k+g]);
         }
     }

     // Return total no. of strings/permutation
     return sum;
    }

    //Drivers code
    public static void main(String []args)
    {
        int n = 4, r = 2;
         int b = 0, g = 1;
         System.out.println(possibleStrings(n, r, b, g));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to count number of
# possible strings with n characters.

# Function to calculate number of strings
def possibleStrings(n, r, b, g):

    # Store factorial of numbers up to n
    # for further computation
    fact = [0 for i in range(n + 1)]
    fact[0] = 1
    for i in range(1, n + 1, 1):
        fact[i] = fact[i - 1] * i

    # Find the remaining values to be added
    left = n - (r + g + b)
    sum = 0

    # Make all possible combinations of
    # R, B and G for the remaining value
    for i in range(0, left + 1, 1):
        for j in range(0, left - i + 1, 1):
            k = left - (i + j)

            # Compute permutation of each
            # combination one by one and add them.
            sum = (sum + fact[n] / (fact[i + r] *
                         fact[j + b] * fact[k + g]))

    # Return total no. of
    # strings/permutation
    return sum

# Driver code
if __name__ == '__main__':
    n = 4
    r = 2
    b = 0
    g = 1
    print(int(possibleStrings(n, r, b, g)))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count number of possible
// strings with n characters.
using System;

class GFG
{

    //Function to calculate number of strings
    static int possibleStrings( int n, int r,
                                int b, int g)
    {
        // Store factorial of numbers up to n
        // for further computation
        int[] fact = new int[n + 1];
        fact[0] = 1;

        for (int i = 1; i <= n; i++)
            fact[i] = fact[i - 1] * i;

        // Find the remaining values to be added
        int left = n - (r + g + b);
        int sum = 0;

        // Make all possible combinations
        // of R, B and G for the remaining value
        for (int i = 0; i <= left; i++)
        {
            for (int j = 0; j <= left - i; j++)
            {
                int k = left - (i + j);

                // Compute permutation of each combination
                // one by one and add them.
                sum = sum + fact[n] / (fact[i + r] *
                        fact[j + b] * fact[k + g]);
            }
        }

        // Return total no. of strings/permutation
        return sum;
    }

    //Drivers code
    public static void Main()
    {
        int n = 4, r = 2;
        int b = 0, g = 1;
        Console.WriteLine(possibleStrings(n, r, b, g));
    }
}

// This Code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of possible strings with
// n characters.

// Function to calculate
// number of strings
function possibleStrings( $n, $r, $b, $g)
{

    // Store factorial of
    // numbers up to n for
    // further computation
    $fact[0] = 1;
    for ($i = 1; $i <= $n; $i++)
        $fact[$i] = $fact[$i - 1] * $i;

    // Find the remaining
    // values to be added
    $left = $n - ($r + $g + $b);
    $sum = 0;

    // Make all possible combinations
    // of R, B and G for the remaining value
    for ($i = 0; $i <= $left; $i++)
    {
        for ($j = 0; $j <= $left - $i; $j++)
        {
            $k = $left - ($i+$j);

            // Compute permutation of
            // each combination one
            // by one and add them.
            $sum = $sum + $fact[$n] /
                   ($fact[$i + $r] *
                   $fact[$j + $b] *
                   $fact[$k + $g]);
        }
    }

    // Return total no. of
    // strings/permutation
    return $sum;
}

    // Driver Code
    $n = 4; $r = 2;
    $b = 0; $g = 1;

    echo possibleStrings($n, $r, $b, $g);

// This code is contributed by jit_t.
?>
```

## java 描述语言

```
<script>
// Javascript program to count number of possible
// strings with n characters.

    // Function to calculate number of strings
    function possibleStrings(n,r,b,g)
    {
        // Store factorial of numbers up to n
     // for further computation
     let fact = new Array(n+1);
     fact[0] = 1;
     for (let i = 1; i <= n; i++)
         fact[i] = fact[i-1] * i;

     // Find the remaining values to be added
     let left = n - (r+g+b);
     let sum = 0;

     // Make all possible combinations
     // of R, B and G for the remaining value
     for (let i = 0; i <= left; i++)
     {
         for (let j = 0; j<= left-i; j++)
         {
             let k = left - (i+j);

             // Compute permutation of each combination
             // one by one and add them.
             sum = sum + fact[n] /
                        (fact[i+r]*fact[j+b]*fact[k+g]);
         }
     }

     // Return total no. of strings/permutation
     return sum;
    }

    // Drivers code
    let n = 4, r = 2;
    let b = 0, g = 1;
    document.write(possibleStrings(n, r, b, g));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
22
```

为了处理 n 个大数，我们可以使用[大阶乘](https://www.geeksforgeeks.org/factorial-large-number/)的概念。
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。