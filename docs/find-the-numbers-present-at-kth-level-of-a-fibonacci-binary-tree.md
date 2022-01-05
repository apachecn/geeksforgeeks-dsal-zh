# 找出斐波那契二叉树第 k 层的数字

> 原文:[https://www . geesforgeks . org/find-the-numbers-present-at-kth-level-of-Fibonacci-二叉树/](https://www.geeksforgeeks.org/find-the-numbers-present-at-kth-level-of-a-fibonacci-binary-tree/)

给定一个数字 **K** ，任务是打印出现在**第**级**斐波那契二叉树**的[斐波那契数字](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
**举例:**

```
Input: K = 3
Output: 2, 3, 5, 8
Explanation:
Fibonacci Binary Tree for 3 levels:
        0
       / \
      1   1
     /\  / \
    2  3 5  8
Numbers present at level 3: 2, 3, 5, 8

Input: K = 2
Output: 1, 1
Explanation:
Fibonacci Binary Tree for 2 levels:
        0
       / \
      1   1
Numbers present at level 2: 1, 1
```

**天真方法:**天真的方法是构建一个斐波那契二叉树([斐波那契数的二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/))，然后获取特定级别 k 的元素。
然而，这种方法对于大数来说已经过时了，因为它需要太多时间。
**有效方法:**因为可以通过在范围**【2】<sup>K–1</sup>、2<sup>K</sup>–1】**中找到元素来找到存在于树的某个任意级别 K 的元素。因此:

1.  使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)找到[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)到 10 <sup>6</sup> ，并将其存储在数组中。
2.  计算级别的左索引和右索引，如下所示:

```
left_index = 2K - 1 
right_index = 2K - 1
```

1.  打印斐波那契数列从左索引到右索引的斐波那契数。

以下是上述方法的实现:

## C++

```
// C++ program to print the Fibonacci numbers
// present at K-th level of a Binary Tree

#include <bits/stdc++.h>
using namespace std;

// Initializing the max value
#define MAX_SIZE 100005

// Array to store all the
// fibonacci numbers
int fib[MAX_SIZE + 1];

// Function to generate fibonacci numbers
// using Dynamic Programming
void fibonacci()
{
    int i;

    // 0th and 1st number of the series
    // are 0 and 1
    fib[0] = 0;
    fib[1] = 1;

    for (i = 2; i <= MAX_SIZE; i++) {

        // Add the previous two numbers in the
        // series and store it
        fib[i] = fib[i - 1] + fib[i - 2];
    }
}

// Function to print the Fibonacci numbers
// present at Kth level of a Binary Tree
void printLevel(int level)
{
    // Finding the left and right index
    int left_index = pow(2, level - 1);
    int right_index = pow(2, level) - 1;

    // Iterating and printing the numbers
    for (int i = left_index;
         i <= right_index; i++) {

        cout << fib[i - 1] << " ";
    }
    cout << endl;
}

// Driver code
int main()
{
    // Precomputing Fibonacci numbers
    fibonacci();

    int K = 4;
    printLevel(K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the Fibonacci numbers
// present at K-th level of a Binary Tree
import java.util.*;

class GFG{

// Initializing the max value
static final int MAX_SIZE = 100005;

// Array to store all the
// fibonacci numbers
static int []fib = new int[MAX_SIZE + 1];

// Function to generate fibonacci numbers
// using Dynamic Programming
static void fibonacci()
{
    int i;

    // 0th and 1st number of the series
    // are 0 and 1
    fib[0] = 0;
    fib[1] = 1;

    for (i = 2; i <= MAX_SIZE; i++) {

        // Add the previous two numbers in the
        // series and store it
        fib[i] = fib[i - 1] + fib[i - 2];
    }
}

// Function to print the Fibonacci numbers
// present at Kth level of a Binary Tree
static void printLevel(int level)
{
    // Finding the left and right index
    int left_index = (int) Math.pow(2, level - 1);
    int right_index = (int) (Math.pow(2, level) - 1);

    // Iterating and printing the numbers
    for (int i = left_index;
         i <= right_index; i++) {

        System.out.print(fib[i - 1]+ " ");
    }
    System.out.println();
}

// Driver code
public static void main(String[] args)
{
    // Precomputing Fibonacci numbers
    fibonacci();

    int K = 4;
    printLevel(K);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to print the Fibonacci numbers
# present at K-th level of a Binary Tree

# Initializing the max value
MAX_SIZE = 100005

# Array to store all the
# fibonacci numbers
fib =[0]*(MAX_SIZE + 1)

# Function to generate fibonacci numbers
# using Dynamic Programming
def fibonacci():

    # 0th and 1st number of the series
    # are 0 and 1
    fib[0] = 0
    fib[1] = 1

    for i in range(2, MAX_SIZE + 1):

        # Add the previous two numbers in the
        # series and store it
        fib[i] = fib[i - 1] + fib[i - 2]

# Function to print the Fibonacci numbers
# present at Kth level of a Binary Tree
def printLevel(level):

    # Finding the left and right index
    left_index = pow(2, level - 1)
    right_index = pow(2, level) - 1

    # Iterating and printing the numbers
    for i in range(left_index, right_index+1):
        print(fib[i - 1],end=" ")

    print()

# Driver code

# Precomputing Fibonacci numbers
fibonacci()

K = 4
printLevel(K)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to print the Fibonacci numbers
// present at K-th level of a Binary Tree
using System;

class GFG{

    // Initializing the max value
    static int MAX_SIZE = 100005;

    // Array to store all the
    // fibonacci numbers
    static int []fib = new int[MAX_SIZE + 1];

    // Function to generate fibonacci numbers
    // using Dynamic Programming
    static void fibonacci()
    {
        int i;

        // 0th and 1st number of the series
        // are 0 and 1
        fib[0] = 0;
        fib[1] = 1;

        for (i = 2; i <= MAX_SIZE; i++) {

            // Add the previous two numbers in the
            // series and store it
            fib[i] = fib[i - 1] + fib[i - 2];
        }
    }

    // Function to print the Fibonacci numbers
    // present at Kth level of a Binary Tree
    static void printLevel(int level)
    {
        // Finding the left and right index
        int left_index = (int) Math.Pow(2, level - 1);
        int right_index = (int) (Math.Pow(2, level) - 1);

        // Iterating and printing the numbers
        for (int i = left_index;
            i <= right_index; i++) {

            Console.Write(fib[i - 1]+ " ");
        }
            Console.WriteLine();
    }

    // Driver code
    public static void Main(string[] args)
    {
        // Precomputing Fibonacci numbers
        fibonacci();

        int K = 4;
        printLevel(K);
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript program to print the Fibonacci numbers
// present at K-th level of a Binary Tree

    // Initializing the max value
     var MAX_SIZE = 100005;

    // Array to store all the
    // fibonacci numbers
    var fib = Array(MAX_SIZE + 1).fill(0);

    // Function to generate fibonacci numbers
    // using Dynamic Programming
    function fibonacci()
    {
        var i;

        // 0th and 1st number of the series
        // are 0 and 1
        fib[0] = 0;
        fib[1] = 1;

        for (i = 2; i <= MAX_SIZE; i++)
        {

            // Add the previous two numbers in the
            // series and store it
            fib[i] = fib[i - 1] + fib[i - 2];
        }
    }

    // Function to print the Fibonacci numbers
    // present at Kth level of a Binary Tree
    function printLevel(level)
    {
        // Finding the left and right index
        var left_index =
        parseInt( Math.pow(2, level - 1));
        var right_index =
        parseInt( (Math.pow(2, level) - 1));

        // Iterating and printing the numbers
        for (i = left_index; i <= right_index; i++)
        {

            document.write(fib[i - 1] + " ");
        }
        document.write();
    }

    // Driver code

        // Precomputing Fibonacci numbers
        fibonacci();

        var K = 4;
        printLevel(K);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
13 21 34 55 89 144 233 377
```