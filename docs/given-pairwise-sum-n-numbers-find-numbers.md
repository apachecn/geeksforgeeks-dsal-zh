# 给定 n 个数字的成对和，求数字

> 原文:[https://www . geesforgeks . org/given-pain-sum-n-numbers-find-numbers/](https://www.geeksforgeeks.org/given-pairwise-sum-n-numbers-find-numbers/)

按指定顺序给出 n(其中 n >= 3)个数字的成对和，找出这些数字。该顺序具有第一和第二、第一和第三、第一和第四、…第二和第三、第二和第四，..等等。考虑一个例子:n = 4，让数字为{a，b，c，d}，它们的成对和以 arr[] = {a+b，a+c，a+d，b+c，b+d，c+d}的顺序给出。
示例:

```
Input  : arr[] = {11, 18, 13, 13, 8, 5}
Output : {8, 3, 10, 5}
8+3 = 11, 8+10 = 18, 8+5 = 13, 3+10 = 13,
3+5 = 8, ...

Input  : arr[] = {13, 10, 14, 9, 17, 21, 
                  16, 18, 13, 17}
Output : {3, 10, 7, 11, 6}
```

亚马逊提问

方法完全基于数学，如下所示:

```
n = 3, {a+b, a+c, b+c}
We can find b-a = arr[2] - arr[1] 
                = (b+c) - (a+c)
We can find b = (arr[0] + (b-a))/2
              = (a + b + (b - a))/2  
              = b
We can find a = arr[0] - b
              = a  

n = 4, {a+b, a+c, a+d, b+c, b+d, c+d}
We can find b-a = arr[3] - arr[1]
                = (b+c) - (a+c)  
We can find b = (arr[0] + (b-a)) / 2
              = ((a+b) + (b-a)) / 2
            a = arr[0] - b
              = (a+b) - b
            c = arr[1] - a
              = (a+c) - a
            d = arr[2] - a
              = (a+d) - a

Observation : 
b_minus_a = b - a = arr[n-1] - arr[1]
b = (arr[0] + b_minus_a)/2
a = (arr[0] - b)
c = arr[1] - a
d = arr[2] - a
..........

n = 5, {a+b, a+c, a+d, a+e, b+c, 
 b+d, b+e, c+d, c+e, d+e}

Then calculate b-a = arr[n-1] - arr[1]
                   = (b+c) - (a+c)
Then b = (arr[0] + (b-a)) / 2
       = ((a+b) + (b-a)) / 2
     a = arr[0] - b
       = (a+b) - b
Then for i=1 to n-2, 
remaining numbers are calculated as
arr[i] - a, like
       c = arr[1] - a
         = (a+c) - a
       d = arr[2] - a
         = (a+c) - a      and so on,
          .
          .
          .
          .
last number = arr[n-2] - a 
```

以下是上述想法的实现。

## C++

```
// C++ program to find n numbers from given ordered
// pairwise sum of them.
#include <bits/stdc++.h>
using namespace std;

// Note : n is not size of array, but number of
// elements whose pairwise sum is stored
// in arr[]
void findNumbers(int arr[], int n)
{
    int num[n];

    // b-a is calculated here
    int b_minus_a = arr[n-1] - arr[1];

    // b is calculated here
    num[1] = (arr[0] + b_minus_a) / 2;

    // a is calculated here
    num[0] = arr[0] - num[1];

    // to calculate all the other numbers
    for (int i=1; i<=(n-2); i++)
        num[i+1] = arr[i] - num[0];

    // display the numbers
    cout << "Numbers are: ";
    for (int i=0; i<n; i++)
        cout << num[i] << " ";
}

//Driver program
int main()
{
    int arr[] = {13, 10, 14, 9, 17, 21, 16, 18, 13, 17};
    int n = 5; // n is not size of array, but number of
               // elements whose pairwise sum is stored
               // in arr[]
    findNumbers(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n numbers from given
// ordered pairwise sum of them.
class GFG {

    // Note : n is not size of array, but number 
    // of elements whose pairwise sum is stored
    // in arr[]
    static void findNumbers(int arr[], int n)
    {

        int num[] = new int[n];

        // b-a is calculated here
        int b_minus_a = arr[n-1] - arr[1];

        // b is calculated here
        num[1] = (arr[0] + b_minus_a) / 2;

        // a is calculated here
        num[0] = arr[0] - num[1];

        // to calculate all the other numbers
        for (int i = 1; i <= (n - 2); i++)
            num[i+1] = arr[i] - num[0];

        // display the numbers
        System.out.print("Numbers are: ");

        for (int i = 0; i < n; i++)
            System.out.print(num[i] + " ");
    }

    // Driver method
    public static void main(String[] args)
    {

        int arr[] = {13, 10, 14, 9, 17, 21,
                             16, 18, 13, 17};

        // n is not size of array, but number of
        // elements whose pairwise sum is stored
        // in arr[]
        int n = 5;

        findNumbers(arr, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find n numbers
# from given ordered pairwise sum of them.

# Note : n is not size of array,
# but number of elements whose
# pairwise sum is stored in arr[]
def findNumbers(arr, n):

    num = [0 for i in range(n)]

    # b-a is calculated here
    b_minus_a = arr[n-1] - arr[1]

    # b is calculated here
    num[1] = (arr[0] + b_minus_a) // 2

    # a is calculated here
    num[0] = arr[0] - num[1]

    # to calculate all the other numbers
    for i in range(1, (n - 2) + 1):
        num[i+1] = arr[i] - num[0]

    # display the numbers
    print("Numbers are: ", end = "")
    for i in range(n):
        print(num[i], end = ", ")

# Driver Code
arr = [13, 10, 14, 9, 17, 21, 16, 18, 13, 17]
n = 5 # n is not size of array, but number
      # of elements whose pairwise sum is
      # stored in arr[]

findNumbers(arr, n)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find n numbers from
// given ordered pairwise sum of them.
using System;

class GFG {

    // Note : n is not size of array, but
    // number of elements whose pairwise
    // sum is stored in arr[]
    static void findNumbers(int []arr, int n)
    {

        int []num = new int[n];

        // b-a is calculated here
        int b_minus_a = arr[n - 1] - arr[1];

        // b is calculated here
        num[1] = (arr[0] + b_minus_a) / 2;

        // a is calculated here
        num[0] = arr[0] - num[1];

        // to calculate all the other numbers
        for (int i = 1; i <= (n - 2); i++)
            num[i + 1] = arr[i] - num[0];

        // display the numbers
        Console.Write("Numbers are: ");

        for (int i = 0; i < n; i++)
            Console.Write(num[i] + " ");
    }

    // Driver code
    public static void Main(String[] args)
    {

        int []arr = {13, 10, 14, 9, 17,
                     21, 16, 18, 13, 17};

        // n is not size of array, but number of
        // elements whose pairwise sum is stored
        // in arr[]
        int n = 5;

        findNumbers(arr, n);
    }
}

// This code is contributed by parashar...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n numbers
// from given ordered pairwise
// sum of them.

// Note : n is not size
// of array, but number of
// elements whose pairwise
// sum is stored in arr[]
function findNumbers($arr, $n)
{
    $num[$n]=0;

    // b-a is calculated here
    $b_minus_a = $arr[$n - 1] - $arr[1];

    // b is calculated here
    $num[1] = ($arr[0] + $b_minus_a) / 2;

    // a is calculated here
    $num[0] = $arr[0] - $num[1];

    // to calculate all the other numbers
    for($i = 1; $i <= ($n - 2); $i++)
        $num[$i + 1] = $arr[$i] - $num[0];

    // display the numbers
    echo "Numbers are: ";
    for($i = 0; $i < $n; $i++)
        echo $num[$i]. ", ";
}

// Driver Code
{
    $arr = array(13, 10, 14, 9, 17,
                 21, 16, 18, 13, 17);

    // n is not size of array, but number of
    // elements whose pairwise sum is stored
    // in arr[]
    $n = 5;
    findNumbers($arr, $n);
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// javascript program to find n numbers from given
// ordered pairwise sum of them.    // Note : n is not size of array, but number
    // of elements whose pairwise sum is stored
    // in arr
    function findNumbers(arr , n) {

        var num = Array(n).fill(0);

        // b-a is calculated here
        var b_minus_a = arr[n - 1] - arr[1];

        // b is calculated here
        num[1] = parseInt((arr[0] + b_minus_a) / 2);

        // a is calculated here
        num[0] = arr[0] - num[1];

        // to calculate all the other numbers
        for (i = 1; i <= (n - 2); i++)
            num[i + 1] = arr[i] - num[0];

        // display the numbers
        document.write("Numbers are: ");

        for (i = 0; i < n; i++)
            document.write(num[i] + " ");
    }

    // Driver method

        var arr = [ 13, 10, 14, 9, 17, 21, 16, 18, 13, 17 ];

        // n is not size of array, but number of
        // elements whose pairwise sum is stored
        // in arr
        var n = 5;

        findNumbers(arr, n);
// This code contributed by umadevi9616
</script>
```

输出:

```
Numbers are: 3, 10, 7, 11, 6
```

时间复杂度:O(n)
参考文献:
[【https://www.careercup.com/question?id=12005195】](https://www.careercup.com/question?id=12005195)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。