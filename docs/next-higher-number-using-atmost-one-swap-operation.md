# 使用 atmost 一次交换操作的下一个更高的数字

> 原文:[https://www . geesforgeks . org/next-higher-number-use-Atmos-one-swap-operation/](https://www.geeksforgeeks.org/next-higher-number-using-atmost-one-swap-operation/)

给定一个非负数 **num** 。问题是通过在**号**中任意两位数字之间的交换操作上执行 atmost，找到大于**号**的最小数字。如果无法形成更大的数字，则打印“不可能”。
这个数字可能非常大，甚至可能不适合 long long int。
**示例:**

```
Input : num = "218765"
Output : 258761
We swap 5 and 1 to get the smallest
number greater than 'num'

Input : num = "541322"
Output : 542312
```

**逼近:**首先找到最右边的数字的索引，这个数字比它大，并且在它的右边。让它的指数为 **ind** 。现在，在索引 **ind** 找到比该数字大的最小数字的索引，并对它。让它的指数为**变大变小**。最后交换索引 **ind** 和 **greatSmallDgt** 处的数字。如果**编号**的数字是按降序排列的，则打印“不可能”。

## C++

```
// C++ implementation to find the next higher number
// using atmost one swap operation
#include <bits/stdc++.h>

using namespace std;

// function to find the next higher number
// using atmost one swap operation
string nxtHighUsingAtMostOneSwap(string num)
{
    int l = num.size();

    // to store the index of the largest digit
    // encountered so far from the right
    int posRMax = l - 1;

    // to store the index of rightmost digit
    // which has a digit greater to it on its
    // right side
    int index = -1;

    // finding the 'index' of rightmost digit
    // which has a digit greater to it on its
    // right side
    for (int i = l - 2; i >= 0; i--) {
        if (num[i] >= num[posRMax])
            posRMax = i;

        // required digit found, store its
        // 'index' and break
        else {
            index = i;
            break;
        }
    }

    // if no such digit is found which has a
    // larger digit on its right side
    if (index == -1)
        return "Not Possible";

    // to store the index of the smallest digit
    // greater than the digit at 'index' and right
    // to it
    int greatSmallDgt = -1;

    // finding the index of the smallest digit
    // greater than the digit at 'index'
    // and right to it
    for (int i = l - 1; i > index; i--) {
        if (num[i] > num[index]) {
            if (greatSmallDgt == -1)
                greatSmallDgt = i;
            else if (num[i] <= num[greatSmallDgt])
                greatSmallDgt = i;
        }
    }

    // swapping the digits
    char temp = num[index];
    num[index] = num[greatSmallDgt];
    num[greatSmallDgt] = temp;

    // required number
    return num;
}

// Driver program to test above
int main()
{
    string num = "218765";
    cout << "Original number: " << num << endl;
    cout << "Next higher number: "
         << nxtHighUsingAtMostOneSwap(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation to find the next higher
// number using atmost one swap operation
class GFG{

    // function to find the next higher number
    // using atmost one swap operation
    static String nextHighUsingAtMostOneSwap(String st)
    {
        char num[] = st.toCharArray();
        int l = num.length;

        // to store the index of the largest digit
        // encountered so far from the right
        int posRMax = l - 1;

        // to store the index of rightmost digit
        // which has a digit greater to it on its
        // right side
        int index = -1;

        // finding the 'index' of rightmost digit
        // which has a digit greater to it on its
        // right side
        for (int i = l - 2; i >= 0; i--)
        {
            if (num[i] >= num[posRMax])
                posRMax = i;

            // required digit found, store its
            // 'index' and break   
            else
            {
                index = i;
                break;
            }   
        }

        // if no such digit is found which has a
        // larger digit on its right side
        if (index == -1)
            return "Not Possible";

        // to store the index of the smallest digit
        // greater than the digit at 'index' and
        // right to it   
        int greatSmallDgt = -1;

        // finding the index of the smallest
        // digit greater than the digit at
        // 'index' and right to it   
        for (int i = l - 1; i > index; i--)   
        {
            if (num[i] > num[index])
            {
                if (greatSmallDgt == -1)
                    greatSmallDgt = i;
                else if (num[i] <= num[greatSmallDgt])   
                    greatSmallDgt = i;
            }
        }

        // swapping the digits
        char temp = num[index];
         num[index] = num[greatSmallDgt];
        num[greatSmallDgt] = temp;

        // required number
        return (String.valueOf(num));
    }

    // Driver program to test above
    public static void main(String[] args)
    {
        String num = "218765";
        System.out.println("Original number: "
                           + num );
        System.out.println("Next higher number: "
              + nextHighUsingAtMostOneSwap(num));
    }

}
/*This code is contributed by Nikita Tiwari*/
```

## 计算机编程语言

```
# Python implementation to find the next higher
# number using atmost one swap operation

# function to find the next higher number
# using atmost one swap operation
def nextHighUsingAtMostOneSwap(st) :
    num = list (st)
    l = len(num)

    # to store the index of the largest digit
    # encountered so far from the right
    posRMax = l - 1

    # to store the index of rightmost digit
    # which has a digit greater to it on its
    # right side
    index = -1

    # finding the 'index' of rightmost digit
    # which has a digit greater to it on its
    # right side
    i = l - 2
    while i >= 0 :
        if (num[i] >= num[posRMax]) :
            posRMax = i

        # required digit found, store its
        # 'index' and break   
        else :
            index = i
            break
        i = i - 1

    # if no such digit is found which has
    # a larger digit on its right side
    if (index == -1) :
        return "Not Possible"

    # to store the index of the smallest digit
    # greater than the digit at 'index' and
    # right to it   
    greatSmallDgt = -1

    # finding the index of the smallest digit
    # greater than the digit at 'index'
    # and right to it   
    i = l - 1
    while i > index :
        if (num[i] > num[index]) :
            if (greatSmallDgt == -1) :
                greatSmallDgt = i
            elif (num[i] <= num[greatSmallDgt]) :
                greatSmallDgt = i

        i = i - 1

    # swapping the digits
    temp = num[index]
    num[index] = num[greatSmallDgt];
    num[greatSmallDgt] = temp;

    # required number
    return ''.join(num)

# Driver program to test above
num = "218765"
print"Original number: " , num
print "Next higher number: ", nextHighUsingAtMostOneSwap(num)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# implementation to find the
// next higher number using atmost
// one swap operation
using System;

class GFG
{

// function to find the next
// higher number using atmost
// one swap operation
static String nextHighUsingAtMostOneSwap(String st)
{
    char[] num = st.ToCharArray();
    int l = num.Length;

    // to store the index of the
    // largest digit encountered
    // so far from the right
    int posRMax = l - 1;

    // to store the index of rightmost
    // digit which has a digit greater
    // to it on its right side
    int index = -1;

    // finding the 'index' of rightmost
    // digit which has a digit greater
    // to it on its right side
    for (int i = l - 2; i >= 0; i--)
    {
        if (num[i] >= num[posRMax])
            posRMax = i;

        // required digit found, store
        // its 'index' and break
        else
        {
            index = i;
            break;
        }
    }

    // if no such digit is found
    // which has a larger digit
    // on its right side
    if (index == -1)
        return "Not Possible";

    // to store the index of the
    // smallest digit greater than
    // the digit at 'index' and
    // right to it
    int greatSmallDgt = -1;

    // finding the index of the 
    // smallest digit greater
    // than the digit at 'index'
    // and right to it
    for (int i = l - 1; i > index; i--)
    {
        if (num[i] > num[index])
        {
            if (greatSmallDgt == -1)
                greatSmallDgt = i;
            else if (num[i] <= num[greatSmallDgt])
                greatSmallDgt = i;
        }
    }

    // swapping the digits
    char temp = num[index];
    num[index] = num[greatSmallDgt];
    num[greatSmallDgt] = temp;

    string res = new string(num);

    // required number
    return res;
}

// Driver Code
public static void Main()
{
    String num = "218765";
    Console.WriteLine("Original number: "
                                 + num );
    Console.WriteLine("Next higher number: "
         + nextHighUsingAtMostOneSwap(num));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// find the next higher
// number using atmost
// one swap operation

// function to find the
// next higher number
// using atmost one swap
// operation
function nxtHighUsingAtMostOneSwap($num)
{
    $l = strlen($num);

    // to store the index of
    // the largest digit
    // encountered so far
    // from the right
    $posRMax = $l - 1;

    // to store the index of
    // rightmost digit which
    // has a digit greater to
    // it on its right side
    $index = -1;

    // finding the 'index' of
    // rightmost digit which
    // has a digit greater to
    // it on its right side
    for ($i = $l - 2; $i >= 0; $i--)
    {
        if ($num[$i] >= $num[$posRMax])
            $posRMax = $i;

        // required digit
        // found, store its
        // 'index' and break
        else
        {
            $index = $i;
            break;
        }
    }

    // if no such digit is
    // found which has a
    // larger digit on its
    // right side
    if ($index == -1)
        return "Not Possible";

    // to store the index of
    // the smallest digit
    // greater than the digit
    // at 'index' and right
    // to it
    $greatSmallDgt = -1;

    // finding the index of
    // the smallest digit
    // greater than the digit
    // at 'index' and right to it
    for ($i = $l - 1;
         $i > $index; $i--)
    {
        if ($num[$i] > $num[$index])
        {
            if ($greatSmallDgt == -1)
                $greatSmallDgt = $i;
            else if ($num[$i] <= $num[$greatSmallDgt])
                $greatSmallDgt = $i;
        }
    }

    // swapping the digits
    $temp = $num[$index];
    $num[$index] = $num[$greatSmallDgt];
    $num[$greatSmallDgt] = $temp;

    // required number
    return $num;
}

// Driver Code
$num = "218765";
echo "Original number: ".$num."\n";
echo "Next higher number: ".
      nxtHighUsingAtMostOneSwap($num);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript implementation to find the next higher
// number using atmost one swap operation

// function to find the next higher number
// using atmost one swap operation
function nextHighUsingAtMostOneSwap(st)
{
    var num = st.split('');
    var l = num.length;

    // to store the index of the largest digit
    // encountered so far from the right
    var posRMax = l - 1;

    // to store the index of rightmost digit
    // which has a digit greater to it on its
    // right side
    var index = -1;

    // finding the 'index' of rightmost digit
    // which has a digit greater to it on its
    // right side
    for (var i = l - 2; i >= 0; i--)
    {
        if (num[i] >= num[posRMax])
            posRMax = i;

        // required digit found, store its
        // 'index' and break   
        else
        {
            index = i;
            break;
        }   
    }

    // if no such digit is found which has a
    // larger digit on its right side
    if (index == -1)
        return "Not Possible";

    // to store the index of the smallest digit
    // greater than the digit at 'index' and
    // right to it   
    var greatSmallDgt = -1;

    // finding the index of the smallest
    // digit greater than the digit at
    // 'index' and right to it   
    for (var i = l - 1; i > index; i--)   
    {
        if (num[i] > num[index])
        {
            if (greatSmallDgt == -1)
                greatSmallDgt = i;
            else if (num[i] <= num[greatSmallDgt])   
                greatSmallDgt = i;
        }
    }

    // swapping the digits
    var temp = num[index];
     num[index] = num[greatSmallDgt];
    num[greatSmallDgt] = temp;

    // required number
    return (num.join(''));
}

// Driver program to test above
var num = "218765";
document.write("Original number: "
                   + num );
document.write("<br>Next higher number: "
      + nextHighUsingAtMostOneSwap(num));

// This code contributed by shikhasingrajput
</script>
```

**输出:**

```
Original number: 218765
Next higher number: 258761
```

**时间复杂度:** O(n)，其中 **n** 是 **num** 中的位数。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。