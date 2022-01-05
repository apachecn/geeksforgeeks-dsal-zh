# 打印要删除的数字位置，使数字可被 6 整除

> 原文:[https://www . geesforgeks . org/print-digits-position-removed-make-number-除尽-6/](https://www.geeksforgeeks.org/print-digits-position-removed-make-number-divisible-6/)

给定一个数字 N，只去掉一个数字，使这个数字能被 6 整除(使它尽可能大)。打印必须移除的位置，如果不可能，则打印-1。

**示例:**

```
Input: 123
Output: 3 
Explanation: Remove 3rd position element and 
hence the number is 12, which is divisible
by 6 and is the greatest possible.

Input: 134
Output: -1
Explanation: Not possible to remove any and 
make it divisible by 6.

Input: 4510222
Output: 1 
Explanation: Remove either 4 or 1 to make it 
divisible by 6\. The numbers after removing 4
and 1 are 510222 and 450222 respectively.
So, remove 1st position to make it the
greatest possible.
```

**天真方法:**
遍历每一个元素，检查减去它后的数是否能被 6 整除，然后存储最大可能数。当 N 是一个非常大的数字，其可除性无法由%运算符检查时，这将不起作用。它只会对较小的 n 起作用。

**高效方法:**
把输入当成一串，想一想可能的情况。你可以检查任何[更大的数被 6](https://www.geeksforgeeks.org/check-large-number-divisible-6-not/) 整除的可能性，如果它能被 2 和 3 整除，那么它也能被 6 整除。将出现的两种情况是

1) **当单位的数字为奇数时**
当最后一位数字为奇数时，唯一可能的方法就是去掉最后一位数字，使其能被 6 整除。所以去掉最后一个数字，检查总和% 3 == 0，确保去掉最后一个数字后，N 的第二个最后一个数字是偶数，它的总和% 3 == 0，那么你得到的答案是必须去掉的第 N 个位置。如果有任何一种情况失败了，那么你就不能去掉任何一个数字使它能被 6 整除。

2) **当单位的位数为偶数时**
在这种情况下，有多个选择。设和是给定数的位数之和。我们可以删除任何数字 d(除了单位位数字，如果十的位数字是奇数，那么这个数字仍然是 2 的倍数)，其和% 3 == d % 3。这是因为删除那个数字后，总和是 3 的倍数。

现在，为了最大化这个数，我们需要在最大的地方找到满足上述条件的数字。
例:
1。Number = 4510222
位数总和= 4 + 5 + 1 + 2 + 2 + 2 = 16
总和% 3 = 1
现在，我们可以删除位数 1 和 4(因为 1 % 3 = 3 和 4 % 3 = 1)
如果我们删除 1，我们将得到 number 450222。如果我们删除 4，我们得到数字 510222
我们删除最大的数字(最左边)，下一个数字大于被删除的数字。
2。Number = 7510222
位数之和= 7+5+1+0+2+2 = 19
位数之和% 3 = 1
位数 7 和 1 可以根据上述解决方案删除，分别给出数字 510222 和 750222。这里，删除最大的(最左边的)索引给出较小的结果，因为 7 > 5。这在上述情况下起作用，因为 4 < 5。

**正确答案:**
找到最左边同时满足两个约束的数字
1。总和% 3 ==数字% 3
2。数字<紧接着的下一个数字
如果你不能最大化某物的加法，试着最小化它的减少。如果找不到数字，数字小于紧接的右数字，则遵循上述方法。如果您从右侧删除某些内容，该数字将是最大可能值，因为您删除的是最低位的数字。
完成后，如果找到任何这样的元素，打印索引，否则只需打印-1。

以下是上述方法的实施情况

## C++

