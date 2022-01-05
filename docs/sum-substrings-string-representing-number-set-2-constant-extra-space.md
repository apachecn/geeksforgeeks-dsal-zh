# 代表数字的字符串的所有子字符串之和|集合 2(恒定额外空间)

> 原文:[https://www . geesforgeks . org/sum-substrings-string-presented-number-set-2-constant-extra-space/](https://www.geeksforgeeks.org/sum-substrings-string-representing-number-set-2-constant-extra-space/)

给定一个代表数字的字符串，我们需要得到这个字符串所有可能的子字符串的总和。
**例:**

```
Input : s = "6759"
Output : 8421
sum = 6 + 7 + 5 + 9 + 67 + 75 + 
      59 + 675 + 759 + 6759
      = 8421

Input : s = "16"
Output : 23
sum = 1 + 6 + 16 = 23
```

我们在下面的帖子中讨论了一个解决方案。
[代表一个数字的字符串的所有子串的和|集合 1](https://www.geeksforgeeks.org/sum-of-all-substrings-of-a-string-representing-a-number/)
该解决方案基于不使用任何额外空间的不同方法。
这个问题可以这样看。
让编号为 s = "6759"

```
        1    10    100    1000
    6   1     1      1       1
    7   2     2      2
    5   3     3
    9   4
```

上表表明，当所有子串进一步转换为 1、10、100 等时..表单中，字符串的每个索引都会有一些固定的出现。第一个索引将有 1、10 等中的每一个出现..第二个有 2 个，第三个有 3 个，以此类推。
还有一点就是最后一个元素的出现将只限于一个。最后第二个元素将被限制为 1 和 10。倒数第三名将达到 100 名，以此类推。
从以上几点让我们找出总和。

```
sum = 6*(1*1 + 1*10 + 1*100 + 1*1000) + 7*(2*1 + 2*10 + 2*100) + 
      5*(3*1 + 3*10) + 9*(4*1)
    = 6*1*(1111) + 7*2*(111) + 5*3*(11) + 9*4*(1)
    = 6666 + 1554 + 165 + 36
    = 8421
```

现在，为了处理乘法，我们将有一个从 1 开始的乘法因子。从例子中可以清楚地看出，乘法因子(反过来)是 1，11，111，…等等。所以乘法将基于三个因素。数字、它的索引和一个乘法因子。

## C++

```
// C++ program to print sum of all substring of
// a number represented as a string
#include <bits/stdc++.h>
using namespace std;

// Returns sum of all substring of num
int sumOfSubstrings(string num)
{
    long long int sum = 0; // Initialize result

    // Here traversing the array in reverse
    // order.Initializing loop from last
    // element.
    // mf is multiplying factor.
    long long int mf = 1;
    for (int i=num.size()-1; i>=0; i--)
    {
        // Each time sum is added to its previous
        // sum. Multiplying the three factors as
        // explained above.
        // s[i]-'0' is done to convert char to int.
        sum += (num[i]-'0')*(i+1)*mf;

        // Making new multiplying factor as
        // explained above.
        mf = mf*10 + 1;
    }

    return sum;
}

//  Driver code to test above methods
int main()
{
    string num = "6759";
    cout << sumOfSubstrings(num) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print sum of all substring of
// a number represented as a string
import java.util.Arrays;

public class GFG {

    // Returns sum of all substring of num
    public static long sumOfSubstrings(String num)
    {
        long sum = 0; // Initialize result

        // Here traversing the array in reverse
        // order.Initializing loop from last
        // element.
        // mf is multiplying factor.
        long mf = 1;
        for (int i = num.length() - 1; i >= 0; i --)
        {
            // Each time sum is added to its previous
            // sum. Multiplying the three factors as
            // explained above.
            // s[i]-'0' is done to convert char to int.
            sum += (num.charAt(i) - '0') * (i + 1) * mf;

            // Making new multiplying factor as
            // explained above.
            mf = mf * 10 + 1;
        }

        return sum;
    }

    //  Driver code to test above methods
    public static void main(String[] args)
    {
        String num = "6759";

        System.out.println(sumOfSubstrings(num));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to print sum of all substring of
# a number represented as a string

# Returns sum of all substring of num
def sumOfSubstrings(num):

    sum = 0 # Initialize result

    # Here traversing the array in reverse
    # order.Initializing loop from last
    # element.
    # mf is multiplying factor.
    mf = 1
    for i in range(len(num) - 1, -1, -1):

        # Each time sum is added to its previous
        # sum. Multiplying the three factors as
        # explained above.
        # int(s[i]) is done to convert char to int.
        sum = sum + (int(num[i])) * (i + 1) * mf

        # Making new multiplying factor as
        # explained above.
        mf = mf * 10 + 1

    return sum

# Driver code to test above methods
if __name__=='__main__':
    num = "6759"
    print(sumOfSubstrings(num))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to print sum of all substring of
// a number represented as a string
using System;

public class GFG {

    // Returns sum of all substring of num
    public static long sumOfSubstrings(string num)
    {

        long sum = 0; // Initialize result

        // Here traversing the array in reverse
        // order.Initializing loop from last
        // element.
        // mf is multiplying factor.
        long mf = 1;

        for (int i = num.Length - 1; i >= 0; i --)
        {

            // Each time sum is added to its previous
            // sum. Multiplying the three factors as
            // explained above.
            // s[i]-'0' is done to convert char to int.
            sum += (num[i] - '0') * (i + 1) * mf;

            // Making new multiplying factor as
            // explained above.
            mf = mf * 10 + 1;
        }

        return sum;
    }

    // Driver code to test above methods
    public static void Main()
    {
        string num = "6759";

        Console.WriteLine(sumOfSubstrings(num));

    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print sum of
// all substring of  a number
// represented as a string

// Returns sum of all
// substring of num
function sumOfSubstrings($num)
{
    // Initialize result
    $sum = 0;

    // Here traversing the array
    // in reverse order.Initializing
    // loop from last element.
    // mf is multiplying factor.
    $mf = 1;
    for ($i = strlen($num) - 1; $i >= 0; $i--)
    {
        // Each time sum is added to
        // its previous sum. Multiplying
        // the three factors as explained above.
        // s[i]-'0' is done to convert char to int.
        $sum += ($num[$i] - '0') * ($i + 1) * $mf;

        // Making new multiplying
        // factor as explained above.
        $mf = $mf * 10 + 1;
    }

    return $sum;
}

// Driver Code
$num = "6759";
echo sumOfSubstrings($num), "\n";

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
    // Javascript program to print sum of all substring of
    // a number represented as a string

    // Returns sum of all substring of num
    function sumOfSubstrings(num)
    {

        let sum = 0; // Initialize result

        // Here traversing the array in reverse
        // order.Initializing loop from last
        // element.
        // mf is multiplying factor.
        let mf = 1;

        for (let i = num.length - 1; i >= 0; i --)
        {

            // Each time sum is added to its previous
            // sum. Multiplying the three factors as
            // explained above.
            // s[i]-'0' is done to convert char to int.
            sum += (num[i].charCodeAt() - '0'.charCodeAt()) * (i + 1) * mf;

            // Making new multiplying factor as
            // explained above.
            mf = mf * 10 + 1;
        }

        return sum;
    }

    let num = "6759"; 
      document.write(sumOfSubstrings(num));

     // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
8421
```

本文由 **Jatin Goyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。