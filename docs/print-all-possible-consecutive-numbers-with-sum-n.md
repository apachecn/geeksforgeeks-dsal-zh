# 用和 N 打印所有可能的连续数字

> 原文:[https://www . geeksforgeeks . org/print-所有可能的连续数字-带 sum-n/](https://www.geeksforgeeks.org/print-all-possible-consecutive-numbers-with-sum-n/)

给定一个数字 n。任务是打印所有可能的连续数字，这些数字加起来就是 n

**示例:**

```
Input: N = 100
Output:
9 10 11 12 13 14 15 16 
18 19 20 21 22 

Input: N = 125
Output:
8 9 10 11 12 13 14 15 16 17 
23 24 25 26 27 
62 63 
```

一个重要的事实是，我们找不到 N/2 以上加起来等于 N 的连续数字，因为 N/2 + (N/2 + 1)将大于 N。因此，我们从 start = 1 开始，直到 end = N/2，并检查每个连续序列是否加起来等于 N。如果是，那么我们打印该序列，并通过增加起点开始寻找下一个序列。

## C++

```
// C++ program to print consecutive sequences
// that add to a given value
#include<bits/stdc++.h>
using namespace std;

void findConsecutive(int N)
{

    // Note that we don't ever have to sum
    // numbers > ceil(N/2)
    int start = 1, end = (N+1)/2;

    // Repeat the loop from bottom to half
    while (start < end)
    {

        // Check if there exist any sequence
        // from bottom to half which adds up to N
        int sum = 0;
        for (int i = start; i <= end; i++)
        {
            sum = sum + i;

            // If sum = N, this means consecutive
            // sequence exists
            if (sum == N)
            {

                // found consecutive numbers! print them
                for (int j = start; j <= i; j++)
                    cout <<" "<< j;

                cout <<"\n";
                break;
            }

            // if sum increases N then it can not exist
            // in the consecutive sequence starting from
            // bottom
            if (sum > N)
                break;
        }
        sum = 0;
        start++;
    }
}

// Driver code
int main(void)
{
    int N = 125;
    findConsecutive(N);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C++ program to print consecutive sequences
// that add to a given value
#include<stdio.h>

void findConsecutive(int N)
{
    // Note that we don't ever have to sum
    // numbers > ceil(N/2)
    int start = 1, end = (N+1)/2;

    // Repeat the loop from bottom to half
    while (start < end)
    {
        // Check if there exist any sequence
        // from bottom to half which adds up to N
        int sum = 0;
        for (int i = start; i <= end; i++)
        {
            sum = sum + i;

            // If sum = N, this means consecutive
            // sequence exists
            if (sum == N)
            {
                // found consecutive numbers! print them
                for (int j = start; j <= i; j++)
                    printf("%d ", j);

                printf("\n");
                break;
            }

            // if sum increases N then it can not exist
            // in the consecutive sequence starting from
            // bottom
            if (sum > N)
                break;
        }
        sum = 0;
        start++;
    }
}

// Driver code
int main(void)
{
    int N = 125;
    findConsecutive(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// consecutive sequences
// that add to a given value
import java.io.*;

class GFG
{
static void findConsecutive(int N)
{
    // Note that we don't
    // ever have to sum
    // numbers > ceil(N/2)
    int start = 1;
    int end = (N + 1) / 2;

    // Repeat the loop
    // from bottom to half
    while (start < end)
    {
        // Check if there exist
        // any sequence from
        // bottom to half which
        // adds up to N
        int sum = 0;
        for (int i = start; i <= end; i++)
        {
            sum = sum + i;

            // If sum = N, this means
            // consecutive sequence exists
            if (sum == N)
            {
                // found consecutive
                // numbers! print them
                for (int j = start; j <= i; j++)

                    System.out.print(j + " ");
                    System.out.println();
                break;
            }

            // if sum increases N then
            // it can not exist in the
            // consecutive sequence
            // starting from bottom
            if (sum > N)
                break;
        }
        sum = 0;
        start++;
    }
}

// Driver code
public static void main (String[] args)
{
    int N = 125;
    findConsecutive(N);
}
}

// This code is contributed by m_kit
```

## 蟒蛇 3

```
# Python3 program to print consecutive
# sequences that add to a given value
def findConsecutive(N):

    # Note that we don't ever have to
    # Sum numbers > ceil(N/2)
    start = 1
    end = (N + 1) // 2

    # Repeat the loop from bottom to half
    while (start < end):

        # Check if there exist any sequence
        # from bottom to half which adds up to N
        Sum = 0
        for i in range(start, end + 1):

            Sum = Sum + i

            # If Sum = N, this means consecutive
            # sequence exists
            if (Sum == N):

                # found consecutive numbers! prthem
                for j in range(start, i + 1):
                    print(j, end = " ")

                print()
                break

            # if Sum increases N then it can not
            # exist in the consecutive sequence
            # starting from bottom
            if (Sum > N):
                break

        Sum = 0
        start += 1

# Driver code
N = 125
findConsecutive(N)

# This code is contributed by Mohit kumar 29
```

## C#

```
// C# program to print
// consecutive sequences
// that add to a given value
using System;

class GFG
{
static void findConsecutive(int N)
{
    // Note that we don't
    // ever have to sum
    // numbers > ceil(N/2)
    int start = 1;
    int end = (N + 1) / 2;

    // Repeat the loop
    // from bottom to half
    while (start < end)
    {
        // Check if there exist
        // any sequence from
        // bottom to half which
        // adds up to N
        int sum = 0;
        for (int i = start; i <= end; i++)
        {
            sum = sum + i;

            // If sum = N, this means
            // consecutive sequence exists
            if (sum == N)
            {
                // found consecutive
                // numbers! print them
                for (int j = start; j <= i; j++)

                    Console.Write(j + " ");
                    Console.WriteLine();
                break;
            }

            // if sum increases N then
            // it can not exist in the
            // consecutive sequence
            // starting from bottom
            if (sum > N)
                break;
        }
        sum = 0;
        start++;
    }
}

// Driver code
static public void Main ()
{
    int N = 125;
    findConsecutive(N);
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print consecutive
// sequences that add to a given value

function findConsecutive($N)
{
    // Note that we don't ever have
    // to sum numbers > ceil(N/2)
    $start = 1;
    $end = ($N + 1) / 2;

    // Repeat the loop from
    // bottom to half
    while ($start < $end)
    {
        // Check if there exist any
        // sequence from bottom to
        // half which adds up to N
        $sum = 0;
        for ($i = $start; $i <= $end; $i++)
        {
            $sum = $sum + $i;

            // If sum = N, this means
            // consecutive sequence exists
            if ($sum == $N)
            {
                // found consecutive
                // numbers! print them
                for ($j = $start; $j <= $i; $j++)
                    echo $j ," ";

                echo "\n";
                break;
            }

            // if sum increases N then it
            // can not exist in the consecutive
            // sequence starting from bottom
            if ($sum > $N)
                break;
        }
        $sum = 0;
        $start++;
    }
}

// Driver code
$N = 125;
findConsecutive($N);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to print consecutive sequences
// that add to a given value

function findConsecutive( N)
{
    // Note that we don't ever have to sum
    // numbers > ceil(N/2)
    let start = 1, end = Math.trunc((N+1)/2);

    // Repeat the loop from bottom to half
    while (start < end)
    {
        // Check if there exist any sequence
        // from bottom to half which adds up to N
        let sum = 0;
        for (let i = start; i <= end; i++)
        {
            sum = sum + i;

            // If sum = N, this means consecutive
            // sequence exists
            if (sum == N)
            {
                // found consecutive numbers! print them
                for (let j = start; j <= i; j++)
                    document.write(j+" ");

                document.write("<br/>");
                break;
            }

            // if sum increases N then it can not exist
            // in the consecutive sequence starting from
            // bottom
            if (sum > N)
                break;
        }
        sum = 0;
        start++;
    }
}

    // Driver program

    let N = 125;
    findConsecutive(N);

</script>
```

**输出:**

```
8 9 10 11 12 13 14 15 16 17 
23 24 25 26 27 
62 63 
```

**优化解:**
在上面的解中，我们从头到尾一直在重新计算和，这导致了 O(N^2)最坏情况下的时间复杂度。这可以通过使用预先计算的总和数组来避免，或者更好的方法是——只需跟踪到目前为止的总和，并根据它与所需总和的比较情况来调整它。
下面代码的时间复杂度为 O(N)。

## C++

```
// Optimized C++ program to find sequences of all consecutive
// numbers with sum equal to N
#include <bits/stdc++.h>
using namespace std;

void printSums(int N)
{
    int start = 1, end = 1;
    int sum = 1;

    while (start <= N/2)
    {
        if (sum < N)
        {
            end += 1;
            sum += end;
        }
        else if (sum > N)
        {
            sum -= start;
            start += 1;
        }
        else if (sum == N)
        {
            for (int i = start; i <= end; ++i)
                cout <<" "<< i;

            cout <<"\n";
            sum -= start;
            start += 1;
        }
    }
}

// Driver Code
int main()
{
    printSums(125);
    return 0;
}

// this code is contributrd by shivanisinghss2110
```

## C

```
// Optimized C program to find sequences of all consecutive
// numbers with sum equal to N
#include <stdio.h>

void printSums(int N)
{
    int start = 1, end = 1;
    int sum = 1;

    while (start <= N/2)
    {
        if (sum < N)
        {
            end += 1;
            sum += end;
        }
        else if (sum > N)
        {
            sum -= start;
            start += 1;
        }
        else if (sum == N)
        {
            for (int i = start; i <= end; ++i)
                printf("%d ", i);

            printf("\n");
            sum -= start;
            start += 1;
        }
    }
}

// Driver Code
int main()
{
    printSums(125);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Optimized Java program to find
// sequences of all consecutive
// numbers with sum equal to N
import java.io.*;

class GFG {

    static void printSums(int N)
    {
        int start = 1, end = 1;
        int sum = 1;

        while (start <= N/2)
        {
            if (sum < N)
            {
                end += 1;
                sum += end;
            }
            else if (sum > N)
            {
                sum -= start;
                start += 1;
            }
            else if (sum == N)
            {
                for (int i = start;
                         i <= end; ++i)

                    System.out.print(i
                                + " ");

                System.out.println();
                sum -= start;
                start += 1;
            }
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
            printSums(125);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Optimized Python3 program to find sequences of all consecutive
# numbers with sum equal to N
def findConsecutive(N):

    start = 1
    end = 1
    sum = 1

    while start <= N/2:

        if sum < N:
            end += 1
            sum += end

        if sum > N:
            sum -= start
            start += 1

        if sum == N:

            for i in range(start, end + 1):
                print(i, end=' ')
            print( )
            sum -= start
            start += 1

# Driver code
N = 125
findConsecutive(N)

# This code is contributed by Sanskriti Agrawal
```

## C#

```
// Optimized C# program to find
// sequences of all consecutive
// numbers with sum equal to N
using System;

class GFG {

    static void printSums(int N)
    {
        int start = 1, end = 1;
        int sum = 1;

        while (start <= N/2)
        {
            if (sum < N)
            {
                end += 1;
                sum += end;
            }
            else if (sum > N)
            {
                sum -= start;
                start += 1;
            }
            else if (sum == N)
            {
                for (int i = start;
                        i <= end; ++i)

                    Console.Write(i
                                + " ");

                Console.WriteLine();
                sum -= start;
                start += 1;
            }
        }
    }

    // Driver Code
    public static void Main ()
    {
            printSums(125);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Optimized PHP program to find
// sequences of all consecutive
// numbers with sum equal to N

function printSums($N)
{
    $start = 1; $end = 1;
    $sum = 1;

    while ($start <= $N / 2)
    {
        if ($sum < $N)
        {
            $end += 1;
            $sum += $end;
        }
        else if ($sum > $N)
        {
            $sum -= $start;
            $start += 1;
        }
        else if ($sum == $N)
        {
            for ($i = $start; $i <= $end; ++$i)
                echo $i," ";
                echo "\n";
            $sum -= $start;
            $start += 1;
        }
    }
}

// Driver Code
    printSums(125);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// sequences of all consecutive
// numbers with sum equal to N
function printSums(N)
{
    let start = 1, end = 1;
    let sum = 1;

    while (start <= N / 2)
    {
        if (sum < N)
        {
            end += 1;
            sum += end;
        }
        else if (sum > N)
        {
            sum -= start;
            start += 1;
        }
        else if (sum == N)
        {
            for(let i = start;
                    i <= end; ++i)
                document.write(i + " ");

            document.write("<br/>");
            sum -= start;
            start += 1;
        }
    }
}

// Driver code   
printSums(125);

// This code is contributed by splevel62  

</script>
```

**输出:**

```
8 9 10 11 12 13 14 15 16 17 
23 24 25 26 27 
62 63 
```

**参考:**T2[https://www.careercup.com/page?PID = Microsoft-面试-提问& n=2](https://www.careercup.com/page?pid=microsoft-interview-questions&n=2)
本文由**nitesh Kumar**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。