```
// C++ program to print digit's position
// to be removed to make number
// divisible by 6
#include <bits/stdc++.h>
using namespace std;

// function to print the number divisible
// by 6 after exactly removing a digit
void greatest(string s)
{
    int n = s.length();
    int a[n];

    // stores the sum of all elements
    int sum = 0;

    // traverses the string and converts
    // string to number array and sums up
    for (int i = 0; i < n; i++) {
        a[i] = s[i] - '0';
        sum += a[i];
    }

    if (a[n - 1] % 2) // ODD CHECK
    {
        // if second last is odd or
        // sum of n-1 elements are not
        // divisible by 3.
        if (a[n - 2] % 2 != 0 or (sum - a[n - 1]) % 3 != 0) {
            cout << "-1" << endl;
        }

        // second last is even and
        // print n-1 elements
        // removing last digit
        else {

            // last digit removed
            cout << n << endl;
        }
    }
    else {
        int re = sum % 3;
        int del = -1;

        // counter to check if any
        // element after removing,
        // its sum%3==0
        int flag = 0;

        // traverse till second last element
        for (int i = 0; i < n - 1; i++) {

            // to check if any element
            // after removing,
            // its sum%3==0
            if ((a[i]) % 3 == re) {

                // the leftmost element
                if (a[i + 1] > a[i]) {
                    del = i;
                    flag = 1;

                    // break at the leftmost
                    // element
                    break;
                }
                else {
                    // stores the right most
                    // element
                    del = i;
                }
            }
        }

        // if no element has been found
        // as a[i+1]>a[i]
        if (flag == 0) {

            // if second last is even, then
            // remove last if (sum-last)%3==0
            if (a[n - 2] % 2 == 0 and re == a[n - 1] % 3)
                del = n - 1;
        }

        // if no element which on removing
        // gives sum%3==0
        if (del == -1)
            cout << -1 << endl;
        else {
            cout << del + 1 << endl;
        }
    }
}

// driver program to test the above function
int main()
{
    string s = "7510222";
    greatest(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print digit's position
// to be removed to make number
// divisible by 6
import java.util.*;

class solution
{

// function to print the number divisible
// by 6 after exactly removing a digit
static void greatest(String s)
{
    int n = s.length();
    int[] a = new int[n];

    // stores the sum of all elements
    int sum = 0;

    // traverses the string and converts
    // string to number array and sums up
    for (int i = 0; i < n; i++)
    {
        a[i] = s.charAt(i) - '0';
        sum += a[i];
    }

    if (a[n - 1] % 2 !=0) // ODD CHECK
    {
        // if second last is odd or
        // sum of n-1 elements are not
        // divisible by 3.
        if (a[n - 2] % 2 != 0 || (sum - a[n - 1]) % 3 != 0)
        {
            System.out.println("-1");
        }

        // second last is even and
        // print n-1 elements
        // removing last digit
        else
        {

            // last digit removed
            System.out.println(n);
        }
    }

    else
    {
        int re = sum % 3;
        int del = -1;

        // counter to check if any
        // element after removing,
        // its sum%3==0
        int flag = 0;

        // traverse till second last element
        for (int i = 0; i < n - 1; i++)
        {

            // to check if any element
            // after removing,
            // its sum%3==0
            if ((a[i]) % 3 == re)
            {

                // the leftmost element
                if (a[i + 1] > a[i])
                {
                    del = i;
                    flag = 1;

                    // break at the leftmost
                    // element
                    break;
                }
                else
                {
                    // stores the right most
                    // element
                    del = i;
                }
            }
        }

        // if no element has been found
        // as a[i+1]>a[i]
        if (flag == 0)
        {

            // if second last is even, then
            // remove last if (sum-last)%3==0
            if (a[n - 2] % 2 == 0 && re == a[n - 1] % 3)
                del = n - 1;
        }

        // if no element which on removing
        // gives sum%3==0
        if (del == -1)
        System.out.println(-1);
        else
        {
        System.out.println(del + 1);
        }
    }
}

// driver program to test the above function
public static void main(String args[])
{
    String s = "7510222";
    greatest(s);

}
}

//This code is contributed by
//Surendra_Gangwar
```

## 蟒蛇 3

