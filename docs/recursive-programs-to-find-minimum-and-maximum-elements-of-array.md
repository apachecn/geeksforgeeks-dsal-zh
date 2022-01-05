# 寻找数组最小和最大元素的递归程序

> 原文:[https://www . geesforgeks . org/递归程序查找最小和最大数组元素/](https://www.geeksforgeeks.org/recursive-programs-to-find-minimum-and-maximum-elements-of-array/)

给定一个整数数组 **arr** ，任务是使用递归找到该数组的最小和最大元素。

**示例:**

```
Input: arr = {1, 4, 3, -5, -4, 8, 6};
Output: min = -5, max = 8

Input: arr = {1, 4, 45, 6, 10, -8};
Output: min = -8, max = 45
```

**<u>递归法求数组中的最小元素</u>**

**进场:**

*   获取要找到最小值的数组
*   根据以下等式递归查找最小值:
    *   从末尾递归遍历数组
    *   **基本情况:**如果剩余数组长度为 1，则返回唯一存在的元素，即 arr[0]

```
if(n == 1)
   return arr[0];
```

*   **递归调用:**如果不满足基本情况，那么通过从末尾传递一个小一号的数组来调用函数，即从 arr[0]到 arr[n-1]。
*   **Return 语句:**在每次递归调用时(基本情况除外)，返回当前数组最后一个元素(即 arr[n-1])的最小值和上一次递归调用返回的元素。

```
return min(arr[n-1], recursive_function(arr, n-1));
```

*   打印递归函数返回的元素作为最小元素

**递归函数的伪代码:**

```
If there is single element, return it.
Else return minimum of following.
    a) Last Element
    b) Value returned by recursive call
       fir n-1 elements.
```

下面是上述方法的实现:

## C++

```
// Recursive C++ program to find minimum

#include <iostream>
using namespace std;

// function to print Minimum element using recursion
int findMinRec(int A[], int n)
{
    // if size = 0 means whole array has been traversed
    if (n == 1)
        return A[0];
    return min(A[n-1], findMinRec(A, n-1));
}

// driver code to test above function
int main()
{
    int A[] = {1, 4, 45, 6, -50, 10, 2};
    int n = sizeof(A)/sizeof(A[0]);
    cout <<  findMinRec(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to find minimum
import java.util.*;

class GFG {

    // function to return minimum element using recursion
    public static int findMinRec(int A[], int n)
    {
      // if size = 0 means whole array
      // has been traversed
      if(n == 1)
        return A[0];

        return Math.min(A[n-1], findMinRec(A, n-1));
    }

    // Driver code
    public static void main(String args[])
    {
        int A[] = {1, 4, 45, 6, -50, 10, 2};
        int n = A.length;

        // Function calling
        System.out.println(findMinRec(A, n));
    }
}

//This code is contributed by Niraj_Pandey
```

## 蟒蛇 3

```
# Recursive python 3 program to
# find minimum

# function to print Minimum element
# using recursion
def findMinRec(A, n):

    # if size = 0 means whole array
    # has been traversed
    if (n == 1):
        return A[0]
    return min(A[n - 1], findMinRec(A, n - 1))

# Driver Code
if __name__ == '__main__':
    A = [1, 4, 45, 6, -50, 10, 2]
    n = len(A)
    print(findMinRec(A, n))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// Recursive C# program to find minimum
using System;

class GFG
{

// function to return minimum
// element using recursion
public static int findMinRec(int []A,
                             int n)
{
// if size = 0 means whole array
// has been traversed
if(n == 1)
    return A[0];

    return Math.Min(A[n - 1],
                    findMinRec(A, n - 1));
}

// Driver code
static public void Main ()
{
    int []A = {1, 4, 45, 6, -50, 10, 2};
    int n = A.Length;

    // Function calling
    Console.WriteLine(findMinRec(A, n));
}
}

// This code is contributed by Sachin
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to find minimum

// function to print Minimum
// element using recursion
function findMinRec($A, $n)
{

    // if size = 0 means whole
    // array has been traversed
    if ($n == 1)
        return $A[0];
    return min($A[$n - 1], findMinRec($A, $n - 1));
}

    // Driver Code
    $A = array (1, 4, 45, 6, -50, 10, 2);
    $n = sizeof($A);
    echo findMinRec($A, $n);

// This code is contributed by akt
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum

// Function to print Minimum
// element using recursion
function findMinRec(A, n)
{

    // If size = 0 means whole
    // array has been traversed
    if (n == 1)
        return A[0];

    return Math.min(A[n - 1],
        findMinRec(A, n - 1));
}

// Driver Code
let A = [ 1, 4, 45, 6, -50, 10, 2 ];
let n = A.length;

document.write( findMinRec(A, n));

// This code is contributed by sravan kumar G

</script>
```

**输出:**

```
-50
```

**<u>递归法求数组中最大元素</u>**

**进场:**

*   获取要找到最大值的数组
*   根据以下等式递归查找最大值:
    *   从末尾递归遍历数组
    *   **基本情况:**如果剩余数组长度为 1，则返回唯一存在的元素，即 arr[0]

```
if(n == 1)
   return arr[0];
```

*   **递归调用:**如果不满足基本情况，那么通过从末尾传递一个小一号的数组来调用函数，即从 arr[0]到 arr[n-1]。
*   **Return 语句:**每次递归调用时(基本情况除外)，返回当前数组最后一个元素(即 arr[n-1])的最大值和上一次递归调用返回的元素。

```
return max(arr[n-1], recursive_function(arr, n-1));
```

*   将递归函数返回的元素打印为最大元素

**递归函数的伪代码:**

```
If there is single element, return it.
Else return maximum of following.
    a) Last Element
    b) Value returned by recursive call
       fir n-1 elements.
```

下面是上述方法的实现:

## C++

```
// Recursive C++ program to find maximum
#include <iostream>
using namespace std;

// function to return maximum element using recursion
int findMaxRec(int A[], int n)
{
    // if n = 0 means whole array has been traversed
    if (n == 1)
        return A[0];
    return max(A[n-1], findMaxRec(A, n-1));
}

// driver code to test above function
int main()
{
    int A[] = {1, 4, 45, 6, -50, 10, 2};
    int n = sizeof(A)/sizeof(A[0]);
    cout <<  findMaxRec(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to find maximum
import java.util.*;

class GFG {

    // function to return maximum element using recursion
    public static int findMaxRec(int A[], int n)
    {
      // if size = 0 means whole array
      // has been traversed
      if(n == 1)
        return A[0];

        return Math.max(A[n-1], findMaxRec(A, n-1));
    }

    // Driver code
    public static void main(String args[])
    {
        int A[] = {1, 4, 45, 6, -50, 10, 2};
        int n = A.length;

        // Function calling
        System.out.println(findMaxRec(A, n));
    }
}

//This code is contributed by Niraj_Pandey
```

## 蟒蛇 3

```
# Recursive Python 3 program to
# find maximum

# function to return maximum element
# using recursion
def findMaxRec(A, n):

    # if n = 0 means whole array
    # has been traversed
    if (n == 1):
        return A[0]
    return max(A[n - 1], findMaxRec(A, n - 1))

# Driver Code
if __name__ == "__main__":

    A = [1, 4, 45, 6, -50, 10, 2]
    n = len(A)
    print(findMaxRec(A, n))

# This code is contributed by ita_c
```

## C#

```
// Recursive C# program to find maximum
using System;

class GFG
{
// function to return maximum
// element using recursion
public static int findMaxRec(int []A,
                             int n)
{
// if size = 0 means whole array
// has been traversed
if(n == 1)
    return A[0];

    return Math.Max(A[n - 1],
                    findMaxRec(A, n - 1));
}

// Driver code
static public void Main ()
{
    int []A = {1, 4, 45, 6, -50, 10, 2};
    int n = A.Length;

    // Function calling
    Console.WriteLine(findMaxRec(A, n));
}
}

// This code is contributed by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to find maximum

// function to return maximum
// element using recursion
function findMaxRec($A, $n)
{
    // if n = 0 means whole array
    // has been traversed
    if ($n == 1)
        return $A[0];
    return max($A[$n - 1],
        findMaxRec($A, $n - 1));
}

// Driver Code
$A = array(1, 4, 45, 6, -50, 10, 2);
$n = sizeof($A);
echo findMaxRec($A, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Recursive Java program to find maximum

// Function to return maximum element
// using recursion
function findMaxRec(A, n)
{

    // If size = 0 means whole array
    // has been traversed
    if (n == 1)
        return A[0];

    return Math.max(A[n - 1],
        findMaxRec(A, n - 1));
}

// Driver code
let A = [ 1, 4, 45, 6, -50, 10, 2 ];
let n = A.length;

// Function calling
document.write(findMaxRec(A, n));

// This code is contributed by sravan kumar G

</script>
```

**输出:**

```
45
```

**相关文章:**
[程序寻找数组中最大的元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

本文由 [**普拉蒂克·查哈尔**](https://pratik-chhajer.github.io/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。