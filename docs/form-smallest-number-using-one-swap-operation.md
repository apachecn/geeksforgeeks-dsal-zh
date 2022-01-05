# 最多使用一次交换操作形成最小的数字

> 原文:[https://www . geesforgeks . org/form-最小数字使用一个交换操作/](https://www.geeksforgeeks.org/form-smallest-number-using-one-swap-operation/)

给定一个非负数 **num** 。问题是对数字 **num** 最多应用一次交换操作，以使结果是最小可能的数字。该数字可能非常大，因此可以使用字符串类型来存储该数字。输入不包含前导 0，输出也不应该包含前导 0。
**注意:**结果数字中的数字组应该与原始数字中的数字组相同。
**示例:**

```
Input : n = 9625635
Output : 2695635
Swapped the digits 9 and 2.

Input : n = 1205763
Output : 1025763
```

**进场:**
造阵**右转**。 **rightMin[i]** 包含最小数字的索引，它位于 **num[i]** 的右侧，也小于 **num[i]** 。如果不存在这样的数字，则 **rightMin[i]** = -1。现在，检查 **num[0]** 是否有不等于 0 的右小数字。如果是这样，那么用右边的小数字替换第一个数字。否则，遍历 **rightMin[]** 数组从 **i** = 1 到 n-1(其中 **n** 是 **num** 中的总位数)，找到第一个有 **rightMin[i]** 的元素！= -1.执行**交换(num[i]，num[rightMin[i]])** 操作并断开。

## C++

```
// C++ implementation to form the smallest
// number using at most one swap operation
#include <bits/stdc++.h>
using namespace std;

// function to form the smallest number
// using at most one swap operation
string smallestNumber(string num)
{
    int n = num.size();
    int rightMin[n], right;

    // for the rightmost digit, there
    // will be no smaller right digit
    rightMin[n - 1] = -1;

    // index of the smallest right digit
    // till the current index from the
    // right direction
    right = n - 1;

    // traverse the array from second
    // right element up to the left
    // element
    for (int i = n - 2; i >= 1; i--) {
        // if 'num[i]' is greater than
        // the smallest digit encountered
        // so far
        if (num[i] >= num[right])
            rightMin[i] = right;

        else {
            // for cases like 120000654 or 1000000321
            // rightMin will be same for all 0's
            // except the first from last
            if (num[i] == num[i + 1]) {
                rightMin[i] = right;
            }
            else {
                rightMin[i] = -1;
                right = i;
            }
        }
    }

    // special condition for the 1st digit so that
    // it is not swapped with digit '0'
    int small = -1;
    for (int i = 1; i < n; i++)
        if (num[i] != '0') {
            if (small == -1) {
                if (num[i] < num[0])
                    small = i;
            }
            else if (num[i] <= num[small])
                small = i;
        }

    if (small != -1)
        swap(num[0], num[small]);

    else {
        // traverse the 'rightMin[]' array from
        // 2nd digit up to the last digit
        for (int i = 1; i < n; i++) {
            // if for the current digit, smaller
            // right digit exists, then swap it
            // with its smaller right digit and
            // break
            if (rightMin[i] != -1 && num[i] != num[rightMin[i]]) {
                // performing the required
                // swap operation
                swap(num[i], num[rightMin[i]]);
                break;
            }
        }
    }

    // required smallest number
    return num;
}

// Driver program to test above
int main()
{
    string num = "9625635";
    cout << "Smallest number: "
         << smallestNumber(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to form the smallest
// number using at most one swap operation
import java.util.*;
import java.lang.*;

public class GeeksforGeeks {

    // function to form the smallest number
    // using at most one swap operation
    public static String smallestNumber(String str)
    {

        char[] num = str.toCharArray();
        int n = str.length();
        int[] rightMin = new int[n];

        // for the rightmost digit, there
        // will be no smaller right digit
        rightMin[n - 1] = -1;

        // index of the smallest right digit
        // till the current index from the
        // right direction
        int right = n - 1;

        // traverse the array from second
        // right element up to the left
        // element
        for (int i = n - 2; i >= 1; i--) {
            // if 'num[i]' is greater than
            // the smallest digit
            // encountered so far
            if (num[i] > num[right])
                rightMin[i] = right;

            else {
                // there is no smaller right
                // digit for 'num[i]'
                rightMin[i] = -1;

                // update 'right' index
                right = i;
            }
        }

        // special condition for the 1st
        // digit so that it is not swapped
        // with digit '0'
        int small = -1;
        for (int i = 1; i < n; i++)
            if (num[i] != '0') {
                if (small == -1) {
                    if (num[i] < num[0])
                        small = i;
                }
                else if (num[i] < num[small])
                    small = i;
            }

        if (small != -1) {
            char temp;
            temp = num[0];
            num[0] = num[small];
            num[small] = temp;
        }
        else {
            // traverse the 'rightMin[]'
            // array from 2nd digit up
            // to the last digit
            for (int i = 1; i < n; i++) {
                // if for the current digit,
                // smaller right digit exists,
                // then swap it with its smaller
                // right digit and break
                if (rightMin[i] != -1) {
                    // performing the required
                    // swap operation
                    char temp;
                    temp = num[i];
                    num[i] = num[rightMin[i]];
                    num[rightMin[i]] = temp;
                    break;
                }
            }
        }

        // required smallest number
        return (new String(num));
    }

    // driver function
    public static void main(String argc[])
    {
        String num = "9625635";
        System.out.println("Smallest number: " + smallestNumber(num));
    }
}

/*This code is contributed by Sagar Shukla.*/
```

## 蟒蛇 3

```
# Python implementation to form the smallest
# number using at most one swap operation

# function to form the smallest number
# using at most one swap operation
def smallestNumber(num):
    num = list(num)
    n = len(num)
    rightMin = [0]*n
    right = 0

    # for the rightmost digit, there
    # will be no smaller right digit
    rightMin[n-1] = -1;

    # index of the smallest right digit
    # till the current index from the
    # right direction
    right = n-1;

    # traverse the array from second
    # right element up to the left
    # element
    for i in range(n-2, 0, -1):

        # if 'num[i]' is greater than
        # the smallest digit encountered
        # so far
        if num[i] > num[right]:
            rightMin[i] = right

        else:

            # there is no smaller right
            # digit for 'num[i]'
            rightMin[i] = -1

            # update 'right' index
            right = i

    # special condition for the 1st digit so that
    # it is not swapped with digit '0'
    small = -1
    for i in range(1, n):

        if num[i] != '0':

            if small == -1:

                if num[i] < num[0]:
                    small = i

            elif num[i] < num[small]:
                small = i

    if small != -1:
        num[0], num[small] = num[small], num[0]
    else:

        # traverse the 'rightMin[]' array from
        # 2nd digit up to the last digit
        for i in range(1, n):

            # if for the current digit, smaller
            # right digit exists, then swap it
            # with its smaller right digit and
            # break
            if rightMin[i] != -1:

                # performing the required
                # swap operation
                num[i], num[rightMin[i]] = num[rightMin[i]], num[i]
                break

    # required smallest number
    return ''.join(num)

# Driver Code
if __name__ == "__main__":
    num = "9625635"
    print("Smallest number: ", smallestNumber(num))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation to form the smallest
// number using at most one swap operation.
using System;

public class GeeksforGeeks {

    // function to form the smallest number
    // using at most one swap operation
    public static String smallestNumber(String str)
    {

        char[] num = str.ToCharArray();
        int n = str.Length;
        int[] rightMin = new int[n];

        // for the rightmost digit, there
        // will be no smaller right digit
        rightMin[n - 1] = -1;

        // index of the smallest right digit
        // till the current index from the
        // right direction
        int right = n - 1;

        // traverse the array from second
        // right element up to the left
        // element
        for (int i = n - 2; i >= 1; i--) {

            // if 'num[i]' is greater than
            // the smallest digit
            // encountered so far
            if (num[i] > num[right])
                rightMin[i] = right;

            else {

                // there is no smaller right
                // digit for 'num[i]'
                rightMin[i] = -1;

                // update 'right' index
                right = i;
            }
        }

        // special condition for the 1st
        // digit so that it is not swapped
        // with digit '0'
        int small = -1;
        for (int i = 1; i < n; i++)
            if (num[i] != '0') {
                if (small == -1) {
                    if (num[i] < num[0])
                        small = i;
                }
                else if (num[i] < num[small])
                    small = i;
            }

        if (small != -1) {
            char temp;
            temp = num[0];
            num[0] = num[small];
            num[small] = temp;
        }
        else {

            // traverse the 'rightMin[]'
            // array from 2nd digit up
            // to the last digit
            for (int i = 1; i < n; i++) {

                // if for the current digit,
                // smaller right digit exists,
                // then swap it with its smaller
                // right digit and break
                if (rightMin[i] != -1) {
                    // performing the required
                    // swap operation
                    char temp;
                    temp = num[i];
                    num[i] = num[rightMin[i]];
                    num[rightMin[i]] = temp;
                    break;
                }
            }
        }

        // required smallest number
        return (new String(num));
    }

    // Driver code
    public static void Main()
    {
        String num = "9625635";
        Console.Write("Smallest number: " + smallestNumber(num));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// form the smallest number
// using at most one swap
// operation

// function to form the
// smallest number using
// at most one swap operation
function smallestNumber($num)
{
    $n = strlen($num);
    $rightMin = array_fill(0, $n, -1);
    $right;

    // for the rightmost digit,
    // there will be no smaller
    // right digit
    $rightMin[$n - 1] = -1;

    // index of the smallest
    // right digit till the
    // current index from the
    // right direction
    $right = $n - 1;

    // traverse the array from
    // second right element up
    // to the left element
    for ($i = $n - 2; $i >= 1; $i--)
    {
        // if 'num[i]' is greater
        // than the smallest digit 
        // encountered so far
        if ($num[$i] > $num[$right])
            $rightMin[$i] = $right;

        else
        {
            // there is no smaller
            // right digit for 'num[i]'
            $rightMin[$i] = -1;

            // update 'right' index
            $right = $i;
        }
    }

    // special condition for
    // the 1st digit so that
    // it is not swapped with
    // digit '0'
    $small = -1;
    for ($i = 1; $i < $n; $i++)
        if ($num[$i] != '0')
        {
            if ($small == -1)
            {
                if ($num[$i] < $num[0])
                    $small = $i;
            }
            else if ($num[$i] < $num[$small])
                $small = $i;                
        }

    if ($small != -1)
    {
        $tmp = $num[0];
        $num[0] = $num[$small];
        $num[$small] = $tmp;
    }
    else
    {
        // traverse the 'rightMin[]'
        // array from 2nd digit up
        // to the last digit
        for ($i = 1; $i < $n; $i++)
        {
            // if for the current
            // digit, smaller right
            // digit exists, then
            // swap it with its
            // smaller right digit
            // and break
            if ($rightMin[$i] != -1)
            {
                // performing the required
                // swap operation
                $tmp = $num[$i];
                $num[$i] = $num[$rightMin[$i]];
                $num[$rightMin[$i]] = $tmp;
                break;
            }
        }
    }

    // required smallest number
    return $num;
}

// Driver Code
$num = "9625635";
echo "Smallest number: " .
     smallestNumber($num);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to form the smallest
// number using at most one swap operation

// function to form the smallest number
// using at most one swap operation
function smallestNumber(num)
{
    var n = num.length;
    var rightMin = Array(n).fill(0), right;

    // for the rightmost digit, there
    // will be no smaller right digit
    rightMin[n - 1] = -1;

    // index of the smallest right digit
    // till the current index from the
    // right direction
    right = n - 1;

    // traverse the array from second
    // right element up to the left
    // element
    for (var i = n - 2; i >= 1; i--) {
        // if 'num[i]' is greater than
        // the smallest digit encountered
        // so far
        if (num[i].charCodeAt(0) >= num[right].charCodeAt(0))
            rightMin[i] = right;

        else {
            // for cases like 120000654 or 1000000321
            // rightMin will be same for all 0's
            // except the first from last
            if (num[i] == num[i + 1]) {
                rightMin[i] = right;
            }
            else {
                rightMin[i] = -1;
                right = i;
            }
        }
    }

    // special condition for the 1st digit so that
    // it is not swapped with digit '0'
    var small = -1;
    for (var i = 1; i < n; i++)
        if (num[i] != '0') {
            if (small == -1) {
                if (num[i].charCodeAt(0) < num[0].charCodeAt(0))
                    small = i;
            }
            else if (num[i].charCodeAt(0) <= num[small].charCodeAt(0))
                small = i;
        }

    if (small != -1)
    {
        var tmp = num[0]
        num[0] = num[small]
        num[small] = tmp
    }

    else {
        // traverse the 'rightMin[]' array from
        // 2nd digit up to the last digit
        for (var i = 1; i < n; i++) {
            // if for the current digit, smaller
            // right digit exists, then swap it
            // with its smaller right digit and
            // break
            if (rightMin[i] != -1 && num[i] != num[rightMin[i]]) {
                // performing the required
                // swap operation
                var tmp = num[i]
                num[i]= num[rightMin[i]];
                num[rightMin[i]] = tmp
                break;
            }
        }
    }

    // required smallest number
    return num.join('');
}

// Driver program to test above
var num = "9625635".split('');
document.write( "Smallest number: "
     + smallestNumber(num));

// This code is contributed by rrrtnx.
</script>   
```

**输出:**

```
Smallest number: 2695635
```

**时间复杂度:** O(n)，其中 **n** 为总位数。
**辅助空格:** O(n)，其中 **n** 为总位数。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。