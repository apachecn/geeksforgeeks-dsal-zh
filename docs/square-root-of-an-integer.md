# 整数的平方根

> 原文:[https://www.geeksforgeeks.org/square-root-of-an-integer/](https://www.geeksforgeeks.org/square-root-of-an-integer/)

给定一个整数 x，求它的平方根。如果 x 不是一个完美的正方形，那么返回楼层(√x)。

**示例:**

```
Input: x = 4
Output: 2
Explanation:  The square root of 4 is 2.

Input: x = 11
Output: 3
Explanation:  The square root of 11 lies in between
3 and 4 so floor of the square root is 3.
```

有很多方法可以解决这个问题。比如[巴比伦法](https://www.geeksforgeeks.org/square-root-of-a-perfect-square/)就是一种方式。
**<u>简单逼近</u>** :求平方根的楼层，从 1 开始尝试全自然数。继续递增该数字，直到该数字的平方大于给定的数字。

*   **算法:**
    1.  创建一个变量(计数器) *i* 并处理一些基本情况，即当给定的数字是 0 或 1 时。
    2.  运行一个循环直到 *i*i < = n* ，其中 n 是给定的数字。将 I 增加 1。
    3.  数字平方根的楼层为*I–1*
*   **实施:**

## C++

```
// A C++ program to find floor(sqrt(x)
#include<bits/stdc++.h>
using namespace std;

// Returns floor of square root of x
int floorSqrt(int x)
{
    // Base cases
    if (x == 0 || x == 1)
    return x;

    // Starting from 1, try all numbers until
    // i*i is greater than or equal to x.
    int i = 1, result = 1;
    while (result <= x)
    {
      i++;
      result = i * i;
    }
    return i - 1;
}

// Driver program
int main()
{
    int x = 11;
    cout << floorSqrt(x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find floor(sqrt(x))

class GFG {

    // Returns floor of square root of x
    static int floorSqrt(int x)
    {
        // Base cases
        if (x == 0 || x == 1)
            return x;

        // Starting from 1, try all numbers until
        // i*i is greater than or equal to x.
        int i = 1, result = 1;

        while (result <= x) {
            i++;
            result = i * i;
        }
        return i - 1;
    }

    // Driver program
    public static void main(String[] args)
    {
        int x = 11;
        System.out.print(floorSqrt(x));
    }
}

// This code is contributed by Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python3 program to find floor(sqrt(x)

# Returns floor of square root of x
def floorSqrt(x):

    # Base cases
    if (x == 0 or x == 1):
        return x

    # Starting from 1, try all numbers until
    # i*i is greater than or equal to x.
    i = 1; result = 1
    while (result <= x):

        i += 1
        result = i * i

    return i - 1

# Driver Code
x = 11
print(floorSqrt(x))

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// A C# program to
// find floor(sqrt(x))
using System;

class GFG
{
    // Returns floor of
    // square root of x
    static int floorSqrt(int x)
    {
        // Base cases
        if (x == 0 || x == 1)
            return x;

        // Starting from 1, try all
        // numbers until i*i is
        // greater than or equal to x.
        int i = 1, result = 1;

        while (result <= x)
        {
            i++;
            result = i * i;
        }
        return i - 1;
    }

    // Driver Code
    static public void Main ()
    {
        int x = 11;
        Console.WriteLine(floorSqrt(x));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find floor(sqrt(x)

// Returns floor of square root of x
function floorSqrt($x)
{
    // Base cases
    if ($x == 0 || $x == 1)
    return $x;

    // Starting from 1, try all
    // numbers until i*i is
    // greater than or equal to x.
    $i = 1;
    $result = 1;
    while ($result <= $x)
    {
        $i++;
        $result = $i * $i;
    }
    return $i - 1;
}

// Driver Code
$x = 11;
echo floorSqrt($x), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// A Javascript program to find floor(sqrt(x)

// Returns floor of square root of x
function floorSqrt(x)
{

    // Base cases
    if (x == 0 || x == 1)
        return x;

    // Starting from 1, try all
    // numbers until i*i is
    // greater than or equal to x.
    let i = 1;
    let result = 1;

    while (result <= x)
    {
        i++;
        result = i * i;
    }
    return i - 1;
}

// Driver Code
let x = 11;
document.write(floorSqrt(x));

// This code is contributed by mohan

</script>
```

**输出:**

```
3
```

*   **复杂度分析:**
    *   **时间复杂度:** O(√ n)。
        只需要对解进行一次遍历，因此时间复杂度为 O(√ n)。
    *   **空间复杂度:** O(1)。
        需要持续的额外空间。

*感谢 Fattepur Mahesh 提出这个解决方案。*
**<u>更好的逼近</u> :** 思路是找出平方小于等于给定数的最大整数 *i* 。想法是用[二分搜索法](http://geeksquiz.com/binary-search/)解决问题。i * i 的值是单调递增的，所以这个问题可以用二分搜索法来解决。

*   **算法:**
    1.  注意一些基本情况，即当给定的数字是 0 或 1 时。
    2.  创建一些变量，下限 *l = 0* ，上限 *r = n* ，其中 n 是给定的数字，*中*和 *ans* 存储答案。
    3.  运行一个循环直到 *l < = r* ，搜索空间消失
    4.  检查 mid ( *mid = (l + r)/2* )的平方是否小于或等于 n，如果是，则在搜索空间的后半部分搜索更大的值，即 l = mid + 1，更新 ans = mid
    5.  否则，如果 mid 的平方大于 n，则在搜索空间的前半部分搜索较小的值，即 r = mid–1
    6.  打印答案的值(*和*)
*   **实施:**

## C++

```
#include <iostream>

using namespace std;
int floorSqrt(int x)
{
    // Base cases
    if (x == 0 || x == 1)
        return x;

    // Do Binary Search for floor(sqrt(x))
    int start = 1, end = x/2, ans;
    while (start <= end) {
        int mid = (start + end) / 2;

        // If x is a perfect square
        int sqr = mid * mid;
        if (sqr == x)
            return mid;

        // Since we need floor, we update answer when
        // mid*mid is smaller than x, and move closer to
        // sqrt(x)

        /*
           if(mid*mid<=x)
                   {
                           start = mid+1;
                           ans = mid;
                   }
            Here basically if we multiply mid with itself so
           there will be integer overflow which will throw
           tle for larger input so to overcome this
           situation we can use long or we can just divide
            the number by mid which is same as checking
           mid*mid < x

           */
        if (sqr <= x) {
            start = mid + 1;
            ans = mid;
        }
        else // If mid*mid is greater than x
            end = mid - 1;
    }
    return ans;
}

// Driver program
int main()
{
    int x = 20221;
    cout << floorSqrt(x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find floor(sqrt(x)
public class Test
{
    public static int floorSqrt(int x)
    {
        // Base Cases
        if (x == 0 || x == 1)
            return x;

        // Do Binary Search for floor(sqrt(x))
        long start = 1, end = x, ans=0;
        while (start <= end)
        {
            int mid = (start + end) / 2;

            // If x is a perfect square
            if (mid*mid == x)
                return (int)mid;

            // Since we need floor, we update answer when mid*mid is
            // smaller than x, and move closer to sqrt(x)
            if (mid*mid < x)
            {
                start = mid + 1;
                ans = mid;
            }
            else   // If mid*mid is greater than x
                end = mid-1;
        }
        return (int)ans;
    }

    // Driver Method
    public static void main(String args[])
    {
        int x = 11;
        System.out.println(floorSqrt(x));
    }
}
// Contributed by InnerPeace
```

## 蟒蛇 3

```
# Python 3 program to find floor(sqrt(x)

# Returns floor of square root of x        
def floorSqrt(x) :

    # Base cases
    if (x == 0 or x == 1) :
        return x

    # Do Binary Search for floor(sqrt(x))
    start = 1
    end = x  
    while (start <= end) :
        mid = (start + end) // 2

        # If x is a perfect square
        if (mid*mid == x) :
            return mid

        # Since we need floor, we update
        # answer when mid*mid is smaller
        # than x, and move closer to sqrt(x)
        if (mid * mid < x) :
            start = mid + 1
            ans = mid

        else :

            # If mid*mid is greater than x
            end = mid-1

    return ans

# driver code   
x = 11
print(floorSqrt(x))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A C# program to
// find floor(sqrt(x)
using System;

class GFG
{
    public static int floorSqrt(int x)
    {
        // Base Cases
        if (x == 0 || x == 1)
            return x;

        // Do Binary Search
        // for floor(sqrt(x))
        int start = 1, end = x, ans = 0;
        while (start <= end)
        {
            int mid = (start + end) / 2;

            // If x is a
            // perfect square
            if (mid * mid == x)
                return mid;

            // Since we need floor, we
            // update answer when mid *
            // mid is smaller than x,
            // and move closer to sqrt(x)
            if (mid * mid < x)
            {
                start = mid + 1;
                ans = mid;
            }

            // If mid*mid is
            // greater than x
            else
                end = mid-1;
        }
        return ans;
    }

    // Driver Code
    static public void Main ()
    {
        int x = 11;
        Console.WriteLine(floorSqrt(x));
    }
}

// This code is Contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find floor(sqrt(x)

// Returns floor of
// square root of x        
function floorSqrt($x)
{
    // Base cases
    if ($x == 0 || $x == 1)
    return $x;

    // Do Binary Search
    // for floor(sqrt(x))
    $start = 1; $end = $x; $ans;
    while ($start <= $end)
    {
        $mid = ($start + $end) / 2;

        // If x is a perfect square
        if ($mid * $mid == $x)
            return $mid;

        // Since we need floor, we update
        // answer when mid*mid is  smaller
        // than x, and move closer to sqrt(x)
        if ($mid * $mid < $x)
        {
            $start = $mid + 1;
            $ans = $mid;
        }

        // If mid*mid is
        // greater than x
        else
            $end = $mid-1;    
    }
    return $ans;
}

// Driver Code
$x = 11;
echo floorSqrt($x), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // A Javascript program to find floor(sqrt(x)

// Returns floor of
// square root of x        
function floorSqrt(x)
{
    // Base cases
    if (x == 0 || x == 1)
    return x;

    // Do Binary Search
    // for floor(sqrt(x))
    let start = 1;
    let end = x;
    let ans;
    while (start <= end)
    {
        let mid = (start + end) / 2;

        // If x is a perfect square
        if (mid * mid == x)
            return mid;

        // Since we need floor, we update
        // answer when mid*mid is  smaller
        // than x, and move closer to sqrt(x)
        if (mid * mid < x)
        {
            start = mid + 1;
            ans = mid;
        }

        // If mid*mid is
        // greater than x
        else
            end = mid-1;    
    }
    return ans;
}

// Driver Code
let x = 11;
document.write(floorSqrt(x) +  "<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
142
```

*   **复杂度分析:**
    *   **时间复杂度:** O(log n)。
        二分搜索法的时间复杂度为 O(log n)。
    *   **空间复杂度:** O(1)。
        需要持续的额外空间。

感谢[高拉夫·阿赫瓦尔](http://qa.geeksforgeeks.org/user/Mr.Lazy)提出上述方法。
**注:**二分搜索法可以进一步优化，以‘开始’= 0 和‘结束’= x/2 开始。当 x >为 1 时，x 的平方根不能大于 x/2。
感谢 **vinit** 提出上述优化建议。

**更好的方法:**逻辑很简单，因为我们可以观察到，对于一个完美的平方数，它的平方根代表从 **1 到 x** 的完美平方的总数。

例如:- sqrt(1)=1，sqrt(4)=2，sqrt(9)=3 ...-什么就这样.

*   **算法:**

1.找到 x 的平方根并存储在变量 sqrt 中。

2.使用 sqrt 的最低值并存储在变量结果中，因为对于非完美平方数，它的最低值给出结果。

3.返回结果。

*   **实施:**

## 蟒蛇 3

```
def countSquares(x):
  count = 0
  sqrt = x**0.5
  result = int(sqrt)
  return result
x = 9
print(countSquares(x))
```

**输出:**

```
3
```

*   **复杂度分析:**

**1。时间复杂度:- O(1)**

**2。空间复杂度:- O(1)**

感谢 aakashpanda2000 提出上述方法。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息