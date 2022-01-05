# 形成具有不同相邻元素的阵列的方法数量

> 原文:[https://www . geeksforgeeks . org/形成具有不同相邻元素的数组的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-form-an-array-with-distinct-adjacent-elements/)

给定三个整数 N、M 和 X，任务是找到形成数组的方法的数量，使得数组的所有连续数字都是不同的，并且数组从 2 到 N–1(考虑基于 1 的索引)的任何索引处的值都在 1 和 M 之间，而索引 1 处的值是 X，索引 N 处的值是 1。
注:X 的值介于 1 和 m 之间
**例:**

> **输入:** N = 4，M = 3，X = 2
> **输出:** 3
> 以下数组是可能的:
> 1) 2，1，2，1
> 2) 2，1，3，1
> 3) 2，3，2，1
> **输入:** N = 2，M = 3，X = 2
> **输出:** 1
> 唯一可能的数组是:2，2

**方法:**使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。让，f(i)表示直到第 I 个索引时形成数组的方法的数量，这样数组的每个连续元素都是不同的。让 f(i，One)表示形成数组直到第 I 个索引的方法的数量，这样数组的每个连续元素都是不同的，并且 arr <sub>i</sub> = 1。
同样，让 **f(i，Non-One)** 表示直到第 I 个索引时形成数组的方式数，这样数组的每个连续元素都是不同的，arr <sub>i</sub> 不等于 1。
形成以下复发:

```
f(i, Non-One) = f(i - 1, One) * (M - 1) + f(i - 1, Non-One) * (M - 2)
```

这意味着使用两种情况形成数组直到数组的第 I 个索引 <sub>i</sub> 不等于 1 的方式数:

1.  如果数组<sub>I–1</sub>中的数字为 1，则从**(M–1)**选项中选择一个数字放在 i <sup>第</sup>个索引处，因为数组 <sub>i</sub> 不等于 1。
2.  如果数组<sub>I–1</sub>的数字不是 1，那么我们需要从**(M–2)**选项中选择一个数字，因为数组 <sub>i</sub> 不等于 1，数组 <sub>i</sub> 数组<sub>I–1</sub>。

类似地， **f(i，One)= f(I–1，Non One)**，由于用数组 <sub>i</sub> = 1 形成数组直到第 I 个索引的方式数与用数组<sub>I–1</sub>1 形成数组直到第(I–1)个索引的方式数相同，因此在第 I<sup>I</sup>索引处只有一个选项。如果 f(N，1)自数组 <sub>N</sub> 需要等于 1，则在最后给出所需答案。
以下是上述方法的实施:

## C++

