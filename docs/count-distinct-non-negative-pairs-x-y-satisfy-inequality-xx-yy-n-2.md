# 计算满足不等式 x*x + y*y 的不同非负整数对(x，y)<n

> 原文:[https://www . geesforgeks . org/count-distinct-non-negative-pairs-x-y-submit-不等式-xx-yy-n-2/](https://www.geeksforgeeks.org/count-distinct-non-negative-pairs-x-y-satisfy-inequality-xx-yy-n-2/)

给定一个正数 n，计算所有满足不等式 x*x + y*y < n 的非负整数对(x，y)

**示例:**

```
Input:  n = 5
Output: 6
The pairs are (0, 0), (0, 1), (1, 0), (1, 1), (2, 0), (0, 2)

Input: n = 6
Output: 8
The pairs are (0, 0), (0, 1), (1, 0), (1, 1), (2, 0), (0, 2),
              (1, 2), (2, 1)
```

一个**简单的解决方案**是运行两个循环。外环适用于所有可能的 x 值(从 0 到√n)。内部循环为 x 的当前值选择所有可能的 y 值(由外部循环选择)。

下面是一个简单解决方案的实现。

## C++

```
#include <iostream>
using namespace std;

// This function counts number of pairs (x, y) that satisfy
// the inequality x*x + y*y < n.
int countSolutions(int n)
{
   int res = 0;
   for (int x = 0; x*x < n; x++)
      for (int y = 0; x*x + y*y < n; y++)
         res++;
   return res;
}

// Driver program to test above function
int main()
{
    cout << "Total Number of distinct Non-Negative pairs is "
         << countSolutions(6) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Count Distinct
// Non-Negative Integer Pairs
// (x, y) that Satisfy the
// inequality x*x + y*y < n
import java.io.*;

class GFG
{
    // This function counts number
    // of pairs (x, y) that satisfy
    // the inequality x*x + y*y < n.
    static int countSolutions(int n)
    {
        int res = 0;
        for (int x = 0; x * x < n; x++)
            for (int y = 0; x * x + y * y < n; y++)
                res++;

        return res;
    }

    // Driver program
    public static void main(String args[])
    {
        System.out.println ( "Total Number of distinct Non-Negative pairs is "
                                                        +countSolutions(6));

    }
}

// This article is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# This function counts number of pairs
# (x, y) that satisfy
# the inequality x*x + y*y < n.
def countSolutions(n):

    res = 0
    x = 0
    while(x * x < n):
        y = 0
        while(x * x + y * y < n):
            res = res + 1
            y = y + 1
        x = x + 1

    return res

# Driver program to test above function
if __name__=='__main__':
    print("Total Number of distinct Non-Negative pairs is ",
         countSolutions(6))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# code to Count Distinct
// Non-Negative Integer Pairs
// (x, y) that Satisfy the
// inequality x*x + y*y < n
using System;

class GFG {

    // This function counts number
    // of pairs (x, y) that satisfy
    // the inequality x*x + y*y < n.
    static int countSolutions(int n)
    {
        int res = 0;

        for (int x = 0; x*x < n; x++)
            for (int y = 0; x*x + y*y < n; y++)
                res++;

        return res;
    }

    // Driver program
    public static void Main()
    {
        Console.WriteLine( "Total Number of "
          + "distinct Non-Negative pairs is "
                        + countSolutions(6));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program Count Distinct
// Non-Negative Integer Pairs
// (x, y) that Satisfy the
// Inequality x*x + y*y < n

// function counts number of
// pairs (x, y) that satisfy
// the inequality x*x + y*y < n.
function countSolutions($n)
{
    $res = 0;
    for($x = 0; $x * $x < $n; $x++)
        for($y = 0; $x * $x + $y * $y < $n; $y++)
            $res++;
    return $res;
}

// Driver Code
{
    echo "Total Number of distinct Non-Negative pairs is ";
    echo countSolutions(6) ;
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// This function counts number
// of pairs (x, y) that satisfy
// the inequality x*x + y*y < n.

function countSolutions( n){
   let res = 0;
   for (let x = 0; x*x < n; x++){
      for (let y = 0; x*x + y*y < n; y++){
         res++;
      }
   }
   return res;
}

// Driver program to test above function
document.write("Total Number of distinct Non-Negative pairs is "+countSolutions(6));

</script>
```

**输出:**

```
Total Number of distinct Non-Negative pairs is 8
```

上述解的时间复杂度的上限是 O(n)。外环运行√n 次。内环最多运行√n 次。

**辅助空间:** O(1)

使用**高效解决方案**，我们可以找到 O(√n)时间内的计数。其思想是首先找到与 x 的 0 值相对应的所有 y 值的计数。让不同 y 值的计数为 yCount。我们可以通过运行一个循环并比较 yCount*yCount 和 n 来找到 yCount
在我们有了初始的 yCount 之后，我们可以逐个增加 x 的值，并通过减少 yCount 来找到 y count 的下一个值。

## C++

```
// An efficient C program to find different (x, y) pairs that
// satisfy x*x + y*y < n.
#include <iostream>
using namespace std;

// This function counts number of pairs (x, y) that satisfy
// the inequality x*x + y*y < n.
int countSolutions(int n)
{
   int x = 0, yCount, res = 0;

   // Find the count of different y values for x = 0.
   for (yCount = 0; yCount*yCount < n; yCount++) ;

   // One by one increase value of x, and find yCount for
   // current x.  If yCount becomes 0, then we have reached
   // maximum possible value of x.
   while (yCount != 0)
   {
       // Add yCount (count of different possible values of y
       // for current x) to result
       res  +=  yCount;

       // Increment x
       x++;

       // Update yCount for current x. Keep reducing yCount while
       // the inequality is not satisfied.
       while (yCount != 0 && (x*x + (yCount-1)*(yCount-1) >= n))
         yCount--;
   }

   return res;
}

// Driver program to test above function
int main()
{
    cout << "Total Number of distinct Non-Negative pairs is "
         << countSolutions(6) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to
// find different (x, y) pairs
// that satisfy x*x + y*y < n.
import java.io.*;

class GFG
{
    // This function counts number
    //of pairs (x, y) that satisfy
    // the inequality x*x + y*y < n.
    static int countSolutions(int n)
    {
        int x = 0, yCount, res = 0;

        // Find the count of different
        // y values for x = 0.
        for (yCount = 0; yCount * yCount < n; yCount++) ;

        // One by one increase value of x,
        // and find yCount forcurrent x. If
        // yCount becomes 0, then we have reached
        // maximum possible value of x.
        while (yCount != 0)
        {
            // Add yCount (count of different possible
            // values of y for current x) to result
            res += yCount;

            // Increment x
            x++;

            // Update yCount for current x. Keep reducing
            // yCount while the inequality is not satisfied.
            while (yCount != 0 && (x * x + (yCount - 1)
                                  * (yCount - 1) >= n))
            yCount--;

        }
        return res;

    }

    // Driver program
    public static void main(String args[])
    {
        System.out.println ( "Total Number of distinct Non-Negative pairs is "
                             +countSolutions(6)) ;

    }
}

// This article is contributed by vt_m.
```

## 蟒蛇 3

```
# An efficient python program to
# find different (x, y) pairs
# that satisfy x*x + y*y < n.

# This function counts number of
# pairs (x, y) that satisfy the
# inequality x*x + y*y < n.
def countSolutions(n):

    x = 0
    res = 0
    yCount = 0

    # Find the count of different
    # y values for x = 0.
    while(yCount * yCount < n):
        yCount = yCount + 1

    # One by one increase value of
    # x, and find yCount for current
    # x. If yCount becomes 0, then
    # we have reached maximum
    # possible value of x.
    while (yCount != 0):
        # Add yCount (count of
        # different possible values
        # of y for current x) to
        # result
        res = res + yCount

        # Increment x
        x = x + 1

        # Update yCount for current
        # x. Keep reducing yCount
        # while the inequality is
        # not satisfied.
        while (yCount != 0 and (x * x
                     + (yCount - 1) *
                     (yCount - 1) >= n)):
            yCount = yCount - 1

    return res

# Driver program to test
# above function
print ("Total Number of distinct ",
           "Non-Negative pairs is "
               , countSolutions(6))

# This code is contributed by Sam007.
```

## C#

```
// An efficient C# program to
// find different (x, y) pairs
// that satisfy x*x + y*y < n.
using System;

class GFG {

    // This function counts number
    //of pairs (x, y) that satisfy
    // the inequality x*x + y*y < n.
    static int countSolutions(int n)
    {
        int x = 0, yCount, res = 0;

        // Find the count of different
        // y values for x = 0.
        for (yCount = 0; yCount * yCount < n;
                                   yCount++) ;

        // One by one increase value of x,
        // and find yCount forcurrent x. If
        // yCount becomes 0, then we have
        // reached maximum possible value
        // of x.
        while (yCount != 0)
        {

            // Add yCount (count of different
            // possible values of y for
            // current x) to result
            res += yCount;

            // Increment x
            x++;

            // Update yCount for current x.
            // Keep reducing yCount while the
            // inequality is not satisfied.
            while (yCount != 0 && (x * x +
                            (yCount - 1) *
                         (yCount - 1) >= n))
            yCount--;
        }

        return res;
    }

    // Driver program
    public static void Main()
    {
        Console.WriteLine( "Total Number of "
          + "distinct Non-Negative pairs is "
                       + countSolutions(6)) ;
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient C program to find different
// (x, y) pairs that satisfy x*x + y*y < n.

// This function counts number of pairs
// (x, y) that satisfy the inequality
// x*x + y*y < n.
function countSolutions( $n)
{
    $x = 0; $yCount; $res = 0;

    // Find the count of different y values
    // for x = 0.
    for ($yCount = 0; $yCount*$yCount < $n;
                               $yCount++) ;

    // One by one increase value of x, and
    // find yCount for current x. If yCount
    // becomes 0, then we have reached
    // maximum possible value of x.
    while ($yCount != 0)
    {
        // Add yCount (count of different
        // possible values of y
        // for current x) to result
        $res += $yCount;

        // Increment x
        $x++;

        // Update yCount for current x. Keep
        // reducing yCount while the
        // inequality is not satisfied.
        while ($yCount != 0 and ($x * $x +
           ($yCount-1) * ($yCount-1) >= $n))
            $yCount--;
    }

    return $res;
}

// Driver program to test above function
echo "Total Number of distinct Non-Negative",
        "pairs is ", countSolutions(6) ,"\n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // An efficient Javascript program to
    // find different (x, y) pairs
    // that satisfy x*x + y*y < n.

    // This function counts number
    //of pairs (x, y) that satisfy
    // the inequality x*x + y*y < n.
    function countSolutions(n)
    {
        let x = 0, yCount, res = 0;

        // Find the count of different
        // y values for x = 0.
        for (yCount = 0; yCount * yCount < n;
                                   yCount++) ;

        // One by one increase value of x,
        // and find yCount forcurrent x. If
        // yCount becomes 0, then we have
        // reached maximum possible value
        // of x.
        while (yCount != 0)
        {

            // Add yCount (count of different
            // possible values of y for
            // current x) to result
            res += yCount;

            // Increment x
            x++;

            // Update yCount for current x.
            // Keep reducing yCount while the
            // inequality is not satisfied.
            while (yCount != 0 && (x * x +
                            (yCount - 1) *
                         (yCount - 1) >= n))
            yCount--;
        }

        return res;
    }

    document.write( "Total Number of "
          + "distinct Non-Negative pairs is "
                       + countSolutions(6)) ;

</script>
```

**输出:**

```
Total Number of distinct Non-Negative pairs is 8
```

**以上解的时间复杂度**看起来比较多，但是如果我们仔细看的话，可以看出是 O(√n)。在内部循环的每一步中，yCount 的值都会递减 1。当 yCount 被计数为 x = 0 的 y 值时，yCount 值最多可以递减 O(√n)次。在外循环中，x 的值递增。x 的值最多也可以增加 O(√n)倍，因为最后一个 x 代表 yCount 等于 1。

**辅助空间:** O(1)
本文由**萨钦·古普塔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。