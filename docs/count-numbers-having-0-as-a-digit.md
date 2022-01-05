# 以 0 为数字计数

> 原文:[https://www . geesforgeks . org/count-numbers-having-0 作为数字/](https://www.geeksforgeeks.org/count-numbers-having-0-as-a-digit/)

**问题:**统计从 1 到 N 有多少个整数包含 0 作为数字。
**例:**

```
Input:  n = 9
Output: 0

Input: n = 107
Output: 17
The numbers having 0 are 10, 20,..90, 100, 101..107

Input: n = 155
Output: 24
The numbers having 0 are 10, 20,..90, 100, 101..110,
120, ..150.
```

在[之前的帖子](https://www.geeksforgeeks.org/count-numbers-0-digit/)
中讨论了一个天真的解决方案，在这篇帖子中讨论了一个优化的解决方案。让我们仔细分析一下这个问题。
**让给定的数字有 d 位数。**
通过计算以下两个值可以计算出所需答案:

1.  最大 d-1 位数的 0 位数整数计数。
2.  精确到 d 位的 0 位整数的计数(当然小于/等于给定的数字！)

因此，解决方案将是以上两个的总和。
第一部分已经讨论过[这里](https://www.geeksforgeeks.org/count-positive-integers-0-digit/)。
**第二部怎么找？**
我们可以找到 d 位数(小于等于给定数)的整数总数，其中不包含任何零。
为了找到这个，我们遍历数字，一次一个数字。
我们发现非负整数的计数如下:

1.  如果那个地方的数字是零，递减计数器 1 并断开(因为我们不能再移动了，递减以确保数字本身包含零)
2.  否则，将(数字-1)乘以幂(9，它右边的位数)

让我们用一个例子来说明。

```
Let the number be n = 123. non_zero = 0
We encounter 1 first, 
 add (1-1)*92  to non_zero (= 0+0)

We encounter 2, 
 add (2-1)*91 to non_zero (= 0+9 = 9)

We encounter 3, 
 add (3-1)*90 to non_zero (=9+3 = 12)
```

我们可以观察到，非零表示 3 位数(不大于 123)组成的整数个数，不包含任何零。即(111，112，…..，119，121，122，123)(建议验证一次)
现在，有人可能会问，计算没有零的数字的计数有什么意义？
**正确！我们感兴趣的是找到零的整数的计数。**
然而，我们现在可以很容易地发现，通过在忽略最重要的地方后从 n 中减去非零，也就是说，在我们前面的例子中，零= 23–非零= 23-12 =11，最后我们将这两部分相加，得到所需的结果！！
以下是上述想法的实现。

## C++

```
//Modified C++ program to count number from 1 to n with
// 0 as a digit.
#include <bits/stdc++.h>
using namespace std;

// Returns count of integers having zero upto given digits
int zeroUpto(int digits)
{
    // Refer below article for details
    // https://www.geeksforgeeks.org/count-positive-integers-0-digit/
    int first = (pow(10,digits)-1)/9;
    int second = (pow(9,digits)-1)/8;
    return 9 * (first - second);
}

// utility function to convert character representation
// to integer
int toInt(char c)
{
    return int(c)-48;
}

// counts numbers having zero as digits upto a given
// number 'num'
int countZero(string num)
{
    // k denoted the number of digits in the number
    int k = num.length();

    // Calculating the total number having zeros,
    // which upto k-1 digits
    int total = zeroUpto(k-1);

    // Now let us calculate the numbers which don't have
    // any zeros. In that k digits upto the given number
    int non_zero = 0;
    for (int i=0; i<num.length(); i++)
    {
        // If the number itself contains a zero then
        // decrement the counter
        if (num[i] == '0')
        {
            non_zero--;
            break;
        }

        // Adding the number of non zero numbers that
        // can be formed
        non_zero += (toInt(num[i])-1) * (pow(9,k-1-i));
    }

    int no = 0, remaining = 0,calculatedUpto=0;

    // Calculate the number and the remaining after
    // ignoring the most significant digit
    for (int i=0; i<num.length(); i++)
    {
        no = no*10 + (toInt(num[i]));
        if (i != 0)
            calculatedUpto = calculatedUpto*10 + 9;
    }
    remaining = no-calculatedUpto;

    // Final answer is calculated
    // It is calculated by subtracting 9....9 (d-1) times
    // from no.
    int ans = zeroUpto(k-1) + (remaining-non_zero-1);
    return ans;
}

// Driver program to test the above functions
int main()
{
    string num = "107";
    cout << "Count of numbers from 1" << " to "
         << num << " is " << countZero(num) << endl;

    num = "1264";
    cout << "Count of numbers from 1" << " to "
         << num << " is " <<countZero(num) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Modified Java program to count number from 1 to n with
// 0 as a digit.

public class GFG {

// Returns count of integers having zero upto given digits
static int zeroUpto(int digits)
{
    // Refer below article for details
    // https://www.geeksforgeeks.org/count-positive-integers-0-digit/
    int first = (int) ((Math.pow(10,digits)-1)/9);
    int second = (int) ((Math.pow(9,digits)-1)/8);
    return 9 * (first - second);
}

// utility function to convert character representation
// to integer
static int toInt(char c)
{
    return (int)(c)-48;
}

// counts numbers having zero as digits upto a given
// number 'num'
static int countZero(String num)
{
    // k denoted the number of digits in the number
    int k = num.length();

    // Calculating the total number having zeros,
    // which upto k-1 digits
    int total = zeroUpto(k-1);

    // Now let us calculate the numbers which don't have
    // any zeros. In that k digits upto the given number
    int non_zero = 0;
    for (int i=0; i<num.length(); i++)
    {
        // If the number itself contains a zero then
        // decrement the counter
        if (num.charAt(i) == '0')
        {
            non_zero--;
            break;
        }

        // Adding the number of non zero numbers that
        // can be formed
        non_zero += (toInt(num.charAt(i))-1) * (Math.pow(9,k-1-i));
    }

    int no = 0, remaining = 0,calculatedUpto=0;

    // Calculate the number and the remaining after
    // ignoring the most significant digit
    for (int i=0; i<num.length(); i++)
    {
        no = no*10 + (toInt(num.charAt(i)));
        if (i != 0)
            calculatedUpto = calculatedUpto*10 + 9;
    }
    remaining = no-calculatedUpto;

    // Final answer is calculated
    // It is calculated by subtracting 9....9 (d-1) times
    // from no.
    int ans = zeroUpto(k-1) + (remaining-non_zero-1);
    return ans;
}

// Driver program to test the above functions

    static public void main(String[] args) {
        String num = "107";
    System.out.println("Count of numbers from 1" + " to "
         + num + " is " + countZero(num));

    num = "1264";
    System.out.println("Count of numbers from 1" + " to "
         + num + " is " +countZero(num));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count number from 1 to n
# with 0 as a digit.

# Returns count of integers having zero
# upto given digits
def zeroUpto(digits):

    first = int((pow(10, digits) - 1) / 9);
    second = int((pow(9, digits) - 1) / 8);
    return 9 * (first - second);

# counts numbers having zero as digits
# upto a given number 'num'
def countZero(num):

    # k denoted the number of digits
    # in the number
    k = len(num);

    # Calculating the total number having 
    # zeros, which upto k-1 digits
    total = zeroUpto(k - 1);

    # Now let us calculate the numbers which
    # don't have any zeros. In that k digits
    # upto the given number
    non_zero = 0;
    for i in range(len(num)):

        # If the number itself contains a zero 
        # then decrement the counter
        if (num[i] == '0'):
            non_zero -= 1;
            break;

        # Adding the number of non zero numbers 
        # that can be formed
        non_zero += (((ord(num[i]) - ord('0')) - 1) *
                                (pow(9, k - 1 - i)));

    no = 0;
    remaining = 0;
    calculatedUpto = 0;

    # Calculate the number and the remaining
    # after ignoring the most significant digit
    for i in range(len(num)):
        no = no * 10 + (ord(num[i]) - ord('0'));
        if (i != 0):
            calculatedUpto = calculatedUpto * 10 + 9;

    remaining = no - calculatedUpto;

    # Final answer is calculated. It is calculated 
    # by subtracting 9....9 (d-1) times from no.
    ans = zeroUpto(k - 1) + (remaining - non_zero - 1);
    return ans;

# Driver Code
num = "107";
print("Count of numbers from 1 to",
        num, "is", countZero(num));

num = "1264";
print("Count of numbers from 1 to",
       num, "is", countZero(num));

# This code is contributed by mits
```

## C#

```
// Modified C# program to count number from 1 to n with
// 0 as a digit. 

using System;
public class GFG{

// Returns count of integers having zero upto given digits
static int zeroUpto(int digits)
{
    // Refer below article for details
    // https://www.geeksforgeeks.org/count-positive-integers-0-digit/
    int first = (int) ((Math.Pow(10,digits)-1)/9);
    int second = (int) ((Math.Pow(9,digits)-1)/8);
    return 9 * (first - second);
}

// utility function to convert character representation
// to integer
static int toInt(char c)
{
    return (int)(c)-48;
}

// counts numbers having zero as digits upto a given
// number 'num'
static int countZero(String num)
{
    // k denoted the number of digits in the number
    int k = num.Length;

    // Calculating the total number having zeros,
    // which upto k-1 digits
    int total = zeroUpto(k-1);

    // Now let us calculate the numbers which don't have
    // any zeros. In that k digits upto the given number
    int non_zero = 0;
    for (int i=0; i<num.Length; i++)
    {
        // If the number itself contains a zero then
        // decrement the counter
        if (num[i] == '0')
        {
            non_zero--;
            break;
        }

        // Adding the number of non zero numbers that
        // can be formed
        non_zero += (toInt(num[i])-1) * (int)(Math.Pow(9,k-1-i));
    }

    int no = 0, remaining = 0,calculatedUpto=0;

    // Calculate the number and the remaining after
    // ignoring the most significant digit
    for (int i=0; i<num.Length; i++)
    {
        no = no*10 + (toInt(num[i]));
        if (i != 0)
            calculatedUpto = calculatedUpto*10 + 9;
    }
    remaining = no-calculatedUpto;

    // Final answer is calculated
    // It is calculated by subtracting 9....9 (d-1) times
    // from no.
    int ans = zeroUpto(k-1) + (remaining-non_zero-1);
    return ans;
}

// Driver program to test the above functions

    static public void Main() {
        String num = "107";
    Console.WriteLine("Count of numbers from 1" + " to "
        + num + " is " + countZero(num));

    num = "1264";
    Console.WriteLine("Count of numbers from 1" + " to "
        + num + " is " +countZero(num));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// number from 1 to n
// with 0 as a digit.

// Returns count of integers
// having zero upto given digits
function zeroUpto($digits)
{

    $first = (int)((pow(10,
                    $digits) - 1) / 9);
    $second = (int)((pow(9,
                    $digits) - 1) / 8);
    return 9 * ($first - $second);
}

// counts numbers having
// zero as digits upto a
// given number 'num'
function countZero($num)
{
    // k denoted the number
    // of digits in the number
    $k = strlen($num);

    // Calculating the total
    // number having zeros,
    // which upto k-1 digits
    $total = zeroUpto($k-1);

    // Now let us calculate
    // the numbers which don't
    // have any zeros. In that
    // k digits upto the given
    // number
    $non_zero = 0;
    for ($i = 0;
         $i < strlen($num); $i++)
    {
        // If the number itself
        // contains a zero then
        // decrement the counter
        if ($num[$i] == '0')
        {
            $non_zero--;
            break;
        }

        // Adding the number of
        // non zero numbers that
        // can be formed
        $non_zero += (($num[$i] - '0') - 1) *
                      (pow(9, $k - 1 - $i));
    }

    $no = 0;
    $remaining = 0;
    $calculatedUpto = 0;

    // Calculate the number
    // and the remaining after
    // ignoring the most
    // significant digit
    for ($i = 0;
         $i < strlen($num); $i++)
    {
        $no = $no * 10 + ($num[$i] - '0');
        if ($i != 0)
            $calculatedUpto = $calculatedUpto *
                                        10 + 9;
    }

    $remaining = $no - $calculatedUpto;

    // Final answer is calculated
    // It is calculated by subtracting
    // 9....9 (d-1) times from no.
    $ans = zeroUpto($k - 1) +
                   ($remaining -
                    $non_zero - 1);
    return $ans;
}

// Driver Code
$num = "107";
echo "Count of numbers from 1 to " .
                     $num . " is " .
             countZero($num) . "\n";

$num = "1264";
echo "Count of numbers from 1 to " .
                     $num . " is " .
                    countZero($num);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Modified javascript program to count number from 1 to n with
// 0 as a digit.

// Returns count of integers having zero upto given digits
function zeroUpto(digits)
{

    // Refer below article for details
    // https://www.geeksforgeeks.org/count-positive-integers-0-digit/
    var first = parseInt( ((Math.pow(10,digits)-1)/9));
    var second = parseInt( ((Math.pow(9,digits)-1)/8));
    return 9 * (first - second);
}

// utility function to convert character representation
// to integer
function toInt(c)
{
    return parseInt((c.charCodeAt(0))-48);
}

// counts numbers having zero as digits upto a given
// number 'num'
function countZero(num)
{
    // k denoted the number of digits in the number
    var k = num.length;

    // Calculating the total number having zeros,
    // which upto k-1 digits
    var total = zeroUpto(k-1);

    // Now let us calculate the numbers which don't have
    // any zeros. In that k digits upto the given number
    var non_zero = 0;
    for (i=0; i<num.length; i++)
    {
        // If the number itself contains a zero then
        // decrement the counter
        if (num.charAt(i) == '0')
        {
            non_zero--;
            break;
        }

        // Adding the number of non zero numbers that
        // can be formed
        non_zero += (toInt(num.charAt(i))-1) * (Math.pow(9,k-1-i));
    }

    var no = 0, remaining = 0,calculatedUpto=0;

    // Calculate the number and the remaining after
    // ignoring the most significant digit
    for (i=0; i<num.length; i++)
    {
        no = no*10 + (toInt(num.charAt(i)));
        if (i != 0)
            calculatedUpto = calculatedUpto*10 + 9;
    }
    remaining = no-calculatedUpto;

    // Final answer is calculated
    // It is calculated by subtracting 9....9 (d-1) times
    // from no.
    var ans = zeroUpto(k-1) + (remaining-non_zero-1);
    return ans;
}

// Driver program to test the above functions
var num = "107";
document.write("Count of numbers from 1" + " to "
     + num + " is " + countZero(num));

var num = "1264";
document.write("<br>Count of numbers from 1" + " to "
     + num + " is " +countZero(num));

// This code is contributed by shikhasingrajput
</script>
```

**输出:**

```
Count of numbers from 1 to 107 is 17 
Count of numbers from 1 to 1264 is 315
```

**复杂度分析:**
**时间复杂度:** O(d)，其中 *d 为位数，即 O(log(n)*
**辅助空间:O(1)**

本文由[阿舒托什·库马尔](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile)供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论