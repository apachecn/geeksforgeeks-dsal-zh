# 由一个数组的数字组成的两个数的最小和

> 原文:[https://www . geeksforgeeks . org/最小和-两位数-数字-数组/](https://www.geeksforgeeks.org/minimum-sum-two-numbers-formed-digits-array/)

给定一个数字数组(值从 0 到 9)，求由数组的数字组成的两个数字的最小可能和。给定数组的所有数字都必须用来构成这两个数字。
**例:**

```
Input: [6, 8, 4, 5, 2, 3]
Output: 604
The minimum sum is formed by numbers 
358 and 246

Input: [5, 3, 0, 7, 4]
Output: 82
The minimum sum is formed by numbers 
35 and 047 
```

当最小数字出现在最高有效位置，下一个最小数字出现在下一个最高有效位置等等时，最小数字将由一组数字形成..
思路是对数组进行递增排序，通过交替从数组中挑选数字来构建两个数字。所以第一个数字由数组中奇数位置的数字组成，第二个数字由数组中偶数位置的数字组成。最后，我们返回第一个和第二个数的和。
以下是上述思路的实现。

## C++

```
// C++ program to find minimum sum of two numbers
// formed from digits of the array.
#include <bits/stdc++.h>
using namespace std;

// Function to find and return minimum sum of
// two numbers formed from digits of the array.
int solve(int arr[], int n)
{
    // sort the array
    sort(arr, arr + n);

    // let two numbers be a and b
    int a = 0, b = 0;
    for (int i = 0; i < n; i++)
    {
        // fill a and b with every alternate digit
        // of input array
        if (i & 1)
            a = a*10 + arr[i];
        else
            b = b*10 + arr[i];
    }

    // return the sum
    return a + b;
}

// Driver code
int main()
{
    int arr[] = {6, 8, 4, 5, 2, 3};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Sum is " << solve(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum sum of two numbers
// formed from digits of the array.
import java.util.Arrays;

class GFG {

    // Function to find and return minimum sum of
    // two numbers formed from digits of the array.
    static int solve(int arr[], int n)
    {

        // sort the array
        Arrays.sort(arr);

        // let two numbers be a and b
        int a = 0, b = 0;
        for (int i = 0; i < n; i++)
        {

            // fill a and b with every alternate
            // digit of input array
            if (i % 2 != 0)
                a = a * 10 + arr[i];
            else
                b = b * 10 + arr[i];
        }

        // return the sum
        return a + b;
    }

    //driver code
    public static void main (String[] args)
    {
        int arr[] = {6, 8, 4, 5, 2, 3};
        int n = arr.length;

        System.out.print("Sum is "
                          + solve(arr, n));
    }
}

//This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find minimum sum of two
# numbers formed from digits of the array.

# Function to find and return minimum sum of
# two numbers formed from digits of the array.
def solve(arr, n):

    # sort the array
    arr.sort()

    # let two numbers be a and b
    a = 0; b = 0
    for i in range(n):

        # Fill a and b with every alternate
        # digit of input array
        if (i % 2 != 0):
            a = a * 10 + arr[i]
        else:
            b = b * 10 + arr[i]

    # return the sum
    return a + b

# Driver code
arr = [6, 8, 4, 5, 2, 3]
n = len(arr)
print("Sum is ", solve(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find minimum
// sum of two numbers formed
// from digits of the array.
using System;

class GFG
{
    // Function to find and return
    // minimum sum of two numbers
    // formed from digits of the array.
    static int solve(int []arr, int n)
    {
        // sort the array
        Array.Sort(arr);

        // let two numbers be a and b
        int a = 0, b = 0;
        for (int i = 0; i < n; i++)
        {
            // fill a and b with every alternate digit
            // of input array
            if (i % 2 != 0)
                a = a * 10 + arr[i];
            else
                b = b * 10 + arr[i];
        }

        // return the sum
        return a + b;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {6, 8, 4, 5, 2, 3};
        int n = arr.Length;
        Console.WriteLine("Sum is " + solve(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// sum of two numbers formed
// from digits of the array.

// Function to find and return
// minimum sum of two numbers
// formed from digits of the array.
function solve($arr, $n)
{
    // sort the array
    sort($arr); sort($arr , $n);

    // let two numbers be a and b
    $a = 0; $b = 0;
    for ($i = 0; $i < $n; $i++)
    {
        // fill a and b with every
        // alternate digit of input array
        if ($i & 1)
            $a = $a * 10 + $arr[$i];
        else
            $b = $b * 10 + $arr[$i];
    }

    // return the sum
    return $a + $b;
}

// Driver code
$arr = array(6, 8, 4, 5, 2, 3);
$n = sizeof($arr);
echo "Sum is " , solve($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum sum of two numbers
// formed from digits of the array.

    // Function to find and return minimum sum of
    // two numbers formed from digits of the array.
    function solve(arr, n)
    {

        // sort the array
        arr.sort();

        // let two numbers be a and b
        let a = 0, b = 0;
        for (let i = 0; i < n; i++)
        {

            // fill a and b with every alternate
            // digit of input array
            if (i % 2 != 0)
                a = a * 10 + arr[i];
            else
                b = b * 10 + arr[i];
        }

        // return the sum
        return a + b;
    }

// Driver Code

        let arr = [6, 8, 4, 5, 2, 3];
        let n = arr.length;

        document.write("Sum is "
                          + solve(arr, n));

</script>
```

**输出:**

```
Sum is 604
```

**方法 2(对于大数)**

当我们必须处理非常大的数字时(如本问题的[练习](https://practice.geeksforgeeks.org/problems/minimum-sum4058/1#)部分)，上述方法将不起作用。处理这个问题的基本思想和上面一样，但是我们将使用字符串来处理 sum，而不是使用数字。

要将字符串形式给出的两个数字相加，可以参考[这个](https://www.geeksforgeeks.org/sum-two-large-numbers/)。

## C++

```
#include <bits/stdc++.h>
using namespace std;

string solve(int arr[], int n)
{
    // code here
    // sorting of array O(nlogn)
    sort(arr, arr + n);
    // Two String for storing our two minimum numbers
    string a = "", b = "";
    // string string alternatively
    for (int i = 0; i < n; i += 2)
    {
        a += (arr[i] + '0');
    }
    for (int i = 1; i < n; i += 2)
    {
        b += (arr[i] + '0');
    }
    int j = a.length() - 1;
    int k = b.length() - 1;
    // as initial carry is zero
    int carry = 0;
    string ans = "";
    while (j >= 0 && k >= 0)
    {
        int sum = 0;
        sum += (a[j] - '0') + (b[k] - '0') + carry;
        ans += to_string(sum % 10);
        carry = sum / 10;
        j--;
        k--;
    }
    // if string b is over and string a is left
    // here we dont need to put here while condition
    // as it would run at max one time. Because the difference
    // between both the strings could be at max 1.
    while (j >= 0)
    {
        int sum = 0;
        sum += (a[j] - '0') + carry;
        ans += to_string(sum % 10);
        carry = sum / 10;
        j--;
    }
    // if string a is over and string b is left
    while (k >= 0)
    {
        int sum = 0;
        sum += (b[k] - '0') + carry;
        ans += to_string(sum % 10);
        carry = sum / 10;
        k--;
    }
    // if carry is left
    if (carry)
    {
        ans += to_string(carry);
    }
    // to remove leading zeroes as they will be ahead of our sum
    while (!ans.empty() and ans.back() == '0')
        ans.pop_back();
    // reverse our final string because we were storing sum from left to right
    reverse(ans.begin(), ans.end());
    return ans;
}

//  Driver Code Starts.
int main()
{
    int arr[] = {6, 8, 4, 5, 2, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Sum is " << solve(arr, n);
    return 0;
} //  Driver Code Ends
```

**Output**

```
Sum is 604
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上述话题的信息，请写评论