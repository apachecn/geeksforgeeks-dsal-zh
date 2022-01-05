# 打印三角形分离图案

> 原文:[https://www . geesforgeks . org/print-triangle-separated-pattern/](https://www.geeksforgeeks.org/print-triangle-separated-pattern/)

给定一个数字 **N** ，任务是打印三角形分离图案。

> **三角形分隔图案:**四个三角形(左、下、右、上)用正斜杠分隔的图案，见下图:
> \ * * * * */
> * \ * * */*
> * * */* *
> * * */
> * * * \ *
> */* * * \ *
> /* * * * * \

**注:** **N** 应为奇数， **N** 的值应大于 4。
**举例:**

```
Input: N = 5
Output: 
        \***/
        *\*/*
        **/**
        */*\*
        /***\

Input: N = 7
Output:
        \*****/
        *\***/*
        **\*/**
        ***/***
        **/*\**
        */***\*
        /*****\
```

**逼近:**通过观察上述模式，当行列索引相等时，则打印**“**”，当行列索引之和为 **N** 时，则打印**/**。下面是[递归方法](https://www.geeksforgeeks.org/recursion/) :

1.  使用两个值 **i** 作为行，使用 **j** 作为列，从 **(0，0)** 迭代到 **(N-1，N-1)** 以打印所需的图案。
2.  递归迭代从 **(0，0)** 到 **(N-1，N-1)** :
    *   **基本情况:**如果行和列的索引大于或等于 **N** 是给定模式的终止条件。

```
if(i >= N) {
  return 0;
}
if(j >= N) {
  return 1;
}
```

*   **打印声明:**如果不满足基本情况条件，则在以下条件的基础上打印**/**、**“**、**' ***:

```
if(i==j) {
   print('')
}
else if(i + j == N-1) {
   print('/')
}
else {
   print('*')
}
```

*   **递归调用:**在每次递归调用时(基本情况除外)，返回行和列的下一次迭代的递归函数:

```
// Recursive call for rows
recursive_function(i, j+1, N)

// Recursive call for changing rows
recursive_function(i+1, j, N)
```

下面是上述方法的实现:

## C++

```
// C++ program to print the triangle
// separated pattern using
// star and slash character

#include <bits/stdc++.h>
using namespace std;

// Function to print pattern recursively
int printPattern(
    int i, int j, int n)
{
    // Base Case
    if (j >= n) {
        return 0;
    }
    if (i >= n) {
        return 1;
    }

    // Conditions to print slash
    if (j == i || j == n - 1 - i) {

        // Condition to print
        // forword slash
        if (i == n - 1 - j) {
            cout << "/";
        }

        // Condition to print
        // backward slash
        else {
            cout << "\\";
        }
    }

    // Else print '*'
    else {
        cout << "*";
    }

    // Recursive call for rows
    if (printPattern(i, j + 1, n)
        == 1) {
        return 1;
    }

    cout << endl;

    // Recursive call for changing
    // the rows
    return printPattern(i + 1, 0, n);
}

// Driver Code
int main()
{
    int N = 9;

    // Function Call
    printPattern(0, 0, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the triangle
// separated pattern using
// star and slash character
class GFG{

// Function to print pattern recursively
static int printPattern(
    int i, int j, int n)
{
    // Base Case
    if (j >= n) {
        return 0;
    }
    if (i >= n) {
        return 1;
    }

    // Conditions to print slash
    if (j == i || j == n - 1 - i) {

        // Condition to print
        // forword slash
        if (i == n - 1 - j) {
            System.out.print("/");
        }

        // Condition to print
        // backward slash
        else {
            System.out.print("\\");
        }
    }

    // Else print '*'
    else {
        System.out.print("*");
    }

    // Recursive call for rows
    if (printPattern(i, j + 1, n)
        == 1) {
        return 1;
    }

    System.out.println();

    // Recursive call for changing
    // the rows
    return printPattern(i + 1, 0, n);
}

// Driver Code
public static void main(String[] args)
{
    int N = 9;

    // Function Call
    printPattern(0, 0, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to print the triangle
# separated pattern using
# star and slash character

# Function to print pattern recursively
def printPattern(i,j, n):

    # Base Case
    if (j >= n) :
        return 0
    if (i >= n):
        return 1

    # Conditions to print slash
    if (j == i or j == n - 1 - i):

        # Condition to print
        # forword slash
        if (i == n - 1 - j):
            print("/",end="")

        # Condition to print
        # backward slash
        else:
            print("\\",end="")

    # Else print '*'
    else:
        print("*",end="")

    # Recursive call for rows
    if (printPattern(i, j + 1, n)
        == 1):
        return 1

    print()

    # Recursive call for changing
    # the rows
    return printPattern(i + 1, 0, n)

# Driver Code
if __name__ == "__main__":

    N = 9

    # Function Call
    printPattern(0, 0, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program to print the triangle
// separated pattern using
// star and slash character
using System;

class GFG{

// Function to print pattern recursively
static int printPattern(
    int i, int j, int n)
{
    // Base Case
    if (j >= n) {
        return 0;
    }
    if (i >= n) {
        return 1;
    }

    // Conditions to print slash
    if (j == i || j == n - 1 - i) {

        // Condition to print
        // forword slash
        if (i == n - 1 - j) {
            Console.Write("/");
        }

        // Condition to print
        // backward slash
        else {
            Console.Write("\\");
        }
    }

    // Else print '*'
    else {
        Console.Write("*");
    }

    // Recursive call for rows
    if (printPattern(i, j + 1, n)
        == 1) {
        return 1;
    }

    Console.WriteLine();

    // Recursive call for changing
    // the rows
    return printPattern(i + 1, 0, n);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 9;

    // Function Call
    printPattern(0, 0, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to print the triangle
// separated pattern using
// star and slash character

// Function to print pattern recursively
function printPattern(i,j,n)
{
    // Base Case
    if (j >= n) {
        return 0;
    }
    if (i >= n) {
        return 1;
    }

    // Conditions to print slash
    if (j == i || j == n - 1 - i) {

        // Condition to print
        // forword slash
        if (i == n - 1 - j) {
            document.write("/");
        }

        // Condition to print
        // backward slash
        else {
            document.write("\\");
        }
    }

    // Else print '*'
    else {
        document.write("*");
    }

    // Recursive call for rows
    if (printPattern(i, j + 1, n)
        == 1) {
        return 1;
    }

    document.write("<br>");

    // Recursive call for changing
    // the rows
    return printPattern(i + 1, 0, n);
}

// Driver Code

let N = 9;
// Function Call
printPattern(0, 0, N);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
\*******/
*\*****/*
**\***/**
***\*/***
****/****
***/*\***
**/***\**
*/*****\*
/*******\
```