# 数组元素乘法程序

> 原文:[https://www . geesforgeks . org/program-乘法-数组-元素/](https://www.geeksforgeeks.org/program-multiplication-array-elements/)

给我们一个数组，我们必须使用迭代和递归方法来计算数组的乘积。

**示例:**

```
Input : array[] = {1, 2, 3, 4, 5, 6}
Output : 720
Here, product of elements = 1*2*3*4*5*6 = 720

Input : array[] = {1, 3, 5, 7, 9}
Output : 945 
```

**迭代方法:**
我们将结果初始化为 1。我们从左到右遍历数组，并将元素与结果相乘。

## C++

```
// Iterative C++ program to
// multiply array elements
#include<bits/stdc++.h>

using namespace std;

// Function to calculate the
// product of the array
int multiply(int array[], int n)
{
    int pro = 1;
    for (int i = 0; i < n; i++)
        pro = pro * array[i];
    return pro;
}

// Driver Code
int main()
{
    int array[] = {1, 2, 3, 4, 5, 6};
    int n = sizeof(array) / sizeof(array[0]);

    // Function call to calculate product
    cout << multiply(array, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to
// multiply array elements
class GFG
{
    static int arr[] = {1, 2, 3, 4, 5, 6};

    // Method to calculate the
    // product of the array
    static int multiply()
    {
        int pro = 1;
        for (int i = 0; i < arr.length; i++)
            pro = pro * arr[i];
        return pro;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Method call to calculate product
        System.out.println(multiply());
        }
}
```

## 蟒蛇 3

```
# Iterative Python3 code to
# multiply list elements

# Function to calculate
# the product of the array
def multiply( array , n ):
    pro = 1
    for i in range(n):
        pro = pro * array[i]
    return pro

# Driver code
array = [1, 2, 3, 4, 5, 6]
n = len(array)

# Function call to
# calculate product
print(multiply(array, n))

# This code is contributed
# by "Sharad_Bhardwaj".
```

## C#

```
// Iterative C# program to
// multiply array elements
using System;

class GFG
{
    static int []arr = {1, 2, 3, 4, 5, 6};

    // Method to calculate the
    // product of the array
    static int multiply()
    {
        int pro = 1;
        for (int i = 0; i < arr.Length; i++)
            pro = pro * arr[i];
        return pro;
    }

    // Driver Code
    public static void Main()
    {
        // Method call to calculate product
        Console.Write(multiply());
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Iterative PHP program to
// multiply array elements

// Function to calculate the
// product of the array
function multiply($arr, $n)
{
    $pro = 1;
    for ($i = 0; $i < $n; $i++)
        $pro = $pro * $arr[$i];
    return $pro;
}

// Driver Code
$arr = array(1, 2, 3, 4, 5, 6);
$n = sizeof($arr) / sizeof($arr[0]);

// Function call to
// calculate product
echo multiply($arr, $n);
return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Iterative javascript program to
// multiply array elements

    var arr = [ 1, 2, 3, 4, 5, 6 ];

    // Method to calculate the
    // product of the array
    function multiply() {
        var pro = 1;
        for (i = 0; i < arr.length; i++)
            pro = pro * arr[i];
        return pro;
    }

    // Driver Code

        // Method call to calculate product
        document.write(multiply());

// This code contributed by aashish1995

</script>
```

**输出:**

```
720
```

**递归方法:**

## C++

```
// Recursive C++ program to
// multiply array elements
#include<iostream>

using namespace std;

// Function to calculate the
// product of array using recursion
int multiply(int a[], int n)
{
    // Termination condition
    if (n == 0)
        return(a[n]);
    else
        return (a[n] * multiply(a, n - 1));
}

// Driver Code
int main()
{
    int array[] = {1, 2, 3, 4, 5, 6};
    int n = sizeof(array) / sizeof(array[0]);

    // Function call to
    // calculate the product
    cout << multiply(array, n - 1)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to
// multiply array elements
class GFG
{
    static int arr[] = {1, 2, 3, 4, 5, 6};

    // Method to calculate the product
    // of the array using recursion
    static int multiply(int a[], int n)
    {
        // Termination condition
        if (n == 0)
            return(a[n]);
        else
            return (a[n] * multiply(a, n - 1));
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Method call to
        // calculate product
        System.out.println(multiply(arr,
                       arr.length - 1));
        }
}
```

## 蟒蛇 3

```
# Recursive Python3 code
# to multiply array elements

# Function to calculate the product 
# of array using recursion
def multiply( a , n ):

    # Termination condition
    if n == 0:
        return(a[n])
    else:
        return (a[n] * multiply(a, n - 1))

# Driver Code
array = [1, 2, 3, 4, 5, 6]
n = len(array)

# Function call to
# calculate the product
print(multiply(array, n - 1))

# This code is contributed
# by "Sharad_Bhardwaj".
```

## C#

```
// Recursive C# program to
// multiply array elements
using System;

class GFG
{

    static int []arr = {1, 2, 3, 4, 5, 6};

    // Method to calculate the product
    // of the array using recursion
    static int multiply(int []a, int n)
    {

        // Termination condition
        if (n == 0)
            return(a[n]);
        else
            return (a[n] * multiply(a, n - 1));
    }

    // Driver Code
    public static void Main()
    {

        // Method call to
        // calculate product
        Console.Write(multiply(arr,
                               arr.Length - 1));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to
// multiply array elements

// Function to calculate the
// product of array using recursion
function multiply( $a, $n)
{
    // Termination condition
    if ($n == 0)
        return($a[$n]);
    else
        return ($a[$n] *
                 multiply($a, $n - 1));
}

// Driver Code
$array = array(1, 2, 3, 4, 5, 6);
$n = count($array);

// Function call to
// calculate the product
echo multiply($array, $n - 1)

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Recursive javascript program to
// multiply array elements

    var arr = [ 1, 2, 3, 4, 5, 6 ];

    // Method to calculate the product
    // of the array using recursion
    function multiply(a , n) {
        // Termination condition
        if (n == 0)
            return (a[n]);
        else
            return (a[n] * multiply(a, n - 1));
    }

    // Driver Code

        // Method call to
        // calculate product
        document.write(multiply(arr,
                       arr.length - 1));

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
720
```

本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。