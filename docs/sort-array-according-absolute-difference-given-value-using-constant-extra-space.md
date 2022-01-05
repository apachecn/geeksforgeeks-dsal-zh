# 根据给定值的绝对差值排序数组“使用恒定的额外空间”

> 原文:[https://www . geeksforgeeks . org/sort-array-根据绝对差值-给定值-使用常量-额外空间/](https://www.geeksforgeeks.org/sort-array-according-absolute-difference-given-value-using-constant-extra-space/)

给定 n 个不同元素和一个数 x 的数组，根据与 x 的绝对差排列数组元素，即具有最小差的元素排在第一位，以此类推，使用恒定的额外空间。
注意:如果两个或多个元素距离相等，则按照给定数组中的相同顺序排列它们。
**例:**

```
Input  : arr[] = {10, 5, 3, 9, 2}
             x = 7
Output : arr[] = {5, 9, 10, 3, 2}
Explanation : 
7 - 10 = 3(abs)
7 - 5 = 2
7 - 3 = 4 
7 - 9 = 2(abs)
7 - 2 = 5
So according to the difference with X, 
elements are arranged as 5, 9, 10, 3, 2.

Input  : arr[] = {1, 2, 3, 4, 5}
             x = 6
Output : arr[] = {5, 4, 3, 2, 1}
```

上面的问题在之前的帖子[这里](https://www.geeksforgeeks.org/sort-an-array-according-to-absolute-difference-with-given-value/)已经解释过了。它需要 0(n ^ n)的时间和 0(n)的额外空间。下面的解决方案虽然具有相对较差的时间复杂度(即 O(n^2)，但它在不使用任何额外空间或内存的情况下完成工作。
解决方案是基于[插入排序](https://www.geeksforgeeks.org/insertion-sort/)。对于每个 i (1 < = i < n)，我们将 arr[i]之差的绝对值与给定的数字 x 进行比较(假设这是“diff”)。然后，我们将这种差异与 abs(arr[j]-x)的差异进行比较，其中 0 < = j < i(如果 abdiff，让它为 1)。如果 diff 大于 abdiff，我们会移动数组中的值，以适应 arr[i]的正确位置。

## C++

```
// C++ program to sort an array based on absolute
// difference with a given value x.
#include <bits/stdc++.h>
using namespace std;

void arrange(int arr[], int n, int x)
{
    // Below lines are similar to insertion sort
    for (int i = 1; i < n; i++) {
        int diff = abs(arr[i] - x);

        // Insert arr[i] at correct place
        int j = i - 1;
        if (abs(arr[j] - x) > diff) {
            int temp = arr[i];
            while (abs(arr[j] - x) > diff && j >= 0) {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = temp;
        }
    }
}

// Function to print the array
void print(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Main Function
int main()
{
    int arr[] = { 10, 5, 3, 9, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 7;

    arrange(arr, n, x);
    print(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array based on absolute
// difference with a given value x.
class GFG {

static void arrange(int arr[], int n, int x)
{
    // Below lines are similar to insertion sort
    for (int i = 1; i < n; i++) {
        int diff = Math.abs(arr[i] - x);

        // Insert arr[i] at correct place
        int j = i - 1;
        if (Math.abs(arr[j] - x) > diff)
        {
            int temp = arr[i];
            while (j >= 0 && Math.abs(arr[j] - x) > diff)
            {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = temp;
        }
    }
}

// Function to print the array
static void print(int arr[], int n)
{
    for (int i = 0; i < n; i++)
    System.out.print(arr[i] + " ");
}

// Driver code
public static void main(String[] args) {
    int arr[] = { 10, 5, 3, 9, 2 };
    int n = arr.length;
    int x = 7;

    arrange(arr, n, x);
    print(arr, n);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to sort an array
# based on absolute difference with
# a given value x.
def arrange(arr, n, x):

    # Below lines are similar to
    # insertion sort
    for i in range(1, n) :
        diff = abs(arr[i] - x)

        # Insert arr[i] at correct place
        j = i - 1
        if (abs(arr[j] - x) > diff) :
            temp = arr[i]
            while (abs(arr[j] - x) >
                       diff and j >= 0) :
                arr[j + 1] = arr[j]
                j -= 1

            arr[j + 1] = temp

# Function to print the array
def print_1(arr, n):

    for i in range(n):
        print(arr[i], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 10, 5, 3, 9, 2 ]
    n = len(arr)
    x = 7

    arrange(arr, n, x)
    print_1(arr, n)

# This code is contributed by ita_c
```

## C#

```
// C# program to sort an array based on absolute
// difference with a given value x.
using System;

class GFG
{

    static void arrange(int []arr, int n, int x)
    {

        // Below lines are similar to insertion sort
        for (int i = 1; i < n; i++)
        {
            int diff = Math.Abs(arr[i] - x);

            // Insert arr[i] at correct place
            int j = i - 1;
            if (Math.Abs(arr[j] - x) > diff)
            {
                int temp = arr[i];
                while (j >= 0 && Math.Abs(arr[j] - x) > diff)
                {
                    arr[j + 1] = arr[j];
                    j--;
                }
                arr[j + 1] = temp;
            }
        }
    }

    // Function to print the array
    static void print(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 10, 5, 3, 9, 2 };
        int n = arr.Length;
        int x = 7;

        arrange(arr, n, x);
        print(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to sort an array based on
// absolute difference with a given value x.

function arrange($arr, $n, $x)
{
    // Below lines are similar to
    // insertion sort
    for ($i = 1; $i < $n; $i++)
    {
        $diff = abs($arr[$i] - $x);

        // Insert arr[i] at correct place
        $j = $i - 1;
        if (abs($arr[$j] - $x) > $diff)
        {
            $temp = $arr[$i];
            while (abs($arr[$j] - $x) >
                       $diff && $j >= 0)
            {
                $arr[$j + 1] = $arr[$j];
                $j--;
            }
            $arr[$j + 1] = $temp;
        }
    }
    return $arr;
}

// Function to print the array
function print_arr($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
}

// Driver Code
$arr = array(10, 5, 3, 9, 2);
$n = sizeof($arr);
$x = 7;

$arr1 = arrange($arr, $n, $x);
print_arr($arr1, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to sort
// an array based on absolute
// difference with a given value x.

    function arrange(arr,n,x)
    {
        // Below lines are similar
        // to insertion sort
    for (let i = 1; i < n; i++) {
        let diff = Math.abs(arr[i] - x);

        // Insert arr[i] at correct place
        let j = i - 1;
        if (Math.abs(arr[j] - x) > diff)
        {
            let temp = arr[i];
            while (j >= 0 &&
            Math.abs(arr[j] - x) > diff)
            {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = temp;
        }
    }
    }

    // Function to print the array
    function  print(arr,n)
    {
        for (let i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    // Driver code
    let arr=[10, 5, 3, 9, 2 ];
    let n = arr.length;
    let x = 7;
    arrange(arr, n, x);
    print(arr, n);

    // This code is contributed
    // by avanitrachhadiya2155

</script>
```

**输出:**

```
5 9 10 3 2
```

**时间复杂度:** O(n^2)其中 n 是数组的大小。
**辅助空间:** O(1)
本文由**罗黑饶**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。