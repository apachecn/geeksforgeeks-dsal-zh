# 最多使用一次交换操作形成最大数量

> 原文:[https://www . geesforgeks . org/form-最大数量使用一个交换操作/](https://www.geeksforgeeks.org/form-largest-number-using-one-swap-operation/)

给定一个非负数 **num** 。问题是对数字 **num** 最多应用一次交换操作，以使结果是最大可能的数字。该数字可能非常大，因此可以使用字符串类型来存储该数字。

**示例:**

```
Input : n = 8725634
Output : 8765234
Swapped the digits 2 and 6.

Input : n = 54321
Output : 54321
No swapping of digits required.
```

创建一个数组 **rightMax[]** 。 **rightMax[i]** 包含位于 **num[i]** 右侧且大于 **num[i]** 的最大数字的索引。如果不存在这样的数字，则 **rightMax[i]** = -1。现在，遍历 **rightMax[]** 数组，从 **i** = 0 到 n-1(其中 **n** 是 **num** 中的总位数)，找到第一个有 **rightMax[i]** 的元素！= -1.执行**交换(num[i]，num[rightMax[i]])** 操作并断开。

## C++

```
// C++ implementation to form the largest number
// by applying atmost one swap operation
#include <bits/stdc++.h>
using namespace std;

// function to form the largest number by
// applying atmost one swap operation
string largestNumber(string num)
{
    int n = num.size();
    int rightMax[n], right;

    // for the rightmost digit, there
    // will be no greater right digit
    rightMax[n - 1] = -1;

    // index of the greatest right digit till the
    // current index from the right direction
    right = n - 1;

    // traverse the array from second right element
    // up to the left element
    for (int i = n - 2; i >= 0; i--) {

        // if 'num[i]' is less than the greatest digit
        // encountered so far
        if (num[i] < num[right])
            rightMax[i] = right;

        // else
        else {
            // there is no greater right digit
            // for 'num[i]'
            rightMax[i] = -1;

            // update 'right' index
            right = i;
        }
    }

    // traverse the 'rightMax[]' array from left to right
    for (int i = 0; i < n; i++) {

        // if for the current digit, greater right digit exists
        // then swap it with its greater right digit and break
        if (rightMax[i] != -1) {

            // performing the required swap operation
            swap(num[i], num[rightMax[i]]);
            break;
        }
    }

    // required largest number
    return num;
}

// Driver program to test above
int main()
{
    string num = "8725634";
    cout << "Largest number:"
         << largestNumber(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation to form the largest number
//by applying atmost one swap operation
public class GFG
{
    // function to form the largest number by
    // applying atmost one swap operation
    static String largestNumber(String num)
    {
        int n = num.length();
        int right;
        int rightMax[] = new int[n];

        // for the rightmost digit, there
        // will be no greater right digit
        rightMax[n - 1] = -1;

        // index of the greatest right digit
        // till the current index from the
        // right direction
        right = n - 1;

        // traverse the array from second right
        // element up to the left element
        for (int i = n - 1; i >= 0 ; i--)
        {
            // if 'num.charAt(i)' is less than the
            // greatest digit encountered so far
            if (num.charAt(i) < num.charAt(right))
                rightMax[i] = right;

            else
            {
                // there is no greater right digit
                // for 'num.charAt(i)'
                rightMax[i] = -1;

                // update 'right' index
                right = i;
            }
        }

        // traverse the 'rightMax[]' array from
        // left to right
        for (int i = 0; i < n; i++)
        {

            // if for the current digit, greater
            // right digit exists then swap it
            // with its greater right digit and break
            if (rightMax[i] != -1)
            {
                // performing the required swap operation
                num = swap(num,i,rightMax[i]);
                break;
            }
        }

        // required largest number
        return num;
    }

    // Utility method to swap two characters
    // in a String
    static String swap(String num, int i, int j)
    {
        StringBuilder sb= new StringBuilder(num);
        sb.setCharAt(i, num.charAt(j));
        sb.setCharAt(j, num.charAt(i));
        return sb.toString();

    }

    //Driver Function to test above Function
    public static void main(String[] args)
    {
        String num = "8725634";
        System.out.println("Largest Number : " +
                              largestNumber(num));
    }

}
//This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python implementation to form the largest number
# by applying atmost one swap operation

# function to form the largest number by
# applying atmost one swap operation
def largestNumber(num):
    n = len(num)
    rightMax = [0 for i in range(n)]

    # for the rightmost digit, there
    # will be no greater right digit
    rightMax[n - 1] = -1

    # index of the greatest right digit till the
    # current index from the right direction
    right = n - 1

    # traverse the array from second right element
    # up to the left element
    i = n - 2
    while i >= 0:

        # if 'num[i]' is less than the greatest digit
        # encountered so far
        if (num[i] < num[right]):
            rightMax[i] = right

        # else
        else:
            # there is no greater right digit
            # for 'num[i]'
            rightMax[i] = -1

            # update 'right' index
            right = i
        i -= 1

    # traverse the 'rightMax[]' array from left to right
    for i in range(n):

        # if for the current digit, greater right digit exists
        # then swap it with its greater right digit and break
        if (rightMax[i] != -1):

            # performing the required swap operation
            t = num[i]

            num[i] = num[rightMax[i]]
            num[rightMax[i]] = t
            break

    # required largest number
    return num

# Driver program to test above
num = "8725634"
li = [i for i in num]
print "Largest number: "
li = largestNumber(li)
for i in li:
    print i,
print

#This code is contributed by Sachin Bisht
```

## C#

```
// C# implementation to form the largest number
// by applying atmost one swap operation

using System;
using System.Text;
public class GFG
{
    // function to form the largest number by
    // applying atmost one swap operation
    static String largestNumber(String num)
    {
        int n = num.Length;
        int right;
        int[] rightMax = new int[n];

        // for the rightmost digit, there
        // will be no greater right digit
        rightMax[n - 1] = -1;

        // index of the greatest right digit
        // till the current index from the
        // right direction
        right = n - 1;

        // traverse the array from second right
        // element up to the left element
        for (int i = n - 1; i >= 0 ; i--)
        {
            // if 'num.charAt(i)' is less than the
            // greatest digit encountered so far
            if (num[i] < num[right])
                rightMax[i] = right;

            else
            {
                // there is no greater right digit
                // for 'num.charAt(i)'
                rightMax[i] = -1;

                // update 'right' index
                right = i;
            }
        }

        // traverse the 'rightMax[]' array from
        // left to right
        for (int i = 0; i < n; i++)
        {

            // if for the current digit, greater
            // right digit exists then swap it
            // with its greater right digit and break
            if (rightMax[i] != -1)
            {
                // performing the required swap operation
                num = swap(num,i,rightMax[i]);
                break;
            }
        }

        // required largest number
        return num;
    }

    // Utility method to swap two characters
    // in a String
    static String swap(String num, int i, int j)
    {
        StringBuilder sb= new StringBuilder(num);
        sb[i]=num[j];
        sb[j]=num[i];
        return sb.ToString();

    }

    //Driver Function to test above Function
    public static void Main()
    {
        String num = "8725634";
        Console.WriteLine("Largest Number : " +largestNumber(num));
    }

}
//This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to form the
// largest number by applying atmost
// one swap operation

// function to form the largest number by
// applying atmost one swap operation
function largestNumber($num)
{
    $n = strlen($num);
    $rightMax[$n] = array(0);
    $right;

    // for the rightmost digit, there
    // will be no greater right digit
    $rightMax[$n - 1] = -1;

    // index of the greatest right
    // digit till the current index
    // from the right direction
    $right = $n - 1;

    // traverse the array from second
    // right element up to the left element
    for ($i = $n - 2; $i >= 0; $i--)
    {

        // if 'num[i]' is less than the
        // greatest digit encountered so far
        if ($num[$i] < $num[$right])
            $rightMax[$i] = $right;

        // else
        else
        {
            // there is no greater right
            // digit for 'num[i]'
            $rightMax[$i] = -1;

            // update 'right' index
            $right = $i;
        }
    }

    // traverse the 'rightMax[]'
    // array from left to right
    for ($i = 0; $i < $n; $i++)
    {

        // if for the current digit, greater
        // right digit exists then swap it
        // with its greater right digit and break
        if ($rightMax[$i] != -1)
        {

            // performing the required swap operation
            list($num[$i],
                 $num[$rightMax[$i]]) = array($num[$rightMax[$i]],
                                              $num[$i]);

            break;
        }
    }

    // required largest number
    return $num;
}

// Driver Code
$num = "8725634";
echo "Largest number: ",
     largestNumber($num);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript implementation to form the largest number
// by applying atmost one swap operation

// function to form the largest number by
// applying atmost one swap operation
function largestNumber(num)
{
    var n = num.length;
    var rightMax = Array(n), right;

    // for the rightmost digit, there
    // will be no greater right digit
    rightMax[n - 1] = -1;

    // index of the greatest right digit till the
    // current index from the right direction
    right = n - 1;

    // traverse the array from second right element
    // up to the left element
    for (var i = n - 2; i >= 0; i--) {

        // if 'num[i]' is less than the greatest digit
        // encountered so far
        if (num[i] < num[right])
            rightMax[i] = right;

        // else
        else {
            // there is no greater right digit
            // for 'num[i]'
            rightMax[i] = -1;

            // update 'right' index
            right = i;
        }
    }

    // traverse the 'rightMax[]' array from left to right
    for (var i = 0; i < n; i++) {

        // if for the current digit, greater right digit exists
        // then swap it with its greater right digit and break
        if (rightMax[i] != -1) {

            // performing the required swap operation
            var tmp = num[i];
            num[i] = num[rightMax[i]];
            num[rightMax[i]] = tmp
            break;
        }
    }

    // required largest number
    return num.join('');
}

// Driver program to test above
var num = "8725634".split('');
document.write( "Largest number:"
      + largestNumber(num));

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
Largest number: 8765234
```

**时间复杂度:** O(n)，其中 **n** 为总位数。
**辅助空格:** O(n)，其中 **n** 为总位数。

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。