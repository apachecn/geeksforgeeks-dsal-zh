# 画栅栏算法

> 原文:[https://www.geeksforgeeks.org/painting-fence-algorithm/](https://www.geeksforgeeks.org/painting-fence-algorithm/)

给定一个有 n 个柱子和 k 种颜色的围栏，找出油漆围栏的方法，使最多两个相邻的柱子具有相同的颜色。因为答案可能很大，所以返回模 10^9 + 7。
**例:**

```
Input : n = 2 k = 4
Output : 16
We have 4 colors and 2 posts.
Ways when both posts have same color : 4 
Ways when both posts have diff color :
4(choices for 1st post) * 3(choices for 
2nd post) = 12

Input : n = 3 k = 2
Output : 6
```

下图描述了用 2 种颜色绘制 3 个帖子的 6 种可能方式:

![](https://cdnwrite.geeksforgeeks.org/wp-content/uploads/painting-fence-1.png)

考虑下面的图像，其中 c、c’和 c”分别是帖子 I、i-1 和 i -2 的颜色。

![](https://cdnwrite.geeksforgeeks.org/wp-content/uploads/painting-fence-2.png)

根据问题的约束，c = c' = c "不可能同时出现，所以要么 c '！= c 或 c "！= c 或两者都有。c '有 k–1 种可能性！= c 和 k–1 代表 c”！= c。

```
 diff = no of ways when color of last
        two posts is different
 same = no of ways when color of last 
        two posts is same
 total ways = diff + sum

for n = 1
    diff = k, same = 0
    total = k

for n = 2
    diff = k * (k-1) //k choices for
           first post, k-1 for next
    same = k //k choices for common 
           color of two posts
    total = k +  k * (k-1)

for n = 3
    diff = k * (k-1)* (k-1) 
           //(k-1) choices for the first place 
        // k choices for the second place
        //(k-1) choices for the third place
    same = k * (k-1) * 2
        // 2 is multiplied because consider two color R and B
        // R R B or B R R 
        // B B R or R B B  
           c'' != c, (k-1) choices for it

Hence we deduce that,
total[i] = same[i] + diff[i]
same[i]  = diff[i-1]
diff[i]  = (diff[i-1] + diff[i-2]) * (k-1)
         = total[i-1] * (k-1)
```

下面是问题的实现:

## C++

```
// C++ program for Painting Fence Algorithm
// optimised version

#include <bits/stdc++.h>
using namespace std;

// Returns count of ways to color k posts
long countWays(int n, int k)
{
    long dp[n + 1];
    memset(dp, 0, sizeof(dp));
    long long mod = 1000000007;

    dp[1] = k;
    dp[2] = k * k;

    for (int i = 3; i <= n; i++) {
        dp[i] = ((k - 1) * (dp[i - 1] + dp[i - 2])) % mod;
    }

    return dp[n];
}

// Driver code
int main()
{
    int n = 3, k = 2;
    cout << countWays(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Painting Fence Algorithm
import java.util.*;

class GfG {

    // Returns count of ways to color k posts
    // using k colors
    static long countWays(int n, int k)
    {
        // To store results for subproblems
        long dp[] = new long[n + 1];
        Arrays.fill(dp, 0);
        int mod = 1000000007;

        // There are k ways to color first post
        dp[1] = k;

        // There are 0 ways for single post to
        // violate (same color_ and k ways to
        // not violate (different color)
        int same = 0, diff = k;

        // Fill for 2 posts onwards
        for (int i = 2; i <= n; i++) {
            // Current same is same as previous diff
            same = diff;

            // We always have k-1 choices for next post
            diff = (int)(dp[i - 1] * (k - 1));
            diff = diff % mod;

            // Total choices till i.
            dp[i] = (same + diff) % mod;
        }

        return dp[n];
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3, k = 2;
        System.out.println(countWays(n, k));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for Painting Fence Algorithm
# optimised version

# Returns count of ways to color k posts
def countWays(n, k):

    dp = [0] * (n + 1)
    total = k
    mod = 1000000007

    dp[1] = k
    dp[2] = k * k   

    for i in range(3,n+1):
        dp[i] = ((k - 1) * (dp[i - 1] + dp[i - 2])) % mod

    return dp[n]

# Driver code
n = 3
k = 2
print(countWays(n, k))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for Painting Fence Algorithm
using System;
public class GFG
{

  // Returns count of ways to color k posts
  // using k colors
  static long countWays(int n, int k)
  {

    // To store results for subproblems
    long[] dp = new long[n + 1];
    Array.Fill(dp, 0);
    int mod = 1000000007;

    // There are k ways to color first post
    dp[1] = k;

    // There are 0 ways for single post to
    // violate (same color_ and k ways to
    // not violate (different color)
    int same = 0, diff = k;

    // Fill for 2 posts onwards
    for (int i = 2; i <= n; i++)
    {

      // Current same is same as previous diff
      same = diff;

      // We always have k-1 choices for next post
      diff = (int)(dp[i - 1] * (k - 1));
      diff = diff % mod;

      // Total choices till i.
      dp[i] = (same + diff) % mod;
    }

    return dp[n];
  }

  // Driver code
  static public void Main ()
  {
    int n = 3, k = 2;
    Console.WriteLine(countWays(n, k));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
    // Javascript program for Painting Fence Algorithm

    // Returns count of ways to color k posts
    // using k colors
    function countWays(n, k)
    {

      // To store results for subproblems
      let dp = new Array(n + 1);
      dp.fill(0);
      let mod = 1000000007;

      // There are k ways to color first post
      dp[1] = k;

      // There are 0 ways for single post to
      // violate (same color_ and k ways to
      // not violate (different color)
      let same = 0, diff = k;

      // Fill for 2 posts onwards
      for (let i = 2; i <= n; i++)
      {

        // Current same is same as previous diff
        same = diff;

        // We always have k-1 choices for next post
        diff = (dp[i - 1] * (k - 1));
        diff = diff % mod;

        // Total choices till i.
        dp[i] = (same + diff) % mod;
      }

      return dp[n];
    }

    let n = 3, k = 2;
    document.write(countWays(n, k));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
6
```

**空间优化:**
我们可以优化上面的解，用一个变量代替一个表。
下面是问题的实现:

## C++

```
// C++ program for Painting Fence Algorithm
#include <bits/stdc++.h>
using namespace std;

// Returns count of ways to color k posts
// using k colors
long countWays(int n, int k)
{
    // There are k ways to color first post
    long total = k;
    int mod = 1000000007;

    // There are 0 ways for single post to
    // violate (same color) and k ways to
    // not violate (different color)
    int same = 0, diff = k;

    // Fill for 2 posts onwards
    for (int i = 2; i <= n; i++) {
        // Current same is same as previous diff
        same = diff;

        // We always have k-1 choices for next post
        diff = total * (k - 1);
        diff = diff % mod;

        // Total choices till i.
        total = (same + diff) % mod;
    }

    return total;
}

// Driver code
int main()
{
    int n = 3, k = 2;
    cout << countWays(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Painting Fence Algorithm
class GFG {

    // Returns count of ways to color k posts
    // using k colors
    static long countWays(int n, int k)
    {
        // There are k ways to color first post
        long total = k;
        int mod = 1000000007;

        // There are 0 ways for single post to
        // violate (same color_ and k ways to
        // not violate (different color)
        int same = 0, diff = k;

        // Fill for 2 posts onwards
        for (int i = 2; i <= n; i++) {
            // Current same is same as previous diff
            same = diff;

            // We always have k-1 choices for next post
            diff = (int)total * (k - 1);
            diff = diff % mod;

            // Total choices till i.
            total = (same + diff) % mod;
        }
        return total;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3, k = 2;
        System.out.println(countWays(n, k));
    }
}

// This code is contributed by Mukul Singh
```

## 蟒蛇 3

```
# Python3 program for Painting
# Fence Algorithm

# Returns count of ways to color
# k posts using k colors
def countWays(n, k) :

    # There are k ways to color first post
    total = k
    mod = 1000000007

    # There are 0 ways for single post to
    # violate (same color_ and k ways to
    # not violate (different color)
    same, diff = 0, k

    # Fill for 2 posts onwards
    for i in range(2, n + 1) :

        # Current same is same as
        # previous diff
        same = diff

        # We always have k-1 choices
        # for next post
        diff = total * (k - 1)
        diff = diff % mod

        # Total choices till i.
        total = (same + diff) % mod

    return total

# Driver code
if __name__ == "__main__" :

    n, k = 3, 2
    print(countWays(n, k))

# This code is contributed by Ryuga
```

## C#

```
// C# program for Painting Fence Algorithm
using System;

class GFG {
    // Returns count of ways to color k posts
    // using k colors
    static long countWays(int n, int k)
    {
        // There are k ways to color first post
        long total = k;
        int mod = 1000000007;

        // There are 0 ways for single post to
        // violate (same color_ and k ways to
        // not violate (different color)
        long same = 0, diff = k;

        // Fill for 2 posts onwards
        for (int i = 2; i <= n; i++) {
            // Current same is same as previous diff
            same = diff;

            // We always have k-1 choices for next post
            diff = total * (k - 1);
            diff = diff % mod;

            // Total choices till i.
            total = (same + diff) % mod;
        }

        return total;
    }

    // Driver code
    static void Main()
    {
        int n = 3, k = 2;
        Console.Write(countWays(n, k));
    }
}

// This code is contributed by DrRoot_
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Painting Fence Algorithm

// Returns count of ways to color k
// posts using k colors
function countWays($n, $k)
{
    // There are k ways to color first post
    $total = $k;
    $mod = 1000000007;

    // There are 0 ways for single post to
    // violate (same color_ and k ways to
    // not violate (different color)
    $same = 0;
    $diff = $k;

    // Fill for 2 posts onwards
    for ($i = 2; $i <= $n; $i++)
    {
        // Current same is same as previous diff
        $same = $diff;

        // We always have k-1 choices for next post
        $diff = $total * ($k - 1);
        $diff = $diff % $mod;

        // Total choices till i.
        $total = ($same + $diff) % $mod;
    }

    return $total;
}

// Driver code
$n = 3;
$k = 2;
echo countWays($n, $k) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

    // JavaScript program for Painting Fence Algorithm

    // Returns count of ways to color k posts
    // using k colors
    function countWays(n, k)
    {
        // There are k ways to color first post
        let total = k;
        let mod = 1000000007;

        // There are 0 ways for single post to
        // violate (same color_ and k ways to
        // not violate (different color)
        let same = 0, diff = k;

        // Fill for 2 posts onwards
        for (let i = 2; i <= n; i++) {
            // Current same is same as previous diff
            same = diff;

            // We always have k-1 choices for next post
            diff = total * (k - 1);
            diff = diff % mod;

            // Total choices till i.
            total = (same + diff) % mod;
        }

        return total;
    }

    let n = 3, k = 2;
      document.write(countWays(n, k));

</script>
```

**输出:**

```
6
```

本文由**阿迪提·夏尔马**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。