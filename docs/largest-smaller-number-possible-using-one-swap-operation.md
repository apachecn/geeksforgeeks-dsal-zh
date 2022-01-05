# 仅使用一次交换操作的最大可能较小数量

> 原文:[https://www . geesforgeks . org/最大-较小-可能数量-使用一个-交换-操作/](https://www.geeksforgeeks.org/largest-smaller-number-possible-using-one-swap-operation/)

给定一个字符串形式的非负数 N。任务是对数字 N 最多应用一次交换操作，使得结果小于 N，并且是最大的这样的数字。
**例:**

```
Input :str = "12435"
Output : 12345
Although the number 12354 will be the 
largest smaller number from 12435\. But 
it is not possible to make it using only
one swap. So swap 4 and 3 and get 12345.

Input : 34123567
Output : 33124567
We swap 4 with 3 (on its right side) to
get the largest smaller number.

Input : str = " 12345"
Output : -1
Digits are in increasing order. So it 
is not possible to make a smaller number 
from it.
```

[推荐:请先在“<u>”上解，再进行解。</u>](https://practice.geeksforgeeks.org/problems/previous-number-in-one-swap/0)

1.  <u>从右边开始遍历，找到一个大于右边数字之一的数字 is。让这个索引这样的元素成为索引。</u>
2.  <u>然后在 str[index]的右边找到另一个索引，它的最大值小于 str[index]。</u>
3.  <u>交换上面的两个值。</u>

## <u>C++</u>

```
// C++ program to find the largest smaller 
// number by swapping one digit.
#include <bits/stdc++.h>
using namespace std;

// Returns largest possible number with one
// swap such that the number is smaller than
// str. It is assumed that there are leading
// 0s.
string prevNum(string str)
{
    int len = str.length();
    int index = -1;

    // Traverse from right until we find
    // a digit which is greater than its
    // next digit. For example, in 34125,
    // our index is 4.
    for (int i = len - 2; i >= 0; i--) {
        if (str[i] > str[i+1])
        {
            index = i;
            break;
        }
    }

    // We can also use binary search here as
    // digits after index are sorted in increasing
    // order.
    // Find the biggest digit in the right of
    // arr[index] which is smaller than arr[index]
    int smallGreatDgt = -1;
    for (int i = len - 1; i > index; i--) {
        if (str[i] < str[index]) {
            if (smallGreatDgt == -1)
                smallGreatDgt = i;
            else if (str[i] >= str[smallGreatDgt])
                smallGreatDgt = i;
        }
    }

    // If index is -1 i.e. digits are
    // in increasing order.
    if (index == -1)
        return "-1";

    // Swap both values
    if (smallGreatDgt != -1)
    {
        swap(str[index], str[smallGreatDgt]);
        return str;
    }

    return "-1";
}

// Drivers code
int main()
{
    string str = "34125";
    cout << prevNum(str);
    return 0;
}
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Java program to find the largest smaller
// number by swapping one digit.
class GFG
{

    // Returns largest possible number 
    // with one swap such that the number 
    // is smaller than str. It is assumed 
    // that there are leading 0s.
    static String prevNum(String str)
    {
        int len = str.length();
        int index = -1;

        // Traverse from right until we find
        // a digit which is greater than its
        // next digit. For example, in 34125,
        // our index is 4.
        for (int i = len - 2; i >= 0; i--)
        {
            if (str.charAt(i) > str.charAt(i + 1))
            {
                index = i;
                break;
            }
        }

        // We can also use binary search here as
        // digits after index are sorted in increasing
        // order.
        // Find the biggest digit in the right of
        // arr[index] which is smaller than arr[index]
        int smallGreatDgt = -1;
        for (int i = len - 1; i > index; i--)
        {
            if (str.charAt(i) < str.charAt(index))
            {
                if (smallGreatDgt == -1)
                {
                    smallGreatDgt = i;
                }
                else if (str.charAt(i) >=
                        str.charAt(smallGreatDgt))
                {
                    smallGreatDgt = i;
                }
            }
        }

        // If index is -1 i.e. digits are
        // in increasing order.
        if (index == -1)
        {
            return "-1";
        }

        // Swap both values
        if (smallGreatDgt != -1)
        {
            str = swap(str, index, smallGreatDgt);
            return str;
        }

        return "-1";
    }

    static String swap(String str, int i, int j)
    {
        char ch[] = str.toCharArray();
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return String.valueOf(ch);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "34125";
        System.out.println(prevNum(str));
    }
}

// This code is contributed by 29AjayKumar
```

## <u>蟒蛇 3</u>

```
# Python3 program to find the largest smaller
# number by swapping one digit.
import sys

# Returns largest possible number
# with one swap such that the number
# is smaller than str. It is assumed
# that there are leading 0s.
def prevNum(string, n):
    index = -1

    # Traverse from right until we find
    # a digit which is greater than its
    # next digit. For example, in 34125,
    # our index is 4.
    for i in range(n - 2, -1, -1):
        if int(string[i]) > int(string[i + 1]):
            index = i
            break

    # We can also use binary search here as
    # digits after index are sorted in
    # increasing order.
    # Find the biggest digit in the right of
    # arr[index] which is smaller than arr[index]    
    smallGreatDgt = -1
    for i in range(n - 1, index, -1):
        if (smallGreatDgt == -1 and int(string[i]) <
                                    int(string[index])):
            smallGreatDgt = i
        elif (index > -1 and int(string[i]) >=
                             int(string[smallGreatDgt]) and
                             int(string[i]) < int(string[index])):
            smallGreatDgt = i

    # If index is -1 i.e. digits are
    # in increasing order.
    if index == -1:
        return "" . join("-1")
    else:

        # Swap both values
        (string[index],
         string[smallGreatDgt]) = (string[smallGreatDgt],
                                   string[index])
    return "" . join(string)

# Driver Code
if __name__=='__main__':
    n_str = "34125"
    ans = prevNum(list(n_str), len(n_str))
    print(ans)

# This code is contributed by Vikash Kumar 37
```

## <u>C#</u>

```
// C# program to find the largest smaller
// number by swapping one digit.
using System;

class GFG
{

    // Returns largest possible number
    // with one swap such that the number
    // is smaller than str. It is assumed
    // that there are leading 0s.
    static String prevNum(String str)
    {
        int len = str.Length;
        int index = -1;

        // Traverse from right until we find
        // a digit which is greater than its
        // next digit. For example, in 34125,
        // our index is 4.
        for (int i = len - 2; i >= 0; i--)
        {
            if (str[i] > str[i + 1])
            {
                index = i;
                break;
            }
        }

        // We can also use binary search here as
        // digits after index are sorted in increasing
        // order.
        // Find the biggest digit in the right of
        // arr[index] which is smaller than arr[index]
        int smallGreatDgt = -1;
        for (int i = len - 1; i > index; i--)
        {
            if (str[i] < str[index])
            {
                if (smallGreatDgt == -1)
                {
                    smallGreatDgt = i;
                }
                else if (str[i] >=
                        str[smallGreatDgt])
                {
                    smallGreatDgt = i;
                }
            }
        }

        // If index is -1 i.e. digits are
        // in increasing order.
        if (index == -1)
        {
            return "-1";
        }

        // Swap both values
        if (smallGreatDgt != -1)
        {
            str = swap(str, index, smallGreatDgt);
            return str;
        }

        return "-1";
    }

    static String swap(String str, int i, int j)
    {
        char[] ch = str.ToCharArray();
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return String.Join("",ch);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "34125";
        Console.WriteLine(prevNum(str));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## <u>服务器端编程语言（Professional Hypertext Preprocessor 的缩写）</u>

```
<?php
// PHP program to find the
// largest smaller number
// by swapping one digit.
// Returns largest possible
// number with one swap such
// that the number is smaller
// than str. It is assumed
// that there are leading
// 0s.

function prevNum( $str)
{
    $len = strlen($str);
    $index = -1;

    // Traverse from right
    // until we find a digit
    // which is greater than
    // its next digit. For
    // example, in 34125,
    // our index is 4.
    for ($i = $len - 2; $i >= 0; $i--)
    {
        if ($str[$i] > $str[$i + 1])
        {
            $index = $i;
            break;
        }
    }

    // We can also use binary
    // search here as digits
    // after index are sorted
    // in increasing order.
    // Find the biggest digit
    // in the right of arr[index]
    // which is smaller than
    // arr[index]
    $smallGreatDgt = -1;
    for ($i = $len - 1;
         $i > $index; $i--)
    {
        if ($str[$i] < $str[$index])
        {
            if ($smallGreatDgt == -1)
                $smallGreatDgt = $i;
            else if ($str[$i] >= $str[$smallGreatDgt])
                $smallGreatDgt = $i;
        }
    }

    // If index is -1 i.e.
    // digits are in
    // increasing order.
    if ($index == -1)
        return "-1";

    // Swap both values
    if ($smallGreatDgt != -1)
    {
        list($str[$index],
             $str[$smallGreatDgt]) = array($str[$smallGreatDgt],
                                           $str[$index]);

        // swap(str[index],
        // str[smallGreatDgt]);
        return $str;
    }

    return "-1";
}

// Driver code
$str = "34125";
echo prevNum($str);

// This code is contributed
// by akt_mit
?>
```

## <u>java 描述语言</u>

```
<script>
    // Javascript program to find the largest smaller
    // number by swapping one digit.

    // Returns largest possible number
    // with one swap such that the number
    // is smaller than str. It is assumed
    // that there are leading 0s.
    function prevNum(str)
    {
        let len = str.length;
        let index = -1;

        // Traverse from right until we find
        // a digit which is greater than its
        // next digit. For example, in 34125,
        // our index is 4.
        for (let i = len - 2; i >= 0; i--)
        {
            if (str[i] > str[i + 1])
            {
                index = i;
                break;
            }
        }

        // We can also use binary search here as
        // digits after index are sorted in increasing
        // order.
        // Find the biggest digit in the right of
        // arr[index] which is smaller than arr[index]
        let smallGreatDgt = -1;
        for (let i = len - 1; i > index; i--)
        {
            if (str[i] < str[index])
            {
                if (smallGreatDgt == -1)
                {
                    smallGreatDgt = i;
                }
                else if (str[i] >= str[smallGreatDgt])
                {
                    smallGreatDgt = i;
                }
            }
        }

        // If index is -1 i.e. digits are
        // in increasing order.
        if (index == -1)
        {
            return "-1";
        }

        // Swap both values
        if (smallGreatDgt != -1)
        {
            str = swap(str, index, smallGreatDgt);
            return str;
        }

        return "-1";
    }

    function swap(str, i, j)
    {
        let ch = str.split('');
        let temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return ch.join("");
    }

    let str = "34125";
      document.write(prevNum(str));

</script>
```

<u>**输出:**</u> 

```
32145
```