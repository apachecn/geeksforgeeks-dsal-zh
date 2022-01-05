# 使用同一组数字的下一个更高的回文编号

> 原文:[https://www . geesforgeks . org/next-higher-回文-number-use-set-digits/](https://www.geeksforgeeks.org/next-higher-palindromic-number-using-set-digits/)

给定一个回文编号 **num** 具有 **n** 位数。问题是使用与 **num** 中相同的一组数字找到大于 **num** 的最小回文号。如果无法形成这样的数字，则打印“不可能”。
这个数字可能非常大，甚至可能不适合 long long int。

**示例:**

```
Input : 4697557964
Output :  4756996574

Input : 543212345
Output : Not Possible
```

**进场:**以下是步骤:

1.  如果位数 n <= 3，则打印“不可能”并返回。
2.  计算**中间**= n/2–1。
3.  从索引**中间的数字开始遍历到第一个数字，并在遍历时找到最右边数字的索引 **i** ，该数字小于其右侧的数字。**
4.  现在搜索索引范围 **i+1** 到**中间**中大于数字**num【I】**的最小数字。让这个数字的索引为**最小**。
5.  如果找不到这样的最小数字，则打印“不可能”。
6.  否则，交换索引 **i** 和**最小**处的数字，并交换索引 **n-i-1** 和**n-最小-1** 处的数字。这样做是为了保持**号**中的回文特性。
7.  现在反转指数范围 **i+1** 到**中间**的数字。此外，如果 **n** 为偶数，则反转索引范围**中间+1** 至 **n-i-2** 中的数字，否则如果 **n** 为奇数，则反转索引范围**中间+2** 至 **n-i-2** 中的数字。这样做是为了保持**号**中的回文特性。
8.  打印最终修改号**编号**。

## C++

```
// C++ implementation to find next higher
// palindromic number using the same set
// of digits
#include <bits/stdc++.h>
using namespace std;

// function to reverse the digits in the
// range i to j in 'num'
void reverse(char num[], int i, int j)
{
    while (i < j) {
        swap(num[i], num[j]);
        i++;
        j--;
    }
}

// function to find next higher palindromic
// number using the same set of digits
void nextPalin(char num[], int n)
{
    // if length of number is less than '3'
    // then no higher palindromic number
    // can be formed
    if (n <= 3) {
        cout << "Not Possible";
        return;
    }

    // find the index of last digit
    // in the 1st half of 'num'
    int mid = n / 2 - 1;
    int i, j;

    // Start from the (mid-1)th digit and
    // find the first digit that is
    // smaller than the digit next to it.
    for (i = mid - 1; i >= 0; i--)
        if (num[i] < num[i + 1])
            break;

    // If no such digit is found, then all
    // digits are in descending order which
    // means there cannot be a greater
    // palindromic number with same set of
    // digits
    if (i < 0) {
        cout << "Not Possible";
        return;
    }

    // Find the smallest digit on right
    // side of ith digit which is greater
    // than num[i] up to index 'mid'
    int smallest = i + 1;
    for (j = i + 2; j <= mid; j++)
        if (num[j] > num[i] &&
            num[j] <= num[smallest])
            smallest = j;

    // swap num[i] with num[smallest]
    swap(num[i], num[smallest]);

    // as the number is a palindrome, the same
    // swap of digits should be performed in
    // the 2nd half of 'num'
    swap(num[n - i - 1], num[n - smallest - 1]);

    // reverse digits in the range (i+1) to mid
    reverse(num, i + 1, mid);

    // if n is even, then reverse digits in the
    // range mid+1 to n-i-2
    if (n % 2 == 0)
        reverse(num, mid + 1, n - i - 2);

    // else if n is odd, then reverse digits
    // in the range mid+2 to n-i-2
    else
        reverse(num, mid + 2, n - i - 2);

    // required next higher palindromic number
    cout << "Next Palindrome: "
         << num;
}

// Driver program to test above
int main()
{
    char num[] = "4697557964";
    int n = strlen(num);
    nextPalin(num, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find next higher
// palindromic number using the same set
// of digits
import java.util.*;

class NextHigherPalindrome
{
    // function to reverse the digits in the
    // range i to j in 'num'
    public static void reverse(char num[], int i,
                                          int j)
    {
        while (i < j) {
            char temp = num[i];
            num[i] = num[j];
            num[j] = temp;
            i++;
            j--;
        }
    }

    // function to find next higher palindromic
    // number using the same set of digits
    public static void nextPalin(char num[], int n)
    {
        // if length of number is less than '3'
        // then no higher palindromic number
        // can be formed
        if (n <= 3) {
            System.out.println("Not Possible");
            return;
        }
        char temp;

        // find the index of last digit
        // in the 1st half of 'num'
        int mid = n / 2 - 1;
        int i, j;

        // Start from the (mid-1)th digit and
        // find the first digit that is
        // smaller than the digit next to it.
        for (i = mid - 1; i >= 0; i--)
            if (num[i] < num[i + 1])
                break;

        // If no such digit is found, then all
        // digits are in descending order which
        // means there cannot be a greater
        // palindromic number with same set of
        // digits
        if (i < 0) {
            System.out.println("Not Possible");
            return;
        }

        // Find the smallest digit on right
        // side of ith digit which is greater
        // than num[i] up to index 'mid'
        int smallest = i + 1;
        for (j = i + 2; j <= mid; j++)
            if (num[j] > num[i] &&
                num[j] <= num[smallest])
                smallest = j;

        // swap num[i] with num[smallest]
        temp = num[i];
        num[i] = num[smallest];
        num[smallest] = temp;

        // as the number is a palindrome,
        // the same swap of digits should
        // be performed in the 2nd half of
        // 'num'
        temp = num[n - i - 1];
        num[n - i - 1] = num[n - smallest - 1];
        num[n - smallest - 1] = temp;

        // reverse digits in the range (i+1)
        // to mid
        reverse(num, i + 1, mid);

        // if n is even, then reverse
        // digits in the range mid+1 to
        // n-i-2
        if (n % 2 == 0)
            reverse(num, mid + 1, n - i - 2);

        // else if n is odd, then reverse
        // digits in the range mid+2 to n-i-2
        else
            reverse(num, mid + 2, n - i - 2);

        // required next higher palindromic
        // number
        String result=String.valueOf(num);
        System.out.println("Next Palindrome: "+
                                   result);
    }

    // Driver Code
    public static void main(String args[])
    {
        String str="4697557964";
        char num[]=str.toCharArray();
        int n=str.length();
        nextPalin(num,n);
    }
}

// This code is contributed by Danish Kaleem
```

## 计算机编程语言

```
# Python implementation to find next higher
# palindromic number using the same set
# of digits

# function to reverse the digits in the
# range i to j in 'num'
def reverse(num, i, j) :

    while (i < j) :
        temp = num[i]
        num[i] = num[j]
        num[j] = temp
        i = i + 1
        j = j - 1

# function to find next higher palindromic
# number using the same set of digits
def nextPalin(num, n) :

    # if length of number is less than '3'
    # then no higher palindromic number
    # can be formed
    if (n <= 3) :
        print "Not Possible"
        return

    # find the index of last digit
    # in the 1st half of 'num'
    mid = n / 2 - 1

    # Start from the (mid-1)th digit and
    # find the first digit that is
    # smaller than the digit next to it.
    i = mid - 1
    while i >= 0 :
        if (num[i] < num[i + 1]) :
            break
        i = i - 1

    # If no such digit is found, then all
    # digits are in descending order which
    # means there cannot be a greater
    # palindromic number with same set of
    # digits
    if (i < 0) :
        print "Not Possible"
        return

    # Find the smallest digit on right
    # side of ith digit which is greater
    # than num[i] up to index 'mid'
    smallest = i + 1
    j = i + 2
    while j <= mid :
        if (num[j] > num[i] and num[j] <
                        num[smallest]) :
            smallest = j
        j = j + 1

    # swap num[i] with num[smallest]
    temp = num[i]
    num[i] = num[smallest]
    num[smallest] = temp

    # as the number is a palindrome,
    # the same swap of digits should
    # be performed in the 2nd half of
    # 'num'
    temp = num[n - i - 1]
    num[n - i - 1] = num[n - smallest - 1]
    num[n - smallest - 1] = temp

    # reverse digits in the range (i+1)
    # to mid
    reverse(num, i + 1, mid)

    # if n is even, then reverse
    # digits in the range mid+1 to
    # n-i-2
    if (n % 2 == 0) :
        reverse(num, mid + 1, n - i - 2)

    # else if n is odd, then reverse
    # digits in the range mid+2 to n-i-2
    else :
        reverse(num, mid + 2, n - i - 2)

    # required next higher palindromic
    # number
    result = ''.join(num)

    print "Next Palindrome: ",result

# Driver Code
st = "4697557964"
num = list(st)
n = len(st)
nextPalin(num, n)

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# implementation to find
// next higher palindromic
// number using the same set
// of digits
using System;

class GFG
{
    // function to reverse
    // the digits in the
    // range i to j in 'num'
    public static void reverse(char[] num,
                               int i, int j)
    {
        while (i < j)
        {
            char temp = num[i];
            num[i] = num[j];
            num[j] = temp;
            i++;
            j--;
        }
    }

    // function to find next
    // higher palindromic number
    // using the same set of digits
    public static void nextPalin(char[] num,
                                 int n)
    {
        // if length of number is
        // less than '3' then no
        // higher palindromic number
        // can be formed
        if (n <= 3)
        {
            Console.WriteLine("Not Possible");
            return;
        }
        char temp;

        // find the index of last
        // digit in the 1st half
        // of 'num'
        int mid = n / 2 - 1;
        int i, j;

        // Start from the (mid-1)th
        // digit and find the
        // first digit that is
        // smaller than the digit
        // next to it.
        for (i = mid - 1; i >= 0; i--)
            if (num[i] < num[i + 1])
                break;

        // If no such digit is found,
        // then all digits are in
        // descending order which
        // means there cannot be a
        // greater palindromic number
        // with same set of digits
        if (i < 0)
        {
            Console.WriteLine("Not Possible");
            return;
        }

        // Find the smallest digit on
        // right side of ith digit 
        // which is greater than num[i]
        // up to index 'mid'
        int smallest = i + 1;
        for (j = i + 2; j <= mid; j++)
            if (num[j] > num[i] &&
                num[j] < num[smallest])
                smallest = j;

        // swap num[i] with
        // num[smallest]
        temp = num[i];
        num[i] = num[smallest];
        num[smallest] = temp;

        // as the number is a palindrome,
        // the same swap of digits should
        // be performed in the 2nd half of
        // 'num'
        temp = num[n - i - 1];
        num[n - i - 1] = num[n - smallest - 1];
        num[n - smallest - 1] = temp;

        // reverse digits in the 
        // range (i+1) to mid
        reverse(num, i + 1, mid);

        // if n is even, then
        // reverse digits in the
        // range mid+1 to n-i-2
        if (n % 2 == 0)
            reverse(num, mid + 1,
                    n - i - 2);

        // else if n is odd, then
        // reverse digits in the
        // range mid+2 to n-i-2
        else
            reverse(num, mid + 2,
                    n - i - 2);

        // required next higher
        // palindromic number
        String result = new String(num);
        Console.WriteLine("Next Palindrome: "+
                                      result);
    }

    // Driver Code
    public static void Main()
    {
        String str = "4697557964";
        char[] num = str.ToCharArray();
        int n = str.Length;
        nextPalin(num, n);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// next higher palindromic number
// using the same set of digits

// function to reverse the digits
// in the range i to j in 'num'
function reverse(&$num, $i, $j)
{
    while ($i < $j)
    {
        $t = $num[$i];
        $num[$i] = $num[$j];
        $num[$j] = $t;
        $i++;
        $j--;
    }
}

// function to find next higher
// palindromic number using the
// same set of digits
function nextPalin($num, $n)
{
    // if length of number is less
    // than '3' then no higher
    // palindromic number can be formed
    if ($n <= 3)
    {
        echo "Not Possible";
        return;
    }

    // find the index of last digit
    // in the 1st half of 'num'
    $mid = ($n / 2) - 1;
    $i = $mid - 1;
    $j;

    // Start from the (mid-1)th digit
    // and find the first digit
    // that is smaller than the digit
    // next to it.
    for (; $i >= 0; $i--)
        if ($num[$i] < $num[$i + 1])
            break;

    // If no such digit is found,
    // then all digits are in
    // descending order which means
    // there cannot be a greater
    // palindromic number with same
    // set of digits
    if ($i < 0)
    {
        echo "Not Possible";
        return;
    }

    // Find the smallest digit on right
    // side of ith digit which is greater
    // than num[i] up to index 'mid'
    $smallest = $i + 1;
    $j = 0;
    for ($j = $i + 2; $j <= $mid; $j++)
        if ($num[$j] > $num[$i] &&
            $num[$j] < $num[$smallest])
            $smallest = $j;

    // swap num[i] with num[smallest]
    $t = $num[$i];
    $num[$i] = $num[$smallest];
    $num[$smallest] = $t;

    // as the number is a palindrome,
    // the same swap of digits should
    // be performed in the 2nd half of 'num'
    $t = $num[$n - $i - 1];
    $num[$n - $i - 1] = $num[$n - $smallest - 1];
    $num[$n - $smallest - 1] = $t;

    // reverse digits in the
    // range (i+1) to mid
    reverse($num, $i + 1, $mid);

    // if n is even, then
    // reverse digits in the
    // range mid+1 to n-i-2
    if ($n % 2 == 0)
        reverse($num, $mid + 1, $n - $i - 2);

    // else if n is odd, then reverse
    // digits in the range mid+2
    // to n-i-2
    else
        reverse($num, $mid + 2, $n - $i - 2);

    // required next higher
    // palindromic number
    echo "Next Palindrome: " . $num;
}

// Driver Code
$num = "4697557964";
$n = strlen($num);
nextPalin($num, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find next higher
// palindromic number using the same set
// of digitsclass NextHigherPalindrome

// Function to reverse the digits in the
// range i to j in 'num'
function reverse(num , i, j)
{
    while (i < j)
    {
        var temp = num[i];
        num[i] = num[j];
        num[j] = temp;
        i++;
        j--;
    }
}

// Function to find next higher palindromic
// number using the same set of digits
function nextPalin(num, n)
{

    // If length of number is less than '3'
    // then no higher palindromic number
    // can be formed
    if (n <= 3)
    {
        document.write("Not Possible");
        return;
    }
    var temp;

    // Find the index of last digit
    // in the 1st half of 'num'
    var mid = n / 2 - 1;
    var i, j;

    // Start from the (mid-1)th digit and
    // find the first digit that is
    // smaller than the digit next to it.
    for(i = mid - 1; i >= 0; i--)
        if (num[i] < num[i + 1])
            break;

    // If no such digit is found, then all
    // digits are in descending order which
    // means there cannot be a greater
    // palindromic number with same set of
    // digits
    if (i < 0)
    {
        document.write("Not Possible");
        return;
    }

    // Find the smallest digit on right
    // side of ith digit which is greater
    // than num[i] up to index 'mid'
    var smallest = i + 1;
    for(j = i + 2; j <= mid; j++)
        if (num[j] > num[i] &&
            num[j] <= num[smallest])
            smallest = j;

    // Swap num[i] with num[smallest]
    temp = num[i];
    num[i] = num[smallest];
    num[smallest] = temp;

    // As the number is a palindrome,
    // the same swap of digits should
    // be performed in the 2nd half of
    // 'num'
    temp = num[n - i - 1];
    num[n - i - 1] = num[n - smallest - 1];
    num[n - smallest - 1] = temp;

    // Reverse digits in the range (i+1)
    // to mid
    reverse(num, i + 1, mid);

    // If n is even, then reverse
    // digits in the range mid+1 to
    // n-i-2
    if (n % 2 == 0)
        reverse(num, mid + 1, n - i - 2);

    // Else if n is odd, then reverse
    // digits in the range mid+2 to n-i-2
    else
        reverse(num, mid + 2, n - i - 2);

    // Required next higher palindromic
    // number
    var result = num.join('');
    document.write("Next Palindrome: "+
                   result);
}

// Driver Code
var str = "4697557964";
var num = str.split('');
var n = str.length;

nextPalin(num,n);

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
Next Palindrome: 4756996574
```

**时间复杂度:** O(n)

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。