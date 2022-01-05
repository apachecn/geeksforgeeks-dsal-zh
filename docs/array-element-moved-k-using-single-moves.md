# 使用单次移动将数组元素移动 k

> 原文:[https://www . geesforgeks . org/array-element-moved-k-using-single-moves/](https://www.geeksforgeeks.org/array-element-moved-k-using-single-moves/)

给定一个 N 个整数的列表，其中包含 1-n 个混洗的数字和一个整数 k。N 个人排队打羽毛球。首先，队列中的前两个玩家玩一个游戏。然后输的人走到队伍的最后，赢的人和队伍的下一个人玩，以此类推。他们一直玩到有人连续赢了 k 场比赛。这个玩家成为赢家。

**示例:**

```
Input: arr[] = {2, 1, 3, 4, 5}
       k = 2  
Output: 5 
Explanation: 
2 plays with 1, 1 goes to end of queue.
2 plays with 3, 3 wins, 2 goes to end of queue.
3 plays with 4, so 3 goes to the end of the queue.
5 plays with everyone and wins as it is the 
largest of all elements.

Input: arr[] = {3, 1, 2} 
       k = 2
Output: 3
Explanation :  
3 plays with 1\. 3 wins. 1 goes to the end of the line. 
3 plays with 2\. 3 wins. 3 wins twice in a row.
```

一种**天真的方法**是运行两个嵌套的 for 循环，并检查每个元素，从 I 到 n 哪个更大是第一个循环，第二个是从 i+1 到 n，然后从 0 到 n-1，并计算连续的较小元素的数量，得到答案。
这将不够高效，因为它需要 **O(n*n)** 。

一种**有效的方法**是运行一个从 1 到 n 的循环，并跟踪到目前为止最好的(或最大的)元素以及比这个最大值小的元素的数量。如果当前最佳松动，将较大的值初始化为最佳，并将计数设为 1，因为获胜者已经赢了 1 次。如果在任何一步它赢了 k 次，你会得到你的答案。但是如果 k > = n-1，那么最大值将是唯一的答案，因为它的最大次数将是最大的。如果在迭代的时候你没有发现任何玩家赢了 k 次，那么列表中的最大数量将永远是我们的答案。

下面是上述方法的实现

## C++

```
// C++ program to find winner of game
#include <iostream>
using namespace std;

int winner(int a[], int n, int k)
{
    // if the number of steps is more then
    // n-1,
    if (k >= n - 1)
        return n;

    // initially the best is 0 and no of
    // wins is 0.
    int best = 0, times = 0;

    // traverse through all the numbers
    for (int i = 0; i < n; i++) {

        // if the value of array is more
        // then that of previous best
        if (a[i] > best) {

            // best is replaced by a[i]
            best = a[i];

            // if not the first index
            if (i)
                times = 1; // no of wins is 1 now
        }

        else
            times += 1; // if it wins

        // if any position has more then k wins
        // then return
        if (times >= k)
            return best;
    }

    // Maximum element will be winner because
    // we move smaller element at end and repeat
    // the process.
    return best;
}

// driver program to test the above function
int main()
{
    int a[] = { 2, 1, 3, 4, 5 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 2;
    cout << winner(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find winner of game
import java.io.*;

class GFG {

    static int winner(int a[], int n, int k)
    {
        // if the number of steps is more then
        // n-1,
        if (k >= n - 1)
            return n;

        // initially the best is 0 and no of
        // wins is 0.
        int best = 0, times = 0;

        // traverse through all the numbers
        for (int i = 0; i < n; i++) {

            // if the value of array is more
            // then that of previous best
            if (a[i] > best) {

                // best is replaced by a[i]
                best = a[i];

                // if not the first index
                if (i == 1)

                    // no of wins is 1 now
                    times = 1;
            }

            else

                // if it wins
                times += 1;

            // if any position has more then
            // k wins then return
            if (times >= k)
                return best;
        }

        // Maximum element will be winner
        // because we move smaller element
        // at end and repeat the process.
        return best;
    }

    // driver program to test the above function
    public static void main(String args[])
    {
        int a[] = { 2, 1, 3, 4, 5 };
        int n = a.length;
        int k = 2;

        System.out.println(winner(a, n, k));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 code to find
# winner of game

# function to find the winner
def winner( a, n, k):

    # if the number of steps is
    # more then n-1
    if k >= n - 1:
        return n

    # initially the best is 0
    # and no of wins is 0.
    best = 0
    times = 0

    # traverse through all the numbers
    for i in range(n):

        # if the value of array is more
        # then that of previous best
        if a[i] > best:

            # best is replaced by a[i]
            best = a[i]

            # if not the first index
            if i == True:

                # no of wins is 1 now
                times = 1
        else:
            times += 1 # if it wins

        # if any position has more
        # then k wins then return
        if times >= k:
            return best

    # Maximum element will be winner
    # because we move smaller element
    # at end and repeat the process.
    return best

# driver code
a = [ 2, 1, 3, 4, 5 ]
n = len(a)
k = 2
print(winner(a, n, k))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# program to find winner of game
using System;

class GFG {

    static int winner(int[] a, int n, int k)
    {

        // if the number of steps is more
        // then n-1,
        if (k >= n - 1)
            return n;

        // initially the best is 0 and no of
        // wins is 0.
        int best = 0, times = 0;

        // traverse through all the numbers
        for (int i = 0; i < n; i++) {

            // if the value of array is more
            // then that of previous best
            if (a[i] > best) {

                // best is replaced by a[i]
                best = a[i];

                // if not the first index
                if (i == 1)

                    // no of wins is 1 now
                    times = 1;
            }

            else

                // if it wins
                times += 1;

            // if any position has more
            // then k wins then return
            if (times >= k)
                return best;
        }

        // Maximum element will be winner
        // because we move smaller element
        // at end and repeat the process.
        return best;
    }

    // driver program to test the above
    // function
    public static void Main()
    {
        int[] a = { 2, 1, 3, 4, 5 };
        int n = a.Length;
        int k = 2;

        Console.WriteLine(winner(a, n, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find winner of game

function winner($a, $n, $k)
{
    // if the number of steps
    // is more then n-1,
    if ($k >= $n - 1)
        return $n;

    // initially the best is 0
    // and no. of wins is 0.
    $best = 0; $times = 0;

    // traverse through all the numbers
    for ($i = 0; $i < $n; $i++)
    {

        // if the value of array is more
        // then that of previous best
        if ($a[$i] > $best)
        {

            // best is replaced by a[i]
            $best = $a[$i];

            // if not the first index
            if ($i)

                // no of wins is 1 now
                $times = 1;
        }

        else

            // if it wins
            $times += 1;

        // if any position has more then
        // k wins then return
        if ($times >= $k)
            return $best;
    }

    // Maximum element will be winner
    // because we move smaller element
    // at end and repeat the process.
    return $best;
}

// Driver Code
$a = array( 2, 1, 3, 4, 5 );
$n = sizeof($a);
$k = 2;
echo(winner($a, $n, $k));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find winner of game

function winner(a, n, k)
{

    // If the number of steps is more then
    // n-1,
    if (k >= n - 1)
        return n;

    // Initially the best is 0 and no of
    // wins is 0.
    let best = 0, times = 0;

    // Traverse through all the numbers
    for(let i = 0; i < n; i++)
    {

        // If the value of array is more
        // then that of previous best
        if (a[i] > best)
        {

            // best is replaced by a[i]
            best = a[i];

            // If not the first index
            if (i)

                // No of wins is 1 now
                times = 1;
        }

        else

            // If it wins
            times += 1;

        // If any position has more
        // then k wins then return
        if (times >= k)
            return best;
    }

    // Maximum element will be winner because
    // we move smaller element at end and repeat
    // the process.
    return best;
}

// Driver code
let a = [ 2, 1, 3, 4, 5 ];
let n = a.length;
let k = 2;

document.write(winner(a, n, k));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
5
```

**时间复杂度** : O(n)