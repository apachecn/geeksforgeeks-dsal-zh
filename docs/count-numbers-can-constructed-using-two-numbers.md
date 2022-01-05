# 计数可以用两个数字构成的数字

> 原文:[https://www . geesforgeks . org/count-numbers-can-construct-use-two-numbers/](https://www.geeksforgeeks.org/count-numbers-can-constructed-using-two-numbers/)

给定三个正整数 x，y 和 n，任务是找出从 1 到 n 的所有可以用 x 和 y 构成的数的计数。如果我们可以通过将 x 和/或 y 的任意出现次数相加来得到一个数，则可以用 x 和 y 构成一个数。
**示例:**

```
Input  : n = 10, x = 2, y = 3
Output : 9
We can form 9 out of 10 numbers using 2 and 3
2 = 2, 3 = 3, 4 = 2+2, 5 = 2+3, 6 = 3+3
7 = 2+2+3, 8 = 3+3+2, 9 = 3+3+3
and 10 = 3+3+2+2\. 

Input  : n = 10, x = 5, y = 7
Output : 3
We can form 3 out of 10 numbers using 5 and 7
The numbers are 5, 7 and 10

Input  : n = 15, x = 5, y = 7
Output : 6
We can form 6 out of 10 numbers using 5 and 7.
The numbers are 5, 7, 10, 12, 14 and 15.

Input  : n = 15, x = 2, y = 4
Output : 7
```

一个**简单的解决方案**是写一个递归代码，从 0 开始，进行两次递归调用。一个递归调用增加 x，另一个增加 y。这样我们计算总数。我们需要确保一个数字被计算多次。
一个**有效的解决方案**解决方案是使用大小为 n+1 的布尔数组 arr[]。一个条目 arr[i] = true 意味着我可以用 x 和 y 构成。如果 x 和 y 小于或等于 n，我们将 arr[x]和 arr[y]初始化为 true。我们从两个数字中较小的一个开始遍历数组，并逐个标记所有可以用 x 和 y 构成的数字。下面是实现。

## C++

```
// C++ program to count all numbers that can
// be formed using two number numbers x an y
#include<bits/stdc++.h>
using namespace std;

// Returns count of numbers from 1 to n that can be formed
// using x and y.
int countNums(int n, int x, int y)
{
    // Create an auxiliary array and initialize it
    // as false. An entry arr[i] = true is going to
    // mean that i can be formed using x and y
    vector<bool> arr(n+1, false);

    // x and y can be formed using x and y.
    if (x <= n)
        arr[x] = true;
    if (y <= n)
        arr[y] = true;

    // Initialize result
    int result = 0;

    // Traverse all numbers and increment
    // result if a number can be formed using
    // x and y.
    for (int i=min(x, y); i<=n; i++)
    {
        // If i can be formed using x and y
        if (arr[i])
        {
            // Then i+x and i+y can also be formed
            // using x and y.              
            if (i+x <= n)
                arr[i+x] = true;
            if (i+y <= n)
                arr[i+y] = true;

            // Increment result
            result++;
        }
    }
    return result;
}

// Driver code
int main()
{
    int n = 15, x = 5, y = 7;
    cout << countNums(n, x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all numbers that can
// be formed using two number numbers x an y

class gfg{
// Returns count of numbers from 1 to n that can be formed
// using x and y.
static int countNums(int n, int x, int y)
{
    // Create an auxiliary array and initialize it
    // as false. An entry arr[i] = true is going to
    // mean that i can be formed using x and y
    boolean[] arr=new boolean[n+1];

    // x and y can be formed using x and y.
    if (x <= n)
        arr[x] = true;
    if (y <= n)
        arr[y] = true;

    // Initialize result
    int result = 0;

    // Traverse all numbers and increment
    // result if a number can be formed using
    // x and y.
    for (int i=Math.min(x, y); i<=n; i++)
    {
        // If i can be formed using x and y
        if (arr[i])
        {
            // Then i+x and i+y can also be formed
            // using x and y.            
            if (i+x <= n)
                arr[i+x] = true;
            if (i+y <= n)
                arr[i+y] = true;

            // Increment result
            result++;
        }
    }
    return result;
}

// Driver code
public static void main(String[] args)
{
    int n = 15, x = 5, y = 7;
    System.out.println(countNums(n, x, y));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to count all numbers
# that can be formed using two number
# numbers x an y

# Returns count of numbers from 1
# to n that can be formed using x and y.
def countNums(n, x, y):

    # Create an auxiliary array and
    # initialize it as false. An
    # entry arr[i] = True is going to
    # mean that i can be formed using
    # x and y
    arr = [False for i in range(n + 2)]

    # x and y can be formed using x and y.
    if(x <= n):
        arr[x] = True
    if(y <= n):
        arr[y] = True

    # Initialize result
    result = 0

    # Traverse all numbers and increment
    # result if a number can be formed
    # using x and y.
    for i in range(min(x, y), n + 1):

        # If i can be formed using x and y
        if(arr[i]):

            # Then i+x and i+y can also
            # be formed using x and y.
            if(i + x <= n):
                arr[i + x] = True
            if(i + y <= n):
                arr[i + y] = True

            # Increment result
            result = result + 1

    return result

# Driver code
n = 15
x = 5
y = 7
print(countNums(n, x, y))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count all numbers that can
// be formed using two number numbers x an y

using System;

public class GFG{
    // Returns count of numbers from 1 to n that can be formed
// using x and y.
static int countNums(int n, int x, int y)
{
    // Create an auxiliary array and initialize it
    // as false. An entry arr[i] = true is going to
    // mean that i can be formed using x and y
    bool []arr=new bool[n+1];

    // x and y can be formed using x and y.
    if (x <= n)
        arr[x] = true;
    if (y <= n)
        arr[y] = true;

    // Initialize result
    int result = 0;

    // Traverse all numbers and increment
    // result if a number can be formed using
    // x and y.
    for (int i=Math.Min(x, y); i<=n; i++)
    {
        // If i can be formed using x and y
        if (arr[i])
        {
            // Then i+x and i+y can also be formed
            // using x and y.            
            if (i+x <= n)
                arr[i+x] = true;
            if (i+y <= n)
                arr[i+y] = true;

            // Increment result
            result++;
        }
    }
    return result;
}

// Driver code
    static public void Main (){
        int n = 15, x = 5, y = 7;
        Console.WriteLine(countNums(n, x, y));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all numbers
// that can be formed using two
// number numbers x an y

// Returns count of numbers from
// 1 to n that can be formed
// using x and y.
function countNums($n, $x, $y)
{
    // Create an auxiliary array and
    // initialize it as false. An
    // entry arr[i] = true is going
    // to mean that i can be formed
    // using x and y
    $arr = array_fill(0, $n + 1, false);

    // x and y can be formed
    // using x and y.
    if ($x <= $n)
        $arr[$x] = true;
    if ($y <= $n)
        $arr[$y] = true;

    // Initialize result
    $result = 0;

    // Traverse all numbers and increment
    // result if a number can be formed
    // using x and y.
    for ($i = min($x, $y); $i <= $n; $i++)
    {
        // If i can be formed using
        // x and y
        if ($arr[$i])
        {
            // Then i+x and i+y can also
            // be formed using x and y.        
            if ($i + $x <= $n)
                $arr[$i + $x] = true;
            if ($i+$y <= $n)
                $arr[$i + $y] = true;

            // Increment result
            $result++;
        }
    }
    return $result;
}

// Driver code
$n = 15;
$x = 5;
$y = 7;
echo countNums($n, $x, $y);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to count all numbers that can
// be formed using two number numbers x an y

// Returns count of numbers from 1 to n that can be formed
// using x and y.
function countNums(n, x, y)
{

    // Create an auxiliary array and initialize it
    // as false. An entry arr[i] = true is going to
    // mean that i can be formed using x and y
    arr= Array(n+1).fill(false);

    // x and y can be formed using x and y.
    if (x <= n)
        arr[x] = true;
    if (y <= n)
        arr[y] = true;

    // Initialize result
    var result = 0;

    // Traverse all numbers and increment
    // result if a number can be formed using
    // x and y.
    for (i = Math.min(x, y); i <= n; i++)
    {

        // If i can be formed using x and y
        if (arr[i])
        {

            // Then i+x and i+y can also be formed
            // using x and y.            
            if (i + x <= n)
                arr[i + x] = true;
            if (i + y <= n)
                arr[i + y] = true;

            // Increment result
            result++;
        }
    }
    return result;
}

// Driver code
var n = 15, x = 5, y = 7;
document.write(countNums(n, x, y));

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
6
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由**Shivam Pradhan(anuj _ charm)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息