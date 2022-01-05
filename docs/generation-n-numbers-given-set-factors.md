# 用给定的一组因子生成 n 个数字

> 原文:[https://www . geesforgeks . org/generation-n-numbers-given-set-factors/](https://www.geeksforgeeks.org/generation-n-numbers-given-set-factors/)

给定一个由 k 个数字组成的数组**因子[]** ，任务是打印前 n 个数字(按升序排列)，其因子来自给定的数组。

**示例:**

```
Input  : factor[] = {2, 3, 4, 7} 
         n = 8
Output : 2 3 4 6 7 8 9 10

Input  :  factor[] = {3, 5, 7}
          n = 10
Output :  3 5 6 7 9 10 12 14 15 18
```

这个问题主要是[丑数问题](https://www.geeksforgeeks.org/ugly-numbers/)的延伸。我们创建一个辅助数组**下一个[]** ，其大小与因子[]相同，以跟踪因子的下一个倍数。在每次迭代中，我们从下一个输出最小元素，然后用相应的因子递增它。如果最小值等于前一个输出值，则递增它(以避免重复)。否则我们打印最小值。

## C++

```
// C++ program to generate n numbers with
// given factors
#include<bits/stdc++.h>
using namespace std;

// Generate n numbers with factors in factor[]
void generateNumbers(int factor[], int n, int k)
{
    // array of k to store next multiples of
    // given factors
    int next[k] = {0};

    // Prints n numbers 
    int output = 0;  // Next number to print as output
    for (int i=0; i<n; )
    {
        // Find the next smallest multiple
        int toincrement = 0;
        for (int j=0; j<k; j++)
            if (next[j] < next[toincrement])
                toincrement = j;

        // Printing minimum in each iteration
        // print the value if output is not equal to
        // current value(to avoid the duplicates)
        if (output != next[toincrement])
        {
            output = next[toincrement];
            printf("%d ",  next[toincrement]);
            i++;
        }

        // incrementing the current value by the
        // respective factor
        next[toincrement] += factor[toincrement];
    }
}

// Driver code
int main()
{
    int factor[] = {3, 5, 7};
    int n = 10;
    int k = sizeof(factor)/sizeof(factor[0]);
    generateNumbers(factor, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate
// n numbers with given factors
import java.io.*;

class GFG
{

// Generate n numbers with
// factors in factor[]
static void generateNumbers(int factor[],
                            int n, int k)
{
    // array of k to store
    // next multiples of
    // given factors
    int next[] = new int[k];

    // Prints n numbers
    int output = 0; // Next number to
                    // print as output
    for (int i = 0; i < n;)
    {
        // Find the next
        // smallest multiple
        int toincrement = 0;
        for (int j = 0; j < k; j++)
            if (next[j] < next[toincrement])
                toincrement = j;

        // Printing minimum in
        // each iteration print
        // the value if output
        // is not equal to current
        // value(to avoid the
        // duplicates)
        if (output != next[toincrement])
        {
            output = next[toincrement];
            System.out.print(
                   next[toincrement] + " ");
            i++;
        }

        // incrementing the
        // current value by the
        // respective factor
        next[toincrement] +=
               factor[toincrement];
    }
}

// Driver code
public static void main (String[] args)
{
    int factor[] = {3, 5, 7};
    int n = 10;
    int k = factor.length;
    generateNumbers(factor, n, k);
}
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python3 program to generate n
# numbers with given factors

# Generate n numbers with
# factors in factor[]
def generateNumbers(factor, n, k):

    # array of k to store next
    # multiples of given factors
    next = [0] * k;

    # Prints n numbers
    output = 0; # Next number to
                # print as output
    i = 0;
    while(i < n):

        # Find the next smallest
        # multiple
        toincrement = 0;
        for j in range(k):
            if(next[j] < next[toincrement]):
                toincrement = j;

        # Printing minimum in each
        # iteration print the value
        # if output is not equal to
        # current value(to avoid the
        # duplicates)
        if(output != next[toincrement]):
            output = next[toincrement];
            print(next[toincrement], end = " ");
            i += 1;

        # incrementing the current
        # value by the respective factor
        next[toincrement] += factor[toincrement];

# Driver code
factor = [3, 5, 7];
n = 10;
k = len(factor);
generateNumbers(factor, n, k);

# This code is contributed by mits
```

## C#

```
// C# program to generate
// n numbers with given factors
using System;

class GFG
{

// Generate n numbers with
// factors in factor[]
static void generateNumbers(int []factor,
                            int n, int k)
{
    // array of k to store
    // next multiples of
    // given factors
    int []next = new int[k];

    // Prints n numbers
    int output = 0; // Next number to
                    // print as output
    for (int i = 0; i < n;)
    {
        // Find the next
        // smallest multiple
        int toincrement = 0;
        for (int j = 0; j < k; j++)
            if (next[j] < next[toincrement])
                toincrement = j;

        // Printing minimum in
        // each iteration print
        // the value if output
        // is not equal to current
        // value(to avoid the
        // duplicates)
        if (output != next[toincrement])
        {
            output = next[toincrement];
            Console.Write(
                next[toincrement] + " ");
            i++;
        }

        // incrementing the
        // current value by the
        // respective factor
        next[toincrement] +=
            factor[toincrement];
    }
}

// Driver code
static public void Main ()
{
    int []factor = {3, 5, 7};
    int n = 10;
    int k = factor.Length;
    generateNumbers(factor, n, k);
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate n numbers
// with given factors

// Generate n numbers with factors
// in factor[]
function generateNumbers($factor, $n, $k)
{
    // array of k to store next
    // multiples of given factors
    $next = array_fill(0, $k, 0);

    // Prints n numbers
    $output = 0; // Next number to print
                 // as output
    for ($i = 0; $i < $n; )
    {
        // Find the next smallest multiple
        $toincrement = 0;
        for ($j = 0; $j < $k; $j++)
            if ($next[$j] < $next[$toincrement])
                $toincrement = $j;

        // Printing minimum in each iteration
        // print the value if output is not
        // equal to current value(to avoid
        // the duplicates)
        if ($output != $next[$toincrement])
        {
            $output = $next[$toincrement];
            echo $next[$toincrement] . " ";
            $i++;
        }

        // incrementing the current value
        // by the respective factor
        $next[$toincrement] += $factor[$toincrement];
    }
}

// Driver code
$factor = array(3, 5, 7);
$n = 10;
$k = count($factor);
generateNumbers($factor, $n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to generate
// n numbers with given factors

// Generate n numbers with
// factors in factor[]
function generateNumbers(factor, n, k)
{

    // Array of k to store
    // next multiples of
    // given factors
    let next = new Array(k);
    next.fill(0);

    // Prints n numbers
    let output = 0; // Next number to
                    // print as output

    for(let i = 0; i < n;)
    {

        // Find the next
        // smallest multiple
        let toincrement = 0;
        for(let j = 0; j < k; j++)
            if (next[j] < next[toincrement])
                toincrement = j;

        // Printing minimum in
        // each iteration print
        // the value if output
        // is not equal to current
        // value(to avoid the
        // duplicates)
        if (output != next[toincrement])
        {
            output = next[toincrement];
            document.write(next[toincrement] + " ");
            i++;
        }

        // Incrementing the
        // current value by the
        // respective factor
        next[toincrement] += factor[toincrement];
    }
}

// Driver code
let factor = [ 3, 5, 7 ];
let n = 10;
let k = factor.length;

generateNumbers(factor, n, k);

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
3 5 6 7 9 10 12 14 15 18 
```

**时间复杂度–**O(n * k)
T3】辅助空间–O(k)

本文由**尼泰什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。