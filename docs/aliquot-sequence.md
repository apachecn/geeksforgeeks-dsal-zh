# 等分序列

> 原文:[https://www.geeksforgeeks.org/aliquot-sequence/](https://www.geeksforgeeks.org/aliquot-sequence/)

给定数字 n，任务是打印其等分序列。一个数的等分序列从它自己开始，序列的剩余项是前一项的适当除数的和。例如，10 的等分序列是 10、8、7、1、0。序列可能会重复。例如，对于 6，我们有一个所有 6 的无穷序列。在这种情况下，我们打印重复的数字并停止。

示例:

```
Input:  n = 10
Output: 10 8 7 1 0
Sum of proper divisors of 10 is  5 + 2 + 1 = 8.
Sum of proper divisors of 8 is 4 + 2 + 1 = 7.
Sum of proper divisors of 7 is 1
Sum of proper divisors of 1 is 0
Note that there is no proper divisor of 1.

Input  : n = 6
Output : 6 
         Repeats with 6

Input : n = 12
Output : 12 16 15 9 4 3 1 0 

```

**要点:**

*   长度为 1 的重复等分序列的数字称为[完全数](https://en.wikipedia.org/wiki/Perfect_number)。例如 6，它的适当除数之和是 6。
*   长度为 2 的重复等分序列的数字称为[友好数字](https://en.wikipedia.org/wiki/Amicable_numbers)。例如，220 是友好号码。
*   长度为 3 的重复等分序列的数称为[合群数](https://en.wikipedia.org/wiki/Sociable_number)。
*   据推测，每个等分序列以下列方式之一结束
    *   质数依次以 1 和 0 结束。
    *   完美的数字
    *   一组友好或友好的数字。

解决方法主要在于计算前一项的所有适当除数之和。

*   如果我们仔细观察，数 n 的除数成对出现。例如，如果 n = 100，那么所有的除数对都是:(1，100)，(2，50)，(4，25)，(5，20)，(10，10)
*   利用这个事实可以有效地计算除数。在检查除数时，我们必须小心是否有两个相等的除数，如(10，10)的情况。
*   在这种情况下，我们将只取其中的一个来计算总和。这个和将包含所有可能除数的和，所以我们必须从所有除数的和中减去数 n，才能得到适当除数的和。

我们可以通过首先打印数字 n，然后使用适当除数的和计算下一个项来生成序列。当我们计算下一个术语时，我们检查我们是否已经看到了这个术语。如果这个术语再次出现，我们有重复序列。我们打印相同的并打破循环。

## C++

```
// C++ implementation of Optimized approach
// to generate Aliquot Sequence
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of all proper divisors
int getSum(int n)
{
    int sum = 0;  // 1 is a proper divisor

    // Note that this loop runs till square root
    // of n
    for (int i=1; i<=sqrt(n); i++)
    {
        if (n%i==0)
        {
            // If divisors are equal, take only one
            // of them
            if (n/i == i)
                sum = sum + i;

            else // Otherwise take both
            {
                sum = sum + i;
                sum = sum + (n / i);
            }
        }
    }

    // calculate sum of all proper divisors only
    return sum - n;
}

// Function to print Aliquot Sequence for an input n.
void printAliquot(int n)
{
    // Print the first term
    printf("%d ", n);
    unordered_set<int>  s;
    s.insert(n);

    int next = 0;
    while (n > 0)
    {
        // Calculate next term from previous term
        n = getSum(n);

        if (s.find(n) != s.end())
        {
            cout << "\nRepeats with " << n;
            break;
        }

        // Print next term
        cout << n << " ";
        s.insert(n);
    }
}

/* Driver program to test above function */
int main()
{
    printAliquot(12);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of Optimized approach 
// to generate Aliquot Sequence 
import java.util.*;

class GFG 
{

    // Function to calculate sum 
    // of all proper divisors 
    static int getSum(int n) 
    {
        int sum = 0; // 1 is a proper divisor 

        // Note that this loop runs till  
        // square root of n 
        for (int i = 1; i <= Math.sqrt(n); i++)
        {
            if (n % i == 0) 
            {
                // If divisors are equal, take only one 
                // of them 
                if (n / i == i) 
                {
                    sum = sum + i;
                }
                else // Otherwise take both 
                {
                    sum = sum + i;
                    sum = sum + (n / i);
                }
            }
        }

        // calculate sum of all proper divisors only 
        return sum - n;
    }

    // Function to print Aliquot 
    // Sequence for an input n. 
    static void printAliquot(int n) 
    {

        // Print the first term 
        System.out.printf("%d ", n);

        TreeSet<Integer> s = new TreeSet<>();
        s.add(n);

        int next = 0;
        while (n > 0) 
        {
            // Calculate next term from previous term 
            n = getSum(n);

            if (s.contains(n) && n != s.last()) 
            {
                System.out.print("\nRepeats with " + n);
                break;
            }

            // Print next term 
            System.out.print(n + " ");
            s.add(n);
        }
    }

    /* Driver code */
    public static void main(String[] args) 
    {
        printAliquot(12);
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python implementation of Optimized approach
# to generate Aliquot Sequence

from math import sqrt

# Function to calculate sum of all proper divisors
def getSum(n):
    summ = 0 # 1 is a proper divisor

    # Note that this loop runs till square root
    # of n
    for i in range(1, int(sqrt(n)) + 1):
        if n % i == 0:

            # If divisors are equal, take only one
            # of them
            if n // i == i:
                summ += i

            # Otherwise take both
            else:
                summ += i
                summ += n // i

    # calculate sum of all proper divisors only
    return summ - n

# Function to print Aliquot Sequence for an input n.
def printAliquot(n):

    # Print the first term
    print(n, end=" ")
    s = set()
    s.add(n)

    nextt = 0
    while n > 0:

        # Calculate next term from previous term
        n = getSum(n)

        if n in s:
            print("Repeats with", n)
            break

        # Print next term
        print(n, end=" ")
        s.add(n)

# Driver Code
if __name__ == "__main__":
    printAliquot(12)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of Optimized approach 
// to generate Aliquot Sequence 
using System;
using System.Collections.Generic;

class GFG 
{ 

    // Function to calculate sum 
    // of all proper divisors 
    static int getSum(int n) 
    { 
        int sum = 0; // 1 is a proper divisor 

        // Note that this loop runs till 
        // square root of n 
        for (int i = 1; i <= Math.Sqrt(n); i++) 
        { 
            if (n % i == 0) 
            { 
                // If divisors are equal,  
                // take only one of them 
                if (n / i == i) 
                { 
                    sum = sum + i; 
                } 
                else // Otherwise take both 
                { 
                    sum = sum + i; 
                    sum = sum + (n / i); 
                } 
            } 
        } 

        // calculate sum of all proper divisors only 
        return sum - n; 
    } 

    // Function to print Aliquot 
    // Sequence for an input n. 
    static void printAliquot(int n) 
    { 

        // Print the first term 
        Console.Write(n+" "); 

        HashSet<int> s = new HashSet<int>(); 
        s.Add(n); 

        while (n > 0) 
        { 

            // Calculate next term from previous term 
            n = getSum(n); 

            if (s.Contains(n)) 
            { 
                Console.Write("\nRepeats with " + n); 
                break; 
            } 

            // Print next term 
            Console.Write(n + " "); 
            s.Add(n); 
        } 
    } 

    /* Driver code */
    public static void Main(String[] args) 
    { 
        printAliquot(12); 
    } 
} 

/* This code has been contributed 
by PrinciRaj1992*/
```

**输出:**

```
12 16 15 9 4 3 1 0 

```

**参考:**T2[https://en.wikipedia.org/wiki/Aliquot_sequence](https://en.wikipedia.org/wiki/Aliquot_sequence)

本文由 [**哈什·阿加瓦尔**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。