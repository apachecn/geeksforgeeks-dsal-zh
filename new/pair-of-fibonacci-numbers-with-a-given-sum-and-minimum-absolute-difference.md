# 一对具有给定总和和最小绝对差的斐波那契数

> 原文：[https://www.geeksforgeeks.org/pair-of-fibonacci-numbers-with-a-given-sum-and-minimum-absolute-difference/](https://www.geeksforgeeks.org/pair-of-fibonacci-numbers-with-a-given-sum-and-minimum-absolute-difference/)

给定整数`N`（小于`10 ^ 6`），任务是找到一对[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，其总和等于给定的`N`， 所选对之间的绝对差最小。

如果没有解决方法，请打印`-1`。

**示例**：

> **输入**：`N = 199`
>
> **输出**：`55 144`
>
> **说明**
>
> 199 可以表示为总和 55 和 144，其最小值 区别。
>
> **输入**：`N = 1830`
>
> **输出**：`233 1597`
>
> **说明**
>
> 1830 可以表示为总和 233 和 1597，其中 具有最小的差异。

**方法**：想法是使用[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)预先计算并存储[斐波纳契节点](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)直到最大值，以使检查变得容易和高效（在`O(1)`中 时间）。

预计算了[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)之后：

1.  从`N / 2`到 1 开始循环（以最小化绝对差），并检查循环计数器`i`和`N – i`是否均为斐波那契。

2.  如果它们是斐波那契，那么我们将打印它们并退出循环。

3.  如果数字`N`不能表示为两个斐波纳契数之和，则我们将打印 -1。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the pair of
// Fibonacci numbers with a given sum
// and minimum absolute difference

#include <bits/stdc++.h>
using namespace std;
#define MAX 1000005

// Hash to store all the
// Fibonacci numbers
set<int> fib;

// Function to generate fibonacci Series
// and create hash table
// to check Fibonacci numbers
void fibonacci()
{
    // Adding the first two Fibonacci
    // numbers into the Hash set
    int prev = 0, curr = 1, len = 2;
    fib.insert(prev);
    fib.insert(curr);

    // Computing the remaining Fibonacci
    // numbers based on the previous
    // two numbers
    while (len <= MAX) {
        int temp = curr + prev;
        fib.insert(temp);
        prev = curr;
        curr = temp;
        len++;
    }
}

// Function to find the pair of
// Fibonacci numbers with the given
// sum and minimum absolute difference
void findFibonacci(int N)
{

    // Start from N/2 such that the
    // difference between i and
    // N - i will be minimum
    for (int i = N / 2; i > 1; i--) {

        // If both 'i' and 'sum - i' are
        // fibonacci numbers then print
        // them and break the loop
        if (fib.find(i) != fib.end()
            && fib.find(N - i) != fib.end()) {

            cout << i << " " << (N - i) << endl;
            return;
        }
    }

    // If there is no Fibonacci pair
    // possible
    cout << "-1" << endl;
}

// Driver code
int main()
{
    // Generate the Fibonacci numbers
    fibonacci();

    int sum = 199;

    // Find the Fibonacci pair
    findFibonacci(sum);

    return 0;
}

```

## Java

```java

// Java program to find the pair of
// Fibonacci numbers with a given sum
// and minimum absolute difference
import java.util.*;

class GFG{
    // Hash to store all the
    // Fibonacci numbers
    static int MAX=1000005;
    static  Set<Integer> fib=new HashSet<Integer>();

    // Function to generate fibonacci Series
    // and create hash table
    // to check Fibonacci numbers
    static void fibonacci()
    {
        // Adding the first two Fibonacci
        // numbers into the Hash set
        int prev = 0, curr = 1, len = 2;
        fib.add(prev);
        fib.add(curr);

        // Computing the remaining Fibonacci
        // numbers based on the previous
        // two numbers
        while (len <= MAX) {
            int temp = curr + prev;
            fib.add(temp);
            prev = curr;
            curr = temp;
            len++;
        }
    }

    // Function to find the pair of
    // Fibonacci numbers with the given
    // sum and minimum absolute difference
    static void findFibonacci(int N)
    {

        // Start from N/2 such that the
        // difference between i and
        // N - i will be minimum
        for (int i = N / 2; i > 1; i--) {

            // If both 'i' and 'sum - i' are
            // fibonacci numbers then print
            // them and break the loop
            if (fib.contains(i)  && fib.contains(N - i)) {

                System.out.println(i+" "+(N - i));
                return;
            }
        }

        // If there is no Fibonacci pair
        // possible
        System.out.println("-1");
    }

    // Driver code
    public static void main(String args[])
    {
        // Generate the Fibonacci numbers
        fibonacci();

        int sum = 199;

        // Find the Fibonacci pair
        findFibonacci(sum);

    }
}

// This code is contributed by AbhiThakur

```

## Python3

```py

# Python 3 program to find 
# the pair of Fibonacci numbers 
# with a given sum and minimum 
# absolute difference
MAX = 10005

# Hash to store all the
# Fibonacci numbers
fib = set()

# Function to generate 
# fibonacci Series and 
# create hash table 
# to check Fibonacci 
# numbers
def fibonacci():

    global fib
    global MAX

    # Adding the first 
    # two Fibonacci numbers 
    # into the Hash set
    prev = 0
    curr = 1
    l = 2
    fib.add(prev)
    fib.add(curr)

    # Computing the remaining 
    # Fibonacci numbers based 
    # on the previous two numbers
    while(l <= MAX):
        temp = curr + prev
        fib.add(temp)
        prev = curr
        curr = temp
        l += 1

# Function to find the 
# pair of Fibonacci numbers 
# with the given sum and 
# minimum absolute difference
def findFibonacci(N):

    global fib

    # Start from N/2 such 
    # that the difference 
    # between i and N - i 
    # will be minimum
    i = N//2
    while(i > 1):

        # If both 'i' and 'sum - i' 
        # are fibonacci numbers then 
        # print them and break the loop
        if (i in fib and
            (N - i) in fib):
            print(i, (N - i))
            return
        i -= 1

    # If there is no Fibonacci 
    # pair possible
    print("-1")

# Driver code
if __name__ == '__main__':

    # Generate the Fibonacci 
    # numbers
    fibonacci()
    sum = 199

    # Find the Fibonacci pair
    findFibonacci(sum)

# This code is contributed by bgangwar59

```

## C#

```cs

// C# program to find the pair of
// Fibonacci numbers with a given sum
// and minimum absolute difference
using System;
using System.Collections.Generic;

class GFG{
    // Hash to store all the
    // Fibonacci numbers
    static int MAX=100005;
    static  HashSet<int> fib=new HashSet<int>();

    // Function to generate fibonacci Series
    // and create hash table
    // to check Fibonacci numbers
    static void fibonacci()
    {
        // Adding the first two Fibonacci
        // numbers into the Hash set
        int prev = 0, curr = 1, len = 2;
        fib.Add(prev);
        fib.Add(curr);

        // Computing the remaining Fibonacci
        // numbers based on the previous
        // two numbers
        while (len <= MAX) {
            int temp = curr + prev;
            fib.Add(temp);
            prev = curr;
            curr = temp;
            len++;
        }
    }

    // Function to find the pair of
    // Fibonacci numbers with the given
    // sum and minimum absolute difference
    static void findFibonacci(int N)
    {

        // Start from N/2 such that the
        // difference between i and
        // N - i will be minimum
        for (int i = N / 2; i > 1; i--) {

            // If both 'i' and 'sum - i' are
            // fibonacci numbers then print
            // them and break the loop
            if (fib.Contains(i)  && fib.Contains(N - i)) {

                Console.WriteLine(i+" "+(N - i));
                return;
            }
        }

        // If there is no Fibonacci pair
        // possible
        Console.WriteLine("-1");
    }

    // Driver code
    public static void Main(String []args)
    {
        // Generate the Fibonacci numbers
        fibonacci();

        int sum = 199;

        // Find the Fibonacci pair
        findFibonacci(sum);
    }
}

// This code is contributed by sapnasingh4991

```

**输出**： 

```
55 144

```



* * *

* * *



