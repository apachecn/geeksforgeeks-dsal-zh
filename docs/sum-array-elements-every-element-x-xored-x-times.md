# 每个元素 x 后的数组元素之和为自身的 x 倍

> 原文:[https://www . geesforgeks . org/sum-array-elements-every-element-x-xored-x-times/](https://www.geeksforgeeks.org/sum-array-elements-every-element-x-xored-x-times/)

给定一个整数数组，任务是在对每个元素 x 与其自身进行 x 次异或运算后，计算所有数组元素的和。例如，如果元素是 4，那么我们对这个数和它自己进行异或运算 4 次，就像:= 4^4^4^4
例子:

```
Input :  arr[] = { 1, 2, 3, 5 }
Output :  9 
explanation:  1 + 2^2 + 3^3^3 + 5^5^5^5^5 : 9

Input :   arr[] ={ 5, 6, 7, 9 }
Output :  21
```

一个**简单的解决方法**就是逐个拾取每个数组元素，根据其值与自身进行异或运算。最后给结果加上异或值。
下面是上面想法的实现。

## C++

```
// C++ program to compute sum of all element after
// doing Xor with itself ( element_time)
#include <bits/stdc++.h>
using namespace std;

// function return sum of all XOR element of array
int XorSum(int arr[], int n)
{
    // store result
    int result = 0;

    // Traverse array element and apply XOR
    // operation on it
    for (int i = 0; i < n; i++) {

        // XOR of current element with itself
        // according to value.
        int k = 0;
        for (int j = 1; j <= arr[i]; j++)
            k ^= arr[i];

        result += k;
    }
    return result;
}
// Driver program
int main()
{
    int arr[] = { 1, 2, 6, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << XorSum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute sum of all
// element after doing Xor with itself
// ( element_time)
import java.io.*;

class GFG {

    // function return sum of all XOR
    // element of array
    static int XorSum(int arr[], int n)
    {
        // store result
        int result = 0;

        // Traverse array element and apply
        // XOR operation on it
        for (int i = 0; i < n; i++) {

            // XOR of current element with
            // itself according to value.
            int k = 0;
            for (int j = 1; j <= arr[i]; j++)
                k ^= arr[i];

            result += k;
        }

        return result;
    }

    // Driver program
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 6, 3, 4, 5 };
        int n = arr.length;
        System.out.println(XorSum(arr, n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 计算机编程语言

```
# Python 3 program to compute sum of
# all element after doing Xor with
# itself ( element_time)

# function return sum of all XOR
# element of array
def XorSum(arr, n) :

    # store result
    result = 0

    # Traverse array element and
    # apply XOR operation on it
    for i in range(0, n) :

        # XOR of current element
        # with itself according to
        # value.
        k = 0
        for j in range(1, arr[i]+1) :
            k = k ^ arr[i]

        result = result + k

    return result

# Driver program

arr = [ 1, 2, 6, 3, 4, 5 ]
n = len(arr)
print(XorSum(arr, n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to compute sum of all
// element after doing Xor with itself
// ( element_time)
using System;

class GFG {

    // function return sum of all XOR
    // element of array
    static int XorSum(int []arr, int n)
    {
        // store result
        int result = 0;

        // Traverse array element and apply
        // XOR operation on it
        for (int i = 0; i < n; i++) {

            // XOR of current element with
            // itself according to value.
            int k = 0;
            for (int j = 1; j <= arr[i]; j++)
                k ^= arr[i];

            result += k;
        }

        return result;
    }

    // Driver program
    public static void Main()
    {
        int []arr = { 1, 2, 6, 3, 4, 5 };
        int n = arr.Length;
        Console.WriteLine(XorSum(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute
// sum of all element after
// doing Xor with itself
// ( element_time)

// function return sum of all
// XOR element of array
function XorSum( $arr, $n)
{

    // store result
    $result = 0;

    // Traverse array element
    // and apply XOR
    // operation on it
    for ($i = 0; $i < $n; $i++)
    {

        // XOR of current element
        // with itself according
        // to value.
        $k = 0;
        for ($j = 1; $j <= $arr[$i]; $j++)
            $k ^= $arr[$i];

        $result += $k;
    }
    return $result;
}

    // Driver Code
    $arr = array(1, 2, 6, 3, 4, 5);
    $n = count($arr);
    echo XorSum($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to compute sum of all element after
// doing Xor with itself ( element_time)

// function return sum of all XOR element of array
function XorSum(arr, n)
{
    // store result
    let result = 0;

    // Traverse array element and apply XOR
    // operation on it
    for (let i = 0; i < n; i++) {

        // XOR of current element with itself
        // according to value.
        let k = 0;
        for (let j = 1; j <= arr[i]; j++)
            k ^= arr[i];

        result += k;
    }
    return result;
}
// Driver program
    let arr = [ 1, 2, 6, 3, 4, 5 ];
    let n = arr.length;
    document.write(XorSum(arr, n));

</script>
```

**输出:**

```
9
```

时间复杂度:O(n*m)(这里 m 是数组中的最大元素)
辅助空间:O(1)
**这个问题的高效解**是基于这样一个事实:如果我们对任意一个数与其自身进行异或运算(偶数次)，它会产生 0，如果我们对奇数次进行异或运算，它会产生相同的数。
例如

```
   let number be  : 3  do XOR with itself 3 time
             3^3^3 = 3 
   let number be :  4 do XOR with itself 4 time 
             4^4^4^4 = 0 
  so if number is odd it's mean output is number 
  itself. Else zero  
```

以下是上述思路的实现:

## C++

```
// C++ program to compute sum of all element after
// doing XOR with itself ( element_time)
#include <bits/stdc++.h>
using namespace std;

// function return sum of all XOR element of array
int XorSum(int arr[], int n)
{
    int result = 0;
    for (int i = 0; i < n; i++) {

        // if number is odd then add it to the
        // result else not
        if (arr[i] % 2 != 0)
            result += arr[i];
    }

    return result;
}

// Driver program
int main()
{
    int arr[] = { 1, 2, 6, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << XorSum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute sum of
// all element after doing XOR
// with itself ( element_time)
class GFG {

// function return sum of all
// XOR element of array
static int XorSum(int arr[], int n) {

    int result = 0;
    for (int i = 0; i < n; i++) {

    // if number is odd then add it to the
    // result else not
    if (arr[i] % 2 != 0)
        result += arr[i];
    }

    return result;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {1, 2, 6, 3, 4, 5};
    int n = arr.length;
    System.out.println(XorSum(arr, n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to compute
# sum of all element after
# doing XOR with itself
# ( element_time)

# function return sum of
# all XOR element of array
def XorSum(arr,n):

    result = 0
    for i in range(n):

        # if number is odd then add it to the
        # result else not
        if (arr[i] % 2 != 0):
            result += arr[i]

    return result

# Driver program
arr = [ 1, 2, 6, 3, 4, 5 ]
n = len(arr)

print(XorSum(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to compute sum of
// all element after doing XOR
// with itself ( element_time)
using System;

class GFG {

    // function return sum of all
    // XOR element of array
    static int XorSum(int []arr, int n)
    {

        int result = 0;
        for (int i = 0; i < n; i++) {

        // if number is odd then add it to the
        // result else not
        if (arr[i] % 2 != 0)
            result += arr[i];
        }

        return result;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {1, 2, 6, 3, 4, 5};
        int n = arr.Length;
        Console.WriteLine(XorSum(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute
// sum of all element after
// doing XOR with itself
// ( element_time)

// function return sum of
// all XOR element of array
function XorSum($arr, $n)
{
    $result = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // if number is odd
        // then add it to the
        // result else not
        if ($arr[$i] % 2 != 0)
            $result += $arr[$i];
    }

    return $result;
}

    // Driver Code
    $arr = array(1, 2, 6, 3, 4, 5);
    $n = count($arr);
    echo XorSum($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to compute
// sum of all element after
// doing XOR with itself ( element_time)

// function return sum of all XOR element of array
function XorSum(arr, n)
{
    let result = 0;
    for (let i = 0; i < n; i++) {

        // if number is odd then add it to the
        // result else not
        if (arr[i] % 2 != 0)
            result += arr[i];
    }

    return result;
}

// Driver program
    let arr = [ 1, 2, 6, 3, 4, 5 ];
    let n = arr.length;
    document.write(XorSum(arr, n));

</script>
```

**输出:**

```
9
```

时间复杂度:O(n)
辅助空间:O(1)
本文由**普拉文库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。