```
// C++ program to count the number of ways
// to form arrays of N numbers such that the
// first and last numbers are fixed
// and all consecutive numbers are distinct
#include <bits/stdc++.h>
using namespace std;

// Returns the total ways to form arrays such that
// every consecutive element is different and each
// element except the first and last can take values
// from 1 to M
int totalWays(int N, int M, int X)
{

    // define the dp[][] array
    int dp[N + 1][2];

    // if the first element is 1
    if (X == 1) {

        // there is only one way to place
        // a 1 at the first index
        dp[0][0] = 1;
    }
    else {

        // the value at first index needs to be 1,
        // thus there is no way to place a non-one integer
        dp[0][1] = 0;
    }

    // if the first element was 1 then at index 1,
    // only non one integer can be placed thus
    // there are M - 1 ways to place a non one integer
    // at index 2 and 0 ways to place a 1 at the 2nd index
    if (X == 1) {
        dp[1][0] = 0;
        dp[1][1] = M - 1;
    }

    // Else there is one way to place a one at
    // index 2 and if a non one needs to be placed here,
    // there are (M - 2) options, i.e
    // neither the element at this index
    // should be 1, neither should it be
    // equal to the previous element
    else {
        dp[1][0] = 1;
        dp[1][1] = (M - 2);
    }

    // Build the dp array in bottom up manner
    for (int i = 2; i < N; i++) {

        // f(i, one) = f(i - 1, non-one)
        dp[i][0] = dp[i - 1][1];

        // f(i, non-one) = f(i - 1, one) * (M - 1) +
        // f(i - 1, non-one) * (M - 2)
        dp[i][1] = dp[i - 1][0] * (M - 1) + dp[i - 1][1] * (M - 2);
    }

    // last element needs to be one, so return dp[n - 1][0]
    return dp[N - 1][0];
}

// Driver Code
int main()
{

    int N = 4, M = 3, X = 2;
    cout << totalWays(N, M, X) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the
// number of ways to form
// arrays of N numbers such
// that the first and last
// numbers are fixed and all
// consecutive numbers are
// distinct
import java.io.*;

class GFG
{

// Returns the total ways to
// form arrays such that every
// consecutive element is
// different and each element
// except the first and last
// can take values from 1 to M
static int totalWays(int N,
                     int M, int X)
{

    // define the dp[][] array
    int dp[][] = new int[N + 1][2];

    // if the first element is 1
    if (X == 1)
    {

        // there is only one
        // way to place a 1
        // at the first index
        dp[0][0] = 1;
    }
    else
    {

        // the value at first index
        // needs to be 1, thus there
        // is no way to place a
        // non-one integer
        dp[0][1] = 0;
    }

    // if the first element was 1
    // then at index 1, only non
    // one integer can be placed
    // thus there are M - 1 ways
    // to place a non one integer
    // at index 2 and 0 ways to
    // place a 1 at the 2nd index
    if (X == 1)
    {
        dp[1][0] = 0;
        dp[1][1] = M - 1;
    }

    // Else there is one way to
    // place a one at index 2
    // and if a non one needs to
    // be placed here, there are
    // (M - 2) options, i.e neither
    // the element at this index
    // should be 1, neither should
    // it be equal to the previous
    // element
    else
    {
        dp[1][0] = 1;
        dp[1][1] = (M - 2);
    }

    // Build the dp array
    // in bottom up manner
    for (int i = 2; i < N; i++)
    {

        // f(i, one) = f(i - 1,
        // non-one)
        dp[i][0] = dp[i - 1][1];

        // f(i, non-one) =
        // f(i - 1, one) * (M - 1) +
        // f(i - 1, non-one) * (M - 2)
        dp[i][1] = dp[i - 1][0] * (M - 1) +
                   dp[i - 1][1] * (M - 2);
    }

    // last element needs to be
    // one, so return dp[n - 1][0]
    return dp[N - 1][0];
}

// Driver Code
public static void main (String[] args)
{
    int N = 4, M = 3, X = 2;
    System.out.println(totalWays(N, M, X));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to count the number of ways
# to form arrays of N numbers such that the
# first and last numbers are fixed
# and all consecutive numbers are distinct

# Returns the total ways to form arrays such that
# every consecutive element is different and each
# element except the first and last can take values
# from 1 to M
def totalWays(N,M,X):

    # define the dp[][] array
    dp = [[0 for i in range(2)] for j in range(N+1)]

    # if the first element is 1
    if (X == 1):

        # there is only one way to place
        # a 1 at the first index
        dp[0][0] = 1

    else:
        # the value at first index needs to be 1,
        # thus there is no way to place a non-one integer
        dp[0][1] = 0

    # if the first element was 1 then at index 1,
    # only non one integer can be placed thus
    # there are M - 1 ways to place a non one integer
    # at index 2 and 0 ways to place a 1 at the 2nd index
    if (X == 1):
        dp[1][0] = 0
        dp[1][1] = M - 1

    # Else there is one way to place a one at
    # index 2 and if a non one needs to be placed here,
    # there are (M - 2) options, i.e
    # neither the element at this index
    # should be 1, neither should it be
    # equal to the previous element
    else:
        dp[1][0] = 1
        dp[1][1] = (M - 2)

    # Build the dp array in bottom up manner
    for i in range(2,N):
        # f(i, one) = f(i - 1, non-one)
        dp[i][0] = dp[i - 1][1]

        # f(i, non-one) = f(i - 1, one) * (M - 1) +
        # f(i - 1, non-one) * (M - 2)
        dp[i][1] = dp[i - 1][0] * (M - 1) + dp[i - 1][1] * (M - 2)

    # last element needs to be one, so return dp[n - 1][0]
    return dp[N - 1][0]

# Driver Code
if __name__ == '__main__':
    N = 4
    M = 3
    X = 2
    print(totalWays(N, M, X))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count the
// number of ways to form
// arrays of N numbers such
// that the first and last
// numbers are fixed and all
// consecutive numbers are
// distinct
using System;

class GFG
{

// Returns the total ways to
// form arrays such that every
// consecutive element is
// different and each element
// except the first and last
// can take values from 1 to M
static int totalWays(int N,
                     int M, int X)
{

    // define the dp[][] array
    int [,]dp = new int[N + 1, 2];

    // if the first element is 1
    if (X == 1)
    {

        // there is only one
        // way to place a 1
        // at the first index
        dp[0, 0] = 1;
    }
    else
    {

        // the value at first index
        // needs to be 1, thus there
        // is no way to place a
        // non-one integer
        dp[0, 1] = 0;
    }

    // if the first element was 1
    // then at index 1, only non
    // one integer can be placed
    // thus there are M - 1 ways
    // to place a non one integer
    // at index 2 and 0 ways to
    // place a 1 at the 2nd index
    if (X == 1)
    {
        dp[1, 0] = 0;
        dp[1, 1] = M - 1;
    }

    // Else there is one way to
    // place a one at index 2
    // and if a non one needs to
    // be placed here, there are
    // (M - 2) options, i.e neither
    // the element at this index
    // should be 1, neither should
    // it be equal to the previous
    // element
    else
    {
        dp[1, 0] = 1;
        dp[1, 1] = (M - 2);
    }

    // Build the dp array
    // in bottom up manner
    for (int i = 2; i < N; i++)
    {

        // f(i, one) = f(i - 1,
        // non-one)
        dp[i, 0] = dp[i - 1, 1];

        // f(i, non-one) =
        // f(i - 1, one) * (M - 1) +
        // f(i - 1, non-one) * (M - 2)
        dp[i, 1] = dp[i - 1, 0] * (M - 1) +
                   dp[i - 1, 1] * (M - 2);
    }

    // last element needs to be
    // one, so return dp[n - 1][0]
    return dp[N - 1, 0];
}

// Driver Code
public static void Main ()
{
    int N = 4, M = 3, X = 2;
    Console.WriteLine(totalWays(N, M, X));
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the
// number of ways to form
// arrays of N numbers such
// that the first and last
// numbers are fixed and all
// consecutive numbers are distinct

// Returns the total ways to
// form arrays such that every
// consecutive element is
// different and each element
// except the first and last
// can take values from 1 to M
function totalWays($N, $M, $X)
{

    // define the dp[][] array
    $dp = array(array());

    // if the first element is 1
    if ($X == 1)
    {

        // there is only one
        // way to place a 1
        // at the first index
        $dp[0][0] = 1;
    }
    else
    {

        // the value at first
        // index needs to be 1,
        // thus there is no way
        // to place a non-one integer
        $dp[0][1] = 0;
    }

    // if the first element was
    // 1 then at index 1, only
    // non one integer can be
    // placed thus there are M - 1
    // ways to place a non one
    // integer at index 2 and 0 ways
    // to place a 1 at the 2nd index
    if ($X == 1)
    {
        $dp[1][0] = 0;
        $dp[1][1] = $M - 1;
    }

    // Else there is one way
    // to place a one at index
    // 2 and if a non one needs
    // to be placed here, there
    // are (M - 2) options, i.e
    // neither the element at
    // this index should be 1,
    // neither should it be equal
    // to the previous element
    else
    {
        $dp[1][0] = 1;
        $dp[1][1] = ($M - 2);
    }

    // Build the dp array
    // in bottom up manner
    for ($i = 2; $i <$N; $i++)
    {

        // f(i, one) =
        // f(i - 1, non-one)
        $dp[$i][0] = $dp[$i - 1][1];

        // f(i, non-one) =
        // f(i - 1, one) * (M - 1) +
        // f(i - 1, non-one) * (M - 2)
        $dp[$i][1] = $dp[$i - 1][0] *
                           ($M - 1) +
                     $dp[$i - 1][1] *
                           ($M - 2);
    }

    // last element needs to
    // be one, so return dp[n - 1][0]
    return $dp[$N - 1][0];
}

// Driver Code
$N = 4; $M = 3; $X = 2;
echo totalWays($N, $M, $X);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to count the
    // number of ways to form
    // arrays of N numbers such
    // that the first and last
    // numbers are fixed and all
    // consecutive numbers are
    // distinct

    // Returns the total ways to
    // form arrays such that every
    // consecutive element is
    // different and each element
    // except the first and last
    // can take values from 1 to M
    function totalWays(N, M, X)
    {

        // define the dp[][] array
        let dp = new Array(N + 1);
        for(let i = 0; i < N + 1; i++)
        {
            dp[i] = new Array(2);
            for(let j = 0; j < 2; j++)
            {
                dp[i][j] = 0;
            }
        }

        // if the first element is 1
        if (X == 1)
        {

            // there is only one
            // way to place a 1
            // at the first index
            dp[0][0] = 1;
        }
        else
        {

            // the value at first index
            // needs to be 1, thus there
            // is no way to place a
            // non-one integer
            dp[0][1] = 0;
        }

        // if the first element was 1
        // then at index 1, only non
        // one integer can be placed
        // thus there are M - 1 ways
        // to place a non one integer
        // at index 2 and 0 ways to
        // place a 1 at the 2nd index
        if (X == 1)
        {
            dp[1][0] = 0;
            dp[1][1] = M - 1;
        }

        // Else there is one way to
        // place a one at index 2
        // and if a non one needs to
        // be placed here, there are
        // (M - 2) options, i.e neither
        // the element at this index
        // should be 1, neither should
        // it be equal to the previous
        // element
        else
        {
            dp[1][0] = 1;
            dp[1][1] = (M - 2);
        }

        // Build the dp array
        // in bottom up manner
        for (let i = 2; i < N; i++)
        {

            // f(i, one) = f(i - 1,
            // non-one)
            dp[i][0] = dp[i - 1][1];

            // f(i, non-one) =
            // f(i - 1, one) * (M - 1) +
            // f(i - 1, non-one) * (M - 2)
            dp[i][1] = dp[i - 1][0] * (M - 1) +
                       dp[i - 1][1] * (M - 2);
        }

        // last element needs to be
        // one, so return dp[n - 1][0]
        return dp[N - 1][0];
    }

    let N = 4, M = 3, X = 2;
    document.write(totalWays(N, M, X));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)，其中 N 是数组的大小