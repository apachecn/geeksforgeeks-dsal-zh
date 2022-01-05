# 移出迷宫的可能性

> 原文:[https://www.geeksforgeeks.org/possibility-moving-maze/](https://www.geeksforgeeks.org/possibility-moving-maze/)

给定迷宫中的 n 个整数，指示从该位置开始的移动次数，以及带有“>”和“的字符串，打印它是停留在数组内部还是移出数组。

**示例:**

```
Input : 3 
        2 1 1 
        > > <       
Output: It stays inside forever
Explanation: 
It moves towards right by a position of 2, 
hence is at the last index, then it moves 
to the left by 1, and then it again moves 
to the right by 1\. Hence it doesn't go
out.

Input: 2
       1 2 
       > <        
Output: comes out 
Explanation: 
Starts at 0th index, moves right by 1 
position, and then moves left by 2 to 
come out 
```

上述问题的处理方法如下:
我们从第 0 个指标开始移动，直到超过 n 或减少 0。如果我们两次到达同一个位置，那么我们就处于一个无限循环中，永远无法移出。
*使用标记数组标记已访问的位置
*从第 0 个索引开始，检查移动和移动到该位置的标志，将该位置标记为已访问的
*如果已访问，我们将永远无法移出，因此中断
*检查中断循环的原因，并打印所需结果。
//下图是上述方法的 python 实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java Possibility of moving out of maze
import java.io.*;

class GFG
{
    // Function to check whether it
    // will stay inside or come out
    static void checkingPossibility( int a[], int n, String s)
    {
           // marks all the positions that is visited
        int mark[] = new int[a[0] * n] ;

            // Initial starting point
            int start = 0;

            // initial assumption is it comes out
            int possible = 1;

            //runs till it is inside or comes out
            while( start >= 0 && start < n)
            {

                //if the movement is towards left
                //then we move left. The start variable
                // and mark that position as visited
                // if not visited previously. Else we
                // break out
                if (s == "<")
                {

                    if (mark[start] == 0)
                    {
                        mark[start] = 1;
                        start -= a[start] ;
                    }

                    // It will be inside forever
                    else{
                        possible = 0;
                        break;}
                }

                // If the movement is towards right, then
                // we move right. The start variable and
                // mark that position as visited if not
                // visited previously else we break out
                else
                {
                    if (mark[start] == 0)
                    {
                        mark[start] = 1;
                        start += a[start] ;
                    }

                    // it will be inside forever
                    else
                    {
                        possible = 0;
                        break;
                    }
                }
            }

            if (possible == 0)
                System.out.print( "it stays inside forever");
            else
            System.out.print ("comes out");
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 2;
        String s = "><";
        int a[] = {1, 2};
        checkingPossibility(a, n, s);

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Function to check whether it will stay inside
# or come out
def checkingPossibility(a, n, s):

    # marks all the positions that is visited
    mark = [0] * n 

    # Initial starting point
    start = 0

    # initial assumption is it comes out
    possible = 1

    # runs till it is inside or comes out
    while start >= 0 and start < n:

        # if the movement is towards left
        # then we move left. The start variable
        # and mark that position as visited
        # if not visited previously. Else we
        # break out
        if s[start] == "<":

            if mark[start] == 0:
                mark[start] = 1
                start -= a[start]

            # It will be inside forever
            else:
                possible = 0
                break

        # If the movement is towards right, then
        # we move right. The start variable and
        # mark that position as visited if not
        # visited previously else we break out  
        else:
            if mark[start] == 0:
                mark[start] = 1
                start += a[start]

            # it will be inside forever
            else:
                possible = 0
                break

    if possible == 0:
        print "it stays inside forever"
    else:
        print "comes out"

# Driver code
n = 2
s = "><"
a = [1, 2]
checkingPossibility(a, n, s)
```

## C#

```
// C# Possibility of moving out of maze
using System;

class GFG {

    // Function to check whether it
    // will stay inside or come out
    static void checkingPossibility( int []a,
                              int n, String s)
    {

        // marks all the positions that
        // is visited
        int []mark = new int[a[0] * n] ;

            // Initial starting point
            int start = 0;

            // initial assumption is it
            // comes out
            int possible = 1;

            //runs till it is inside or
            // comes out
            while( start >= 0 && start < n)
            {

                //if the movement is towards
                // left then we move left.
                // The start variable and
                // mark that position as
                // visited if not visited
                // previously. Else we
                // break out
                if (s == "<")
                {

                    if (mark[start] == 0)
                    {
                        mark[start] = 1;
                        start -= a[start] ;
                    }

                    // It will be inside forever
                    else
                    {
                        possible = 0;
                        break;
                    }
                }

                // If the movement is towards
                // right, then we move right.
                // The start variable and mark
                // that position as visited if
                // not visited previously else
                // we break out
                else
                {
                    if (mark[start] == 0)
                    {
                        mark[start] = 1;
                        start += a[start] ;
                    }

                    // it will be inside forever
                    else
                    {
                        possible = 0;
                        break;
                    }
                }
            }

            if (possible == 0)
                Console.Write( "it stays "
                          + "inside forever");
            else
                Console.Write("comes out");
    }

    // Driver code
    public static void Main ()
    {

        int n = 2;
        String s = "><";
        int []a = {1, 2};

        checkingPossibility(a, n, s);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
    // Javascript Possibility of moving out of maze

    // Function to check whether it
    // will stay inside or come out
    function checkingPossibility(a, n, s)
    {

        // marks all the positions that
        // is visited
        let mark = new Array(a[0] * n);
        mark.fill(0);

        // Initial starting point
        let start = 0;

        // initial assumption is it
        // comes out
        let possible = 1;

        //runs till it is inside or
        // comes out
        while(start >= 0 && start < n)
        {

          //if the movement is towards
          // left then we move left.
          // The start variable and
          // mark that position as
          // visited if not visited
          // previously. Else we
          // break out
          if (s == "<")
          {

            if (mark[start] == 0)
            {
              mark[start] = 1;
              start -= a[start] ;
            }

            // It will be inside forever
            else
            {
              possible = 0;
              break;
            }
          }

          // If the movement is towards
          // right, then we move right.
          // The start variable and mark
          // that position as visited if
          // not visited previously else
          // we break out
          else
          {
            if (mark[start] == 0)
            {
              mark[start] = 1;
              start += a[start] ;
            }

            // it will be inside forever
            else
            {
              possible = 0;
              break;
            }
          }
        }

        if (possible == 0)
          document.write( "it stays " + "inside forever");
        else
          document.write("comes out");
    }

    let n = 2;
    let s = "><";
    let a = [1, 2];

    checkingPossibility(a, n, s);

</script>
```

**输出:**

```
comes out
```

**时间复杂度:** O(n)

本文由[](https://www.facebook.com/profile.php?id=100008562932368)**twickl Bajaj 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。**