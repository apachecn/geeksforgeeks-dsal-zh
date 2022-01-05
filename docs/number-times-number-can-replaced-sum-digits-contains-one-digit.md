# 一个数字可以被其位数之和替换的次数，直到它只包含一个位数

> 原文:[https://www . geesforgeks . org/number-times-number-can-replaced-sum-digits-contains-1 位数/](https://www.geeksforgeeks.org/number-times-number-can-replaced-sum-digits-contains-one-digit/)

计算一个数可以被它的数字之和替换的次数，直到它只包含一个数字，并且这个数可以非常大。
**例:**

```
Input : 10
Output : 1
1 + 0 = 1, so only one times 
an number can be replaced by its sum .

Input : 991
Output : 3
9 + 9 + 1 = 19, 1 + 9 = 10, 1 + 0 = 1 
hence 3 times the number can be replaced 
by its sum.
```

我们已经讨论过[求一个数的位数的和，直到和变成个位数](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)。
这里的问题只是上面前面问题的延伸。在这里，我们只想计算一个数可以被它的和替换的次数，直到它只包含一个数字。由于数字可能非常大，因此为了避免溢出，我们将数字输入为字符串。**因此，为了计算这个，我们取一个名为 temporary_sum 的变量，在这个变量中，我们重复计算字符串的位数之和，并将这个 temporary_sum 再次转换为字符串。这个过程一直重复到字符串长度变成 1。**为了更清楚地解释这一点，考虑数字 991
9 + 9 + 1 = 19，现在 19 是一个字符串
1 + 9 = 10，再一次，10 是一个字符串
1 + 0 = 1。同样，1 是一个字符串，但是这里的字符串长度是 1，所以循环中断。
**求和运算的次数就是最终答案。**
以下是本办法的实施情况。

## C++

```
// C++ program to count number of times we
// need to add digits to get a single digit.
#include <bits/stdc++.h>
using namespace std;

int NumberofTimes(string str)
{
    // Here the count variable store
    // how many times we do sum of
    // digits and temporary_sum
    // always store the temporary sum
    // we get at each iteration .
    int temporary_sum = 0, count = 0;

    // In this loop we always compute
    // the sum of digits in temporary_
    // sum variable and convert it
    // into string str till its length
    // become 1 and increase the count
    // in each iteration.
    while (str.length() > 1)
    {
        temporary_sum = 0;

        // computing sum of its digits
        for (int i = 0; i < str.length(); i++)
            temporary_sum += ( str[ i ] - '0' ) ;

        // converting temporary_sum into string
        // str again .
        str = to_string(temporary_sum) ;

        // increase the count
        count++;
    }

    return count;
}

// Driver program to test the above function
int main()
{
    string s = "991";
    cout << NumberofTimes(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of times we
// need to add digits to get a single digit.

public class GFG
{
    static int NumberofTimes(String str)
    {
        // Here the count variable store
        // how many times we do sum of
        // digits and temporary_sum
        // always store the temporary sum
        // we get at each iteration .
        int temporary_sum = 0, count = 0;

        // In this loop we always compute
        // the sum of digits in temporary_
        // sum variable and convert it
        // into string str till its length
        // become 1 and increase the count
        // in each iteration.
        while (str.length() > 1)
        {
            temporary_sum = 0;

            // computing sum of its digits
            for (int i = 0; i < str.length(); i++)
                temporary_sum += ( str.charAt(i) - '0' ) ;

            // converting temporary_sum into string
            // str again .
            str = temporary_sum + "" ;

            // increase the count
            count++;
        }

        return count;
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
         String s = "991";
         System.out.println(NumberofTimes(s));
    }

}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python 3 program to count number of times we
# need to add digits to get a single digit.
def NumberofTimes(s):

    # Here the count variable store
    # how many times we do sum of
    # digits and temporary_sum
    # always store the temporary sum
    # we get at each iteration .
    temporary_sum = 0
    count = 0

    # In this loop we always compute
    # the sum of digits in temporary_
    # sum variable and convert it
    # into string str till its length
    # become 1 and increase the count
    # in each iteration.
    while (len(s) > 1):

        temporary_sum = 0

        # computing sum of its digits
        for i in range(len(s)):
            temporary_sum += (ord(s[ i ]) -
                              ord('0'))

        # converting temporary_sum into
        # string str again .
        s = str(temporary_sum)

        # increase the count
        count += 1

    return count

# Driver Code
if __name__ == "__main__":

    s = "991"
    print(NumberofTimes(s))

# This code is contributed by Ita_c
```

## C#

```
// C# program to count number of
// times we need to add digits to
// get a single digit.
using System;

class GFG {

    // Function to count number of
    // times we need to add digits
    // to get a single digit
    static int NumberofTimes(String str)
    {

        // Here the count variable store
        // how many times we do sum of
        // digits and temporary_sum
        // always store the temporary sum
        // we get at each iteration .
        int temporary_sum = 0, count = 0;

        // In this loop we always compute
        // the sum of digits in temporary_
        // sum variable and convert it
        // into string str till its length
        // become 1 and increase the count
        // in each iteration.
        while (str.Length > 1)
        {
            temporary_sum = 0;

            // computing sum of its digits
            for (int i = 0; i < str.Length; i++)
                temporary_sum += (str[i] - '0');

            // converting temporary_sum
            // into string str again .
            str = temporary_sum + "" ;

            // increase the count
            count++;
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        String s = "991";
        Console.Write(NumberofTimes(s));
    }

}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of times we
// need to add digits to get a single digit.

function NumberofTimes($str)
{
    // Here the count variable store
    // how many times we do sum of
    // digits and temporary_sum
    // always store the temporary sum
    // we get at each iteration .
    $temporary_sum = 0; $count = 0;

    // In this loop we always compute
    // the sum of digits in temporary_
    // sum variable and convert it
    // into string str till its length
    // become 1 and increase the count
    // in each iteration.
    while (strlen($str) > 1)
    {
        $temporary_sum = 0;

        // computing sum of its digits
        for ($i = 0; $i < strlen($str); $i++)
            $temporary_sum += ($str[ $i ] - '0');

        // converting temporary_sum into
        // string str again .
        $str = (string)($temporary_sum);

        // increase the count
        $count++;
    }

    return $count;
}

// Driver Code
$s = "991";
echo NumberofTimes($s);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to
// count number of times we
// need to add digits to
// get a single digit.

function NumberofTimes(str)
{
    // Here the count variable store
    // how many times we do sum of
    // digits and temporary_sum
    // always store the temporary sum
    // we get at each iteration .
    var temporary_sum = 0, count = 0;

    // In this loop we always compute
    // the sum of digits in temporary_
    // sum variable and convert it
    // into string str till its length
    // become 1 and increase the count
    // in each iteration.
    while (str.length > 1)
    {
        temporary_sum = 0;

        // computing sum of its digits
        for (i = 0; i < str.length; i++)
         temporary_sum += ( str.charAt(i) - '0' ) ;

        // converting temporary_sum into string
        // str again .
        str = temporary_sum + "" ;

        // increase the count
        count++;
    }

    return count;
}

// Driver program to test above functions
var s = "991";
document.write(NumberofTimes(s));

// This code contributed by Princi Singh

</script>
```

**输出:**

```
3
```

本文由 **Surya Priy** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。