# 最多进行 K 次跳跃到达第 n 层的方式数

> 原文:[https://www . geeksforgeeks . org/到达第 n 层的途径数最多 k 次跳跃/](https://www.geeksforgeeks.org/number-of-ways-to-reach-nth-floor-by-taking-at-most-k-leaps/)

给定 N 个楼梯。同样给定一次跳跃最多能走的步数(K)。任务是找到一个(**只考虑组合**)可以从底层 K 次或更少的跳跃爬上建筑顶部的可能方式的数量。
**例:**

> **输入:** N = 5，K = 3
> **输出:** 5
> 要到达 5 号楼梯，我们可以选择以下跳跃组合:
> 1 1 1 1 1 1
> 1 1 2
> 1 2 2
> 1 1 3
> 2 3
> 因此答案是 5。
> **输入:** N = 29，K = 5
> **输出:** 603

设*组合【I】*为到达 I 层的路数。因此，通过跳跃 i-j 从 combo[j]到达 combo[i]的方法数量将是 ***combo[i] += combo[j]。*** 所以迭代所有可能的跳跃，并为每个可能的跳跃不断添加可能的组合到组合数组。最终答案将存储在组合框[N]中。
以下是上述方法的实施。

## C++

```
// C++ program to reach N-th stair
// by taking a maximum of K leap
#include <bits/stdc++.h>

using namespace std;

int solve(int N, int K)
{

    // elements of combo[] stores the no of
    // possible ways to reach it by all
    // combinations of k leaps or less

    int combo[N + 1] = { 0 };

    // assuming leap 0 exist and assigning
    // its value to 1 for calculation
    combo[0] = 1;

    // loop to iterate over all
    // possible leaps upto k;
    for (int i = 1; i <= K; i++) {

        // in this loop we count all possible
        // leaps to reach the jth stair with
        // the help of ith leap or less
        for (int j = 0; j <= N; j++) {

            // if the leap is not more than the i-j
            if (j >= i) {

                // calculate the value and
                // store in combo[j]
                // to reuse it for next leap
                // calculation for the jth stair
                combo[j] += combo[j - i];
            }
        }
    }

    // returns the no of possible number
    // of leaps to reach the top of
    // building of n stairs
    return combo[N];
}

// Driver Code
int main()
{
    // N i the no of total stairs
    // K is the value of the greatest leap
    int N = 29;
    int K = 5;

    cout << solve(N, K);

    solve(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reach N-th
// stair by taking a maximum
// of K leap
class GFG
{
static int solve(int N, int K)
{

    // elements of combo[] stores
    // the no. of possible ways
    // to reach it by all combinations
    // of k leaps or less
    int[] combo;
    combo = new int[50];

    // assuming leap 0 exist
    // and assigning its value
    // to 1 for calculation
    combo[0] = 1;

    // loop to iterate over all
    // possible leaps upto k;
    for (int i = 1; i <= K; i++)
    {

        // in this loop we count all
        // possible leaps to reach
        // the jth stair with the
        // help of ith leap or less
        for (int j = 0; j <= N; j++)
        {

            // if the leap is not
            // more than the i-j
            if (j >= i)
            {

                // calculate the value and
                // store in combo[j] to
                // reuse it for next leap
                // calculation for the
                // jth stair
                combo[j] += combo[j - i];
            }
        }
    }

    // returns the no of possible
    // number of leaps to reach
    // the top of building of
    // n stairs
    return combo[N];
}

// Driver Code
public static void main(String args[])
{
    // N i the no of total stairs
    // K is the value of the
    // greatest leap
    int N = 29;
    int K = 5;

    System.out.println(solve(N, K));

    solve(N, K);
}
}

// This code is contributed
// by ankita_saini
```

## 蟒蛇 3

```
# Python3 program to reach N-th stair
# by taking a maximum of K leap

def solve(N, K) :

    # elements of combo[] stores the no of 
    # possible ways to reach it by all 
    # combinations of k leaps or less
    combo = [0] * (N + 1)

    # assuming leap 0 exist and assigning 
    # its value to 1 for calculation
    combo[0] = 1

    # loop to iterate over all 
    # possible leaps upto k;
    for i in range(1, K + 1) :

        #  in this loop we count all possible 
        # leaps to reach the jth stair with 
        # the help of ith leap or less 
        for j in range(0, N + 1) :

            # if the leap is not more than the i-j 
            if j >= i :

                # calculate the value and 
                # store in combo[j] 
                # to reuse it for next leap 
                # calculation for the jth stair
                combo[j] += combo[j - i]

    # returns the no of possible number 
    # of leaps to reach the top of 
    # building of n stairs 
    return combo[N]

# Driver Code
if __name__ == "__main__" :

    # N i the no of total stairs 
    # K is the value of the greatest leap
    N, K = 29, 5

    print(solve(N, K))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to reach N-th
// stair by taking a maximum
// of K leap
using System;

class GFG
{
static int solve(int N, int K)
{

    // elements of combo[] stores
    // the no. of possible ways
    // to reach it by all combinations
    // of k leaps or less
    int[] combo;
    combo = new int[50];

    // assuming leap 0 exist
    // and assigning its value
    // to 1 for calculation
    combo[0] = 1;

    // loop to iterate over all
    // possible leaps upto k;
    for (int i = 1; i <= K; i++)
    {

        // in this loop we count all
        // possible leaps to reach
        // the jth stair with the
        // help of ith leap or less
        for (int j = 0; j <= N; j++)
        {

            // if the leap is not
            // more than the i-j
            if (j >= i)
            {

                // calculate the value and
                // store in combo[j] to
                // reuse it for next leap
                // calculation for the
                // jth stair
                combo[j] += combo[j - i];
            }
        }
    }

    // returns the no of possible
    // number of leaps to reach
    // the top of building of
    // n stairs
    return combo[N];
}

// Driver Code
public static void Main()
{
    // N i the no of total stairs
    // K is the value of the
    // greatest leap
    int N = 29;
    int K = 5;

    Console.WriteLine(solve(N, K));
    solve(N, K);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
error_reporting(0);
// PHP program to reach N-th
// stair by taking a maximum
// of K leap
function solve($N, $K)
{

    // elements of combo[] stores
    // the no of possible ways to
    // reach it by all combinations
    // of k leaps or less
    $combo[$N + 1] = array();

    // assuming leap 0 exist and
    // assigning its value to 1
    // for calculation
    $combo[0] = 1;

    // loop to iterate over all
    // possible leaps upto k;
    for ($i = 1; $i <= $K; $i++)
    {

        // in this loop we count
        // all possible leaps to
        // reach the jth stair with
        // the help of ith leap or less
        for ($j = 0; $j <= $N; $j++)
        {
            // if the leap is not
            // more than the i-j
            if ($j >= $i)
            {

                // calculate the value and
                // store in combo[j]
                // to reuse it for next leap
                // calculation for the jth stair
                $combo[$j] += $combo[$j - $i];
            }
        }
    }

    // returns the no of possible
    // number of leaps to reach
    // the top of building of n stairs
    return $combo[$N];
}

// Driver Code

// N i the no of total stairs
// K is the value of the greatest leap
$N = 29;
$K = 5;

echo solve($N, $K);

solve($N, $K);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>
    // Javascript program to reach N-th
    // stair by taking a maximum
    // of K leap

    function solve(N, K)
    {

        // elements of combo[] stores
        // the no. of possible ways
        // to reach it by all combinations
        // of k leaps or less
        let combo = new Array(50);
        combo.fill(0);

        // assuming leap 0 exist
        // and assigning its value
        // to 1 for calculation
        combo[0] = 1;

        // loop to iterate over all
        // possible leaps upto k;
        for (let i = 1; i <= K; i++)
        {

            // in this loop we count all
            // possible leaps to reach
            // the jth stair with the
            // help of ith leap or less
            for (let j = 0; j <= N; j++)
            {

                // if the leap is not
                // more than the i-j
                if (j >= i)
                {

                    // calculate the value and
                    // store in combo[j] to
                    // reuse it for next leap
                    // calculation for the
                    // jth stair
                    combo[j] += combo[j - i];
                }
            }
        }

        // returns the no of possible
        // number of leaps to reach
        // the top of building of
        // n stairs
        return combo[N];
    }

    // N i the no of total stairs
    // K is the value of the
    // greatest leap
    let N = 29;
    let K = 5;

    document.write(solve(N, K));
    solve(N, K);

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
603
```

**时间复杂度:**O(N * K)
T3】辅助空间: O(N)