```
# Python program to print digit's position
# to be removed to make number
# divisible by 6
import math as mt

# function to print the number divisible
# by 6 after exactly removing a digit
def greatest(s):

    n = len(s)
    a=[0 for i in range(n)]

    # stores the Sum of all elements
    Sum = 0

    # traverses the string and converts
    # string to number array and Sums up
    for i in range(n):
        a[i] = ord(s[i]) - ord('0')
        Sum += a[i]

    if (a[n - 1] % 2): # ODD CHECK

        # if second last is odd or
        # Sum of n-1 elements are not
        # divisible by 3.
        if (a[n - 2] % 2 != 0 or (Sum - a[n - 1]) % 3 != 0):
            print("-1")

        # second last is even and
        # prn-1 elements
        # removing last digit
        else:

            # last digit removed
            print(n)

    else:
        re = Sum % 3
        dell = -1

        # counter to check if any
        # element after removing,
        # its Sum%3==0
        flag = 0

        # traverse till second last element
        for i in range(n-1):

            # to check if any element
            # after removing,
            # its Sum%3==0
            if ((a[i]) % 3 == re):

                # the leftmost element
                if (a[i + 1] > a[i]):
                    dell = i
                    flag = 1

                    # break at the leftmost
                    # element
                    break

                else:
                    # stores the right most
                    # element
                    dell = i

        # if no element has been found
        # as a[i+1]>a[i]
        if (flag == 0):

            # if second last is even, then
            # remove last if (Sum-last)%3==0
            if (a[n - 2] % 2 == 0 and re == a[n - 1] % 3):
                dell = n - 1

        # if no element which on removing
        # gives Sum%3==0
        if (dell == -1):
            print("-1")
        else:
            print(dell + 1)

# driver program to test the above function

s = "7510222"
greatest(s)

#This code is contributed by Mohit kumar 29
```

## C#

