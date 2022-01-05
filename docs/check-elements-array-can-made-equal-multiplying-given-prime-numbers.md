# 检查给定的素数相乘是否可以使数组的元素相等

> 原文:[https://www . geesforgeks . org/check-elements-array-can-make-equal-乘-给定-质数/](https://www.geeksforgeeks.org/check-elements-array-can-made-equal-multiplying-given-prime-numbers/)

给定整数数组和素数数组。任务是找出是否有可能通过将质数数组中的一个或多个元素相乘来使整数数组中的所有元素相等。
**例:**

```
Input : arr[]   = {50, 200} 
        prime[] = {2, 3}
Output : Yes
We can multiply 50 with 2 two times
to make both elements of arr[] equal

Input : arr[]   = {3, 4, 5, 6, 2} 
        prime[] = {2, 3}
Output : No
```

我们找到所有数组元素的 [LCM。只有当可以将所有数字转换为 LCM 时，才能使所有元素相等。所以我们找到每个元素的乘数，这样我们就可以通过乘以这个数，使这个元素等于 LCM。然后我们发现给定素数的数是否能形成给定的乘数。
**算法-**
**第一步:**求数组 O(n)
**中所有数的 LCM 第二步:**对于每个数 arr[i]
——用 LCM 除以 arr[i]
——用每个输入质数除结果去掉输入质数的所有因子(可以用模检查可除性)
——如果剩余数不是 1，返回 false
**第三步:**返回真
下面是上面算法的实现。](https://www.geeksforgeeks.org/lcm-of-given-array-elements/) 

## C++

```
// C++ program to find if array elements can
// be made same
#include<bits/stdc++.h>
using namespace std;

// To calculate LCM of whole array
int lcmOfArray(int arr[], int n)
{
    int ans = arr[0];
    for (int i=1; i<n; i++)
        ans = (arr[i]*ans)/__gcd(arr[i], ans);
    return ans;
}

// function to check possibility if we can make
// all element same or not
bool checkArray(int arr[], int prime[], int n, int m)
{
    // Find LCM of whole array
    int lcm = lcmOfArray(arr,n);

    // One by one check if value of lcm / arr[i]
    // can be formed using prime numbers.
    for (int i=0; i<n; i++)
    {
        // divide each element of array by LCM
        int val = lcm/arr[i];

        // Use each input prime number to divide
        // the result to remove all factors of
        // input prime numbers
        for (int j=0; j<m && val!=1; j++)
            while (val % prime[j] == 0)
                val = val/prime[j];

        // If the remaining value is not 1, then
        // it is not possible to make all elements
        // same.
        if (val != 1)
          return false;
    }

    return true;
}

// Driver code
int main()
{
    int arr[] = {50, 200};
    int prime[] = {2, 3};
    int n = sizeof(arr)/sizeof(arr[0]);
    int m = sizeof(prime)/sizeof(prime[0]);

    checkArray(arr, prime, n, m)? cout << "Yes" :
                                  cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if array
// elements can be made same

class GFG
{
    static int ___gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
        return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return ___gcd(a - b, b);
        return ___gcd(a, b - a);
    }

    // To calculate LCM of whole array
    static int lcmOfArray(int arr[], int n)
    {
        int ans = arr[0];
        for (int i = 1; i < n; i++)
            ans = (arr[i] * ans)/ ___gcd(arr[i], ans);
        return ans;
    }

    // function to check possibility if we can make
    // all element same or not
    static boolean checkArray(int arr[], int prime[],
                                          int n, int m)
    {
        // Find LCM of whole array
        int lcm = lcmOfArray(arr,n);

        // One by one check if value of lcm / arr[i]
        // can be formed using prime numbers.
        for (int i = 0; i < n; i++)
        {
            // divide each element of array by LCM
            int val = lcm / arr[i];

            // Use each input prime number to divide
            // the result to remove all factors of
            // input prime numbers
            for (int j = 0; j < m && val != 1; j++)
                while (val % prime[j] == 0)
                    val = val / prime[j];

            // If the remaining value is not 1, then
            // it is not possible to make all elements
            // same.
            if (val != 1)
            return false;
        }

        return true;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {50, 200};
        int prime[] = {2, 3};
        int n = arr.length;
        int m = prime.length;

        if(checkArray(arr, prime, n, m))
        System.out.print("Yes");
        else
        System.out.print("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python  program to find
# if array elements can
# be made same

def ___gcd(a,b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return ___gcd(a-b, b)
    return ___gcd(a, b-a)

# To calculate LCM of whole array
def lcmOfArray(arr,n):

    ans = arr[0]
    for i in range(1,n):
        ans = (arr[i]*ans)/___gcd(arr[i], ans)
    return ans

# function to check possibility
# if we can make
# all element same or not
def checkArray(arr, prime, n, m):

    # Find LCM of whole array
    lcm = lcmOfArray(arr, n)

    # One by one check if
    # value of lcm / arr[i]
    # can be formed using prime numbers.
    for i in range(n):

        # divide each element
        # of array by LCM
        val = lcm/arr[i]

        # Use each input prime
        # number to divide
        # the result to remove
        # all factors of
        # input prime numbers
        for j in range(m and val!=1):
            while (val % prime[j] == 0):
                val = val/prime[j]

        # If the remaining value
        # is not 1, then
        # it is not possible to
        # make all elements
        # same.
        if (val != 1):
            return 0

    return 1

# Driver code
arr = [50, 200]
prime = [2, 3]
n = len(arr)
m = len(prime)

if(checkArray(arr, prime, n, m)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find if array
// elements can be made same
using System;

class GFG {

    static int ___gcd(int a, int b)
    {

        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return ___gcd(a - b, b);

        return ___gcd(a, b - a);
    }

    // To calculate LCM of whole array
    static int lcmOfArray(int []arr, int n)
    {
        int ans = arr[0];

        for (int i = 1; i < n; i++)
            ans = ((arr[i] * ans) /
                       ___gcd(arr[i], ans));
        return ans;
    }

    // function to check possibility if
    // we can make all element same or not
    static bool checkArray(int []arr,
                 int []prime, int n, int m)
    {

        // Find LCM of whole array
        int lcm = lcmOfArray(arr, n);

        // One by one check if value of
        // lcm / arr[i] can be formed
        // using prime numbers.
        for (int i = 0; i < n; i++)
        {

            // divide each element of
            // array by LCM
            int val = lcm / arr[i];

            // Use each input prime number
            // to divide the result to
            // remove all factors of
            // input prime numbers
            for (int j = 0; j < m &&
                                val != 1; j++)
                while (val % prime[j] == 0)
                    val = val / prime[j];

            // If the remaining value is not 1,
            // then it is not possible to make
            // all elements same.
            if (val != 1)
                return false;
        }

        return true;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {50, 200};
        int []prime = {2, 3};
        int n = arr.Length;
        int m = prime.Length;

        if(checkArray(arr, prime, n, m))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if
// array elements can be
// made same

function ___gcd($a, $b)
{

    // Everything divides 0
    if ($a == 0 || $b == 0)
        return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return ___gcd($a - $b, $b);

    return ___gcd($a, $b - $a);
}

// To calculate LCM
// of whole array
function lcmOfArray($arr, $n)
{
    $ans = $arr[0];

    for ($i = 1; $i < $n; $i++)
        $ans = (($arr[$i] * $ans) /
                ___gcd($arr[$i], $ans));
    return $ans;
}

// function to check
// possibility if we
// can make all element
// same or not
function checkArray($arr, $prime,
                    $n, $m)
{

    // Find LCM of
    // whole array
    $lcm = lcmOfArray($arr, $n);

    // One by one check if
    // value of lcm / arr[i]
    // can be formed using
    // prime numbers.
    for ($i = 0; $i < $n; $i++)
    {

        // divide each element
        // of array by LCM
        $val = $lcm / $arr[$i];

        // Use each input prime
        // number to divide the
        // result to remove all
        // factors of input prime
        // numbers
        for ($j = 0; $j < $m &&
                     $val != 1; $j++)
            while ($val % $prime[$j] == 0)
                $val = $val / $prime[$j];

        // If the remaining value
        // is not 1, then it is
        // not possible to make
        // all elements same.
        if ($val != 1)
            return false;
    }

    return true;
}

// Driver code
$arr = array(50, 200);
$prime = array(2, 3);
$n = sizeof($arr);
$m = sizeof($prime);

if(checkArray($arr, $prime,
              $n, $m))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to find if array
// elements can be made same

    function ___gcd(a, b)
    {
        // Everything divides 0 
        if (a == 0 || b == 0)
        return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return ___gcd(a - b, b);
        return ___gcd(a, b - a);
    } 

    // To calculate LCM of whole array
    function lcmOfArray(arr, n)
    {
        let ans = arr[0];
        for (let i = 1; i < n; i++)
            ans = (arr[i] * ans)/ ___gcd(arr[i], ans);
        return ans;
    }

    // function to check possibility if we can make
    // all element same or not
    function checkArray(arr, prime, n, m)
    {
        // Find LCM of whole array
        let lcm = lcmOfArray(arr,n);

        // One by one check if value of lcm / arr[i]
        // can be formed using prime numbers.
        for (let i = 0; i < n; i++)
        {
            // divide each element of array by LCM
            let val = lcm / arr[i];

            // Use each input prime number to divide
            // the result to remove all factors of
            // input prime numbers
            for (let j = 0; j < m && val != 1; j++)
                while (val % prime[j] == 0)
                    val = val / prime[j];

            // If the remaining value is not 1, then
            // it is not possible to make all elements
            // same.
            if (val != 1)
            return false;
        }

        return true;
    }

// Driver Code

        let arr = [50, 200];
        let prime = [2, 3];
        let n = arr.length;
        let m = prime.length;

        if(checkArray(arr, prime, n, m))
        document.write("Yes");
        else
        document.write("No");

</script>
```

**输出:**

```
Yes
```

本文由**尼泰什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。