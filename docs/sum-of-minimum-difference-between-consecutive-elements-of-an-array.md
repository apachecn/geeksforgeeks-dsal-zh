# 一个数组的连续元素之间的最小差之和

> 原文:[https://www . geeksforgeeks . org/数组中连续元素之间的最小差之和/](https://www.geeksforgeeks.org/sum-of-minimum-difference-between-consecutive-elements-of-an-array/)

给定一个数组对，其中每一对代表一个范围，任务是找出数组中连续元素之间的最小差的和，其中数组以下面的方式填充:

*   数组的每个元素都位于范围数组中相应索引处给定的范围内。
*   形成的数组中连续元素的差的最终和是最小的。

**例:**

> **输入:**范围[] = {{2，4}、{3，6}、{1，5}、{1，3}、{2，7}}
> **输出:** 0
> 结果为 0 因为选择了数组{3，3，3，3，3，3，3 }
> 那么连续元素的差之和将为
> { |3-3| + |3-3| + |3-3| + |3-3| } = 0 其中最小值。
> **输入:**范围[] = {{1，3}，{2，5}，{6，8}，{1，2}，{2，3}}
> **输出:** 7
> 结果为 7，因为如果选择数组{3，3，6，2，2}则连续元素的差之和将为
> { | 3-3 |+| 6-3 |+| 2-6 |+| 2-2-2

**方法:**为了解决上述问题，采用了贪婪的方法。最初，我们必须以这样一种方式填充数组，即获得的差值之和最小。贪婪的方法如下:

*   如果前一个索引的范围与当前索引的范围相交，则在这种情况下，最小差值将为 0，并存储相交范围的最高值和最低值。
*   如果先前索引的范围的最低值大于当前索引的最高值，那么在这种情况下，最小可能的总和是先前范围的最低值和当前范围中存储的最高值之间的差值。
*   如果先前索引的最高范围低于当前范围的最低值，则最小和是为当前索引存储的最低值和先前索引的最高范围之间的差值。

以下是上述方法的实现:

## C++

```
// C++ program for finding the minimum sum of
// difference between consecutive elements
#include <bits/stdc++.h>
using namespace std;

// function to find minimum sum of
// difference of consecutive element
int solve(pair<int, int> v[], int n)
{
    // ul to store upper limit
    // ll to store lower limit
    int ans, ul, ll;

    // storethe lower range in ll
    // and upper range in ul
    ll = v[0].first;
    ul = v[0].second;

    // initialize the answer with 0
    ans = 0;

    // iterate for all ranges
    for (int i = 1; i < n; i++) {

        // case 1, in this case the difference will be 0
        if ((v[i].first <= ul && v[i].first >= ll) ||
           (v[i].second >= ll && v[i].second <= ul)) {

            // change upper limit and lower limit
            if (v[i].first > ll) {
                ll = v[i].first;
            }
            if (v[i].second < ul) {
                ul = v[i].second;
            }
        }

        // case 2
        else if (v[i].first > ul) {

            // store the difference
            ans += abs(ul - v[i].first);
            ul = v[i].first;
            ll = v[i].first;
        }

        // case 3
        else if (v[i].second < ll) {

            // store the difference
            ans += abs(ll - v[i].second);
            ul = v[i].second;
            ll = v[i].second;
        }
    }
    return ans;
}
// Driver code
int main()
{
    // array of range

    pair<int, int> v[] = { { 1, 3 }, { 2, 5 },
                { 6, 8 }, { 1, 2 }, { 2, 3 } };
    int n = sizeof(v) / sizeof(v[0]);
    cout << solve(v, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding the
// minimum sum of difference
// between consecutive elements
import java.io.*;

class GFG
{

// function to find minimum
// sum of difference of
// consecutive element
static int solve(int[][] v, int n)
{
    // ul to store upper limit
    // ll to store lower limit
    int ans, ul, ll;
    int first = 0;
    int second = 1;

    // storethe lower range
    // in ll and upper range
    // in ul
    ll = v[0][first];
    ul = v[0][second];

    // initialize the
    // answer with 0
    ans = 0;

    // iterate for all ranges
    for (int i = 1; i < n; i++)
    {

        // case 1, in this case
        // the difference will be 0
        if ((v[i][first] <= ul &&
              v[i][first] >= ll) ||
            (v[i][second] >= ll &&
             v[i][second] <= ul))
        {

            // change upper limit
            // and lower limit
            if (v[i][first] > ll)
            {
                ll = v[i][first];
            }
            if (v[i][second] < ul)
            {
                ul = v[i][second];
            }
        }

        // case 2
        else if (v[i][first] > ul)
        {

            // store the difference
            ans += Math.abs(ul - v[i][first]);
            ul = v[i][first];
            ll = v[i][first];
        }

        // case 3
        else if (v[i][second] < ll)
        {

            // store the difference
            ans += Math.abs(ll - v[i][second]);
            ul = v[i][second];
            ll = v[i][second];
        }
    }
    return ans;
}

// Driver code
public static void main(String []args)
{
    // array of range

    int[][] v = {{ 1, 3 }, { 2, 5 },
                 { 6, 8 }, { 1, 2 },
                 { 2, 3 }};
    int n = 5;
    System.out.println(solve(v, n));
}
}

// This code is contributed
// by chandan_jnu
```

## 计算机编程语言

```
# Python program for finding
# the minimum sum of difference
# between consecutive elements

class pair:
    first = 0
    second = 0

    def __init__(self, a, b):
        self.first = a
        self.second = b

# function to find minimum
# sum of difference of
# consecutive element
def solve(v, n):

    # ul to store upper limit
    # ll to store lower limit
    ans = 0; ul = 0; ll = 0;

    # storethe lower range
    # in ll and upper range
    # in ul
    ll = v[0].first
    ul = v[0].second

    # initialize the
    # answer with 0
    ans = 0

    # iterate for all ranges
    for i in range(1, n):

        # case 1, in this case
        # the difference will be 0
        if (v[i].first <= ul and
            v[i].first >= ll) or \
           (v[i].second >= ll and
            v[i].second <= ul):

            # change upper limit
            # and lower limit
            if v[i].first > ll:
                ll = v[i].first

            if v[i].second < ul:
                ul = v[i].second;

        # case 2
        elif v[i].first > ul:

            # store the difference
            ans += abs(ul - v[i].first)
            ul = v[i].first
            ll = v[i].first

        # case 3
        elif v[i].second < ll:

            # store the difference
            ans += abs(ll - v[i].second);
            ul = v[i].second;
            ll = v[i].second;
    return ans

# Driver code

# array of range
v = [pair(1, 3), pair(2, 5),
     pair(6, 8), pair(1, 2),
                 pair(2, 3) ]
n = len(v)
print(solve(v, n))

# This code is contributed
# by Harshit Saini
```

## C#

```
// C# program for finding the
// minimum sum of difference
// between consecutive elements
using System;

class GFG
{
// function to find minimum
// sum of difference of
// consecutive element
static int solve(int[,] v, int n)
{
    // ul to store upper limit
    // ll to store lower limit
    int ans, ul, ll;
    int first = 0;
    int second = 1;

    // storethe lower range
    // in ll and upper range
    // in ul
    ll = v[0, first];
    ul = v[0, second];

    // initialize the
    // answer with 0
    ans = 0;

    // iterate for all ranges
    for (int i = 1; i < n; i++)
    {

        // case 1, in this case
        // the difference will be 0
        if ((v[i, first] <= ul &&
             v[i, first] >= ll) ||
            (v[i, second] >= ll &&
             v[i, second] <= ul))
        {

            // change upper limit
            // and lower limit
            if (v[i, first] > ll)
            {
                ll = v[i, first];
            }
            if (v[i, second] < ul)
            {
                ul = v[i, second];
            }
        }

        // case 2
        else if (v[i, first] > ul)
        {

            // store the difference
            ans += Math.Abs(ul - v[i, first]);
            ul = v[i, first];
            ll = v[i, first];
        }

        // case 3
        else if (v[i, second] < ll)
        {

            // store the difference
            ans += Math.Abs(ll - v[i, second]);
            ul = v[i, second];
            ll = v[i, second];
        }
    }
    return ans;
}

// Driver code
static void Main()
{
    // array of range

    int[,] v = new int[5,2]{ { 1, 3 }, { 2, 5 },
                             { 6, 8 }, { 1, 2 },
                             { 2, 3 } };
    int n = 5;
    Console.WriteLine(solve(v, n));
}
}

// This code is contributed
// by chandan_jnu

```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding the
// minimum sum of difference
// between consecutive elements

// function to find minimum
// sum of difference of
// consecutive element
function solve($v, $n)
{
// ul to store upper limit
// ll to store lower limit
$ans; $ul; $ll;
$first = 0;
$second = 1;

// storethe lower range
// in ll and upper range
// in ul
$ll = $v[0][$first];
$ul = $v[0][$second];

// initialize the
// answer with 0
$ans = 0;

// iterate for all ranges
for ($i = 1; $i <$n; $i++)
{

    // case 1, in this case
    // the difference will be 0
    if (($v[$i][$first] <= $ul and
         $v[$i][$first] >= $ll) or
        ($v[$i][$second] >= $ll and
         $v[$i][$second] <= $ul))
    {

        // change upper limit
        // and lower limit
        if ($v[$i][$first] > $ll)
        {
            $ll = $v[$i][$first];
        }
        if ($v[$i][$second] < $ul)
        {
            $ul = $v[$i][$second];
        }
    }

    // case 2
    else if ($v[$i][$first] > $ul)
    {

        // store the difference
        $ans += abs($ul - $v[$i][$first]);
        $ul = $v[$i][$first];
        $ll = $v[$i][$first];
    }

    // case 3
    else if ($v[$i][$second] < $ll)
    {

        // store the difference
        $ans += abs($ll - $v[$i][$second]);
        $ul = $v[$i][$second];
        $ll = $v[$i][$second];
    }
}
return $ans;
}

// Driver code

// array of range
$v = array(array( 1, 3 ),
           array( 2, 5 ),
           array( 6, 8 ),
           array( 1, 2 ),
           array( 2, 3 ));
$n = 5;
echo(solve($v, $n));

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>

// JavaScript program for finding the
// minimum sum of difference
// between consecutive elements

// function to find minimum
// sum of difference of
// consecutive element
function solve(v, n)
{
    // ul to store upper limit
    // ll to store lower limit
    let ans, ul, ll;
    let first = 0;
    let second = 1;

    // storethe lower range
    // in ll and upper range
    // in ul
    ll = v[0][first];
    ul = v[0][second];

    // initialize the
    // answer with 0
    ans = 0;

    // iterate for all ranges
    for (let i = 1; i < n; i++)
    {

        // case 1, in this case
        // the difference will be 0
        if ((v[i][first] <= ul &&
              v[i][first] >= ll) ||
            (v[i][second] >= ll &&
             v[i][second] <= ul))
        {

            // change upper limit
            // and lower limit
            if (v[i][first] > ll)
            {
                ll = v[i][first];
            }
            if (v[i][second] < ul)
            {
                ul = v[i][second];
            }
        }

        // case 2
        else if (v[i][first] > ul)
        {

            // store the difference
            ans += Math.abs(ul - v[i][first]);
            ul = v[i][first];
            ll = v[i][first];
        }

        // case 3
        else if (v[i][second] < ll)
        {

            // store the difference
            ans += Math.abs(ll - v[i][second]);
            ul = v[i][second];
            ll = v[i][second];
        }
    }
    return ans;
}

// driver code

     let v = [[ 1, 3 ], [ 2, 5 ],
              [ 6, 8 ], [ 1, 2 ],
              [ 2, 3 ]];
    let n = 5;
    document.write(solve(v, n));

</script>
```

**Output:** 

```
7
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)