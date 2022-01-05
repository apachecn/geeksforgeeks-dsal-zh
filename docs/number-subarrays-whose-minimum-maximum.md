# 最小值和最大值相同的子阵数量

> 原文:[https://www . geesforgeks . org/number-subarrays-what-minimum-maximum/](https://www.geeksforgeeks.org/number-subarrays-whose-minimum-maximum/)

给定 n 个整数的数组，求其最小和最大元素相同的子数组的个数。子阵列被定义为连续元素的非空序列。

**示例:**

```
Input: 2 3 1 1 
Output: 5
Explanation: The subarrays are (2), 
(3), (1), (1) and (1, 1) 

Input: 2 4 5 3 3 3
Output: 9
Explanation: The subarrays are (2), (4), 
(5), (3), (3, 3), (3, 3, 3), (3), (3, 3) and 
(3) 
```

首先要观察的是，只有那些所有元素都相同的子阵才会有相同的最小值和最大值。具有不同的元素显然意味着不同的最小值和最大值。因此，我们只需要计算连续的相同元素的数量**(比如 d)** ，然后通过组合公式我们得到子阵列的数量为–

> 有 d 个元素的子阵列的数量= (d * (d+1) / 2)
> 其中 d 是连续的相同元素的数量。

我们从 1-n 开始遍历，然后从 I+1 遍历到 n，然后找到连续的相同元素的数目，然后在结果中加上不可能的子阵列。

## C++

```
// CPP program to count number of subarrays
// having same minimum and maximum.
#include <bits/stdc++.h>
using namespace std;

// calculate the no of contiguous subarrays
// which has same minimum and maximum
int calculate(int a[], int n)
{
    // stores the answer
    int ans = 0;

    // loop to traverse from 0-n
    for (int i = 0; i < n; i++) {

        // start checking subarray from next element
        int r = i + 1;

        // traverse for finding subarrays
        for (int j = r; j < n; j++) {

            // if the elements are same then
            // we check further and keep a count
            // of same numbers in 'r'
            if (a[i] == a[j])
                r += 1;
            else
                break;
        }

        // the no of elements in between r and i
        // with same elements.
        int d = r - i;

        // the no of subarrays that can be formed
        // between i and r
        ans += (d * (d + 1) / 2);

        // again start checking from the next index
        i = r - 1;
    }

    // returns answer
    return ans;
}

// drive program to test the above function
int main()
{
    int a[] = { 2, 4, 5, 3, 3, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << calculate(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of subarrays
// having same minimum and maximum.

class Subarray
{
    // calculate the no of contiguous subarrays
    // which has same minimum and maximum
    static int calculate(int a[], int n)
    {
        // stores the answer
        int ans = 0;

        // loop to traverse from 0-n
        for (int i = 0; i < n; i++) {

            // start checking subarray from
            // next element
            int r = i + 1;

            // traverse for finding subarrays
            for (int j = r; j < n; j++) {

                // if the elements are same then
                // we check further and keep a
                // count of same numbers in 'r'
                if (a[i] == a[j])
                    r += 1;
                else
                    break;
            }

            // the no of elements in between r
            // and i with same elements.
            int d = r - i;

            // the no. of subarrays that can be
            // formed between i and r
            ans += (d * (d + 1) / 2);

            // again start checking from the next
            // index
            i = r - 1;
        }

        // returns answer
        return ans;
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
    int a[] = {  2, 4, 5, 3, 3, 3 };
    System.out.println(calculate(a, a.length));
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to count
# number of subarrays having
# same minimum and maximum.

# calculate the no of contiguous
# subarrays which has same
# minimum and maximum
def calculate(a, n):

    # stores the answer
    ans = 0;
    i = 0;

    # loop to traverse from 0-n
    while(i < n):

        # start checking subarray
        # from next element
        r = i + 1;

        # traverse for
        # finding subarrays
        for j in range(r, n):

            # if the elements are same
            # then we check further
            # and keep a count of same
            # numbers in 'r'
            if (a[i] == a[j]):
                r = r + 1;
            else:
                break;

        # the no of elements in
        # between r and i with
        # same elements.
        d = r - i;

        # the no of subarrays that
        # can be formed between i and r
        ans = ans + (d * (d + 1) / 2);

        # again start checking
        # from the next index
        i = r - 1;
        i = i + 1;

    # returns answer
    return int(ans);

# Driver Code
a = [ 2, 4, 5, 3, 3, 3 ];
n = len(a);
print(calculate(a, n));

# This code is contributed by mits
```

## C#

```
// Program to count number
// of subarrays having same
// minimum and maximum.
using System;

class Subarray {
    // calculate the no of contiguous
    // subarrays which has the same
    // minimum and maximum
    static int calculate(int[] a, int n)
    {
        // stores the answer
        int ans = 0;

        // loop to traverse from 0-n
        for (int i = 0; i < n; i++) {

            // start checking subarray
            // from next element
            int r = i + 1;

            // traverse for finding subarrays
            for (int j = r; j < n; j++) {

                // if the elements are same then
                // we check further and keep a
                // count of same numbers in 'r'
                if (a[i] == a[j])
                    r += 1;
                else
                    break;
            }

            // the no of elements in between
            // r and i with same elements.
            int d = r - i;

            // the no. of subarrays that can
            // be formed between i and r
            ans += (d * (d + 1) / 2);

            // again start checking from
            // the next index
            i = r - 1;
        }

        // returns answer
        return ans;
    }

    // Driver program
    public static void Main()
    {
        int[] a = { 2, 4, 5, 3, 3, 3 };
        Console.WriteLine(calculate(a, a.Length));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of subarrays having same
// minimum and maximum.

// calculate the no of contiguous
// subarrays which has same minimum
// and maximum
function calculate($a, $n)
{
    // stores the answer
    $ans = 0;

    // loop to traverse from 0-n
    for ($i = 0; $i < $n; $i++)
    {

        // start checking subarray
        // from next element
        $r = $i + 1;

        // traverse for finding subarrays
        for ($j = $r; $j < $n; $j++)
        {

            // if the elements are same
            // then we check further and
            // keep a count of same numbers
            // in 'r'
            if ($a[$i] == $a[$j])
                $r += 1;
            else
                break;
        }

        // the no of elements in between
        //  r and i with same elements.
        $d = $r - $i;

        // the no of subarrays that
        // can be formed between i and r
        $ans += ($d * ($d + 1) / 2);

        // again start checking
        // from the next index
        $i = $r - 1;
    }

    // returns answer
    return $ans;
}

// Driver Code
$a = array( 2, 4, 5, 3, 3, 3 );
$n = count($a);
echo calculate($a, $n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// JavaScript program to count number of subarrays
// having same minimum and maximum.

    // calculate the no of contiguous subarrays
    // which has same minimum and maximum
    function calculate(a, n)
    {
        // stores the answer
        let ans = 0;

        // loop to traverse from 0-n
        for (let i = 0; i < n; i++) {

            // start checking subarray from
            // next element
            let r = i + 1;

            // traverse for finding subarrays
            for (let j = r; j < n; j++) {

                // if the elements are same then
                // we check further and keep a
                // count of same numbers in 'r'
                if (a[i] == a[j])
                    r += 1;
                else
                    break;
            }

            // the no of elements in between r
            // and i with same elements.
            let d = r - i;

            // the no. of subarrays that can be
            // formed between i and r
            ans += (d * (d + 1) / 2);

            // again start checking from the next
            // index
            i = r - 1;
        }

        // returns answer
        return ans;
    }

// Driver Code

    let a = [ 2, 4, 5, 3, 3, 3 ];
    document.write(calculate(a, a.length));

</script>
```

**输出:**

```
9
```

**时间复杂度:** O(n^2)
**辅助空间:** O(1)
本文由[**Raja vikramatitya(Raj)**](https://www.facebook.com/raja.vikramaditya.7)投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。