```
// C# program to print digit's position
// to be removed to make number
// divisible by 6
using System;

class GFG
{

// function to print the number divisible
// by 6 after exactly removing a digit
static void greatest(string s)
{
    int n = s.Length;
    int[] a = new int[n];

    // stores the sum of all elements
    int sum = 0;

    // traverses the string and converts
    // string to number array and sums up
    for (int i = 0; i < n; i++)
    {
        a[i] = s[i] - '0';
        sum += a[i];
    }

    if (a[n - 1] % 2 != 0) // ODD CHECK
    {
        // if second last is odd or
        // sum of n-1 elements are not
        // divisible by 3.
        if (a[n - 2] % 2 != 0 ||
           (sum - a[n - 1]) % 3 != 0)
        {
            Console.Write("-1");
        }

        // second last is even and
        // print n-1 elements
        // removing last digit
        else
        {

            // last digit removed
            Console.Write(n);
        }
    }

    else
    {
        int re = sum % 3;
        int del = -1;

        // counter to check if any
        // element after removing,
        // its sum%3==0
        int flag = 0;

        // traverse till second last element
        for (int i = 0; i < n - 1; i++)
        {

            // to check if any element
            // after removing,
            // its sum%3==0
            if ((a[i]) % 3 == re)
            {

                // the leftmost element
                if (a[i + 1] > a[i])
                {
                    del = i;
                    flag = 1;

                    // break at the leftmost
                    // element
                    break;
                }
                else
                {
                    // stores the right most
                    // element
                    del = i;
                }
            }
        }

        // if no element has been found
        // as a[i+1]>a[i]
        if (flag == 0)
        {

            // if second last is even, then
            // remove last if (sum-last)%3==0
            if (a[n - 2] % 2 == 0 &&
                  re == a[n - 1] % 3)
                del = n - 1;
        }

        // if no element which on removing
        // gives sum%3==0
        if (del == -1)
        Console.Write(-1);
        else
        {
        Console.Write(del + 1);
        }
    }
}

// Driver Code
public static void Main()
{
    string s = "7510222";
    greatest(s);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print digit's position
// to be removed to make number
// divisible by 6

// Function to print the number divisible
// by 6 after exactly removing a digit
function greatest($s)
{
    $n = strlen($s);
    $a[$n] = array();

    // stores the sum of all elements
    $sum = 0;

    // traverses the string and converts
    // string to number array and sums up
    for ($i = 0; $i < $n; $i++)
    {
        $a[$i] = $s[$i] - '0';
        $sum += $a[$i];
    }

    if ($a[$n - 1] % 2) // ODD CHECK
    {
        // if second last is odd or
        // sum of n-1 elements are not
        // divisible by 3.
        if ($a[$n - 2] % 2 != 0 or
           ($sum - $a[$n - 1]) % 3 != 0)
        {
            echo "-1" ,"\n";
        }

        // second last is even and print n-1
        // elements removing last digit
        else
        {

            // last digit removed
            echo $n, "\n";
        }
    }
    else
    {
        $re = $sum % 3;
        $del = -1;

        // counter to check if any
        // element after removing,
        // its sum%3==0
        $flag = 0;

        // traverse till second last element
        for ($i = 0; $i < $n - 1; $i++)
        {

            // to check if any element
            // after removing, its sum%3==0
            if (($a[$i]) % 3 == $re)
            {

                // the leftmost element
                if ($a[$i + 1] > $a[$i])
                {
                    $del = $i;
                    $flag = 1;

                    // break at the leftmost
                    // element
                    break;
                }
                else
                {
                    // stores the right most
                    // element
                    $del = $i;
                }
            }
        }

        // if no element has been found
        // as a[i+1]>a[i]
        if ($flag == 0)
        {

            // if second last is even, then
            // remove last if (sum-last)%3==0
            if ($a[$n - 2] % 2 == 0 and
                $re == $a[$n - 1] % 3)
                $del = $n - 1;
        }

        // if no element which on removing
        // gives sum%3==0
        if ($del == -1)
            echo -1, "\n";
        else
        {
            echo $del + 1, "\n";
        }
    }
}

// Driver Code
$s = "7510222";
greatest($s);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to print digit's
// position to be removed to make number
// divisible by 6

// Function to print the number divisible
// by 6 after exactly removing a digit
function greatest(s)
{
    let n = s.length;
    let a = new Array(n);

    // Stores the sum of all elements
    let sum = 0;

    // Traverses the string and converts
    // string to number array and sums up
    for(let i = 0; i < n; i++)
    {
        a[i] = s[i] - '0';
        sum += a[i];
    }

    // ODD CHECK
    if (a[n - 1] % 2)
    {

        // If second last is odd or
        // sum of n-1 elements are not
        // divisible by 3.
        if (a[n - 2] % 2 != 0 ||
         (sum - a[n - 1]) % 3 != 0)
        {
            document.write("-1" + "<br>");
        }

        // Second last is even and
        // print n-1 elements
        // removing last digit
        else
        {

            // Last digit removed
            document.write(n + "<br>");
        }
    }
    else
    {
        let re = sum % 3;
        let del = -1;

        // Counter to check if any
        // element after removing,
        // its sum%3==0
        let flag = 0;

        // Traverse till second last element
        for(let i = 0; i < n - 1; i++)
        {

            // To check if any element
            // after removing,
            // its sum%3==0
            if ((a[i]) % 3 === re)
            {

                // The leftmost element
                if (a[i + 1] > a[i])
                {
                    del = i;
                    flag = 1;

                    // Break at the leftmost
                    // element
                    break;
                }
                else
                {

                    // Stores the right most
                    // element
                    del = i;
                }
            }
        }

        // If no element has been found
        // as a[i+1]>a[i]
        if (flag === 0)
        {

            // If second last is even, then
            // remove last if (sum-last)%3==0
            if (a[n - 2] % 2 === 0 &&
                re === a[n - 1] % 3)
                del = n - 1;
        }

        // If no element which on removing
        // gives sum%3==0
        if (del === -1)
            document.write(-1 + "<br>");
        else {
            document.write(del + 1 + "<br>");
        }
    }
}

// Driver code
let s = "7510222";

greatest(s);

// This code is contributed by Manoj.

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(位数)