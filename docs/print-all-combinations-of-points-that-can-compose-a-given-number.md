# 打印所有可以组成给定数字的点的组合

> 原文:[https://www . geesforgeks . org/print-所有可以组成给定数字的点的组合/](https://www.geeksforgeeks.org/print-all-combinations-of-points-that-can-compose-a-given-number/)

你可以赢三种篮球分，1 分，2 分，3 分。给定总分 n，打印出组成 n 的所有组合。

**示例:**

```
For n = 1, the program should print following:
1

For n = 2, the program should print following:
1 1
2

For n = 3, the program should print following:
1 1 1
1 2
2 1 
3

For n = 4, the program should print following:
1 1 1 1
1 1 2
1 2 1
1 3
2 1 1
2 2
3 1

and so on ...
```

**算法:**

1.  在第一个位置，我们可以有三个数字 1 或 2 或 3。
2.  首先，把 1 放在第一个位置，递归调用 n-1。
3.  然后把 2 放在第一个位置，递归调用 n-2。
4.  然后把 3 放在第一个位置，递归调用 n-3。
5.  如果 n 变成 0，那么我们就形成了一个由 n 组成的组合，所以打印当前的组合。

下面是一个概括的实现。在下面的实现中，如果篮球比赛中有更高的分数(超过 3 分)，我们可以更改 MAX_POINT。

## C++

```
// C++ program to Print all
// combinations of points that
// can compose a given number
#define MAX_POINT 3
#define ARR_SIZE 100
#include <bits/stdc++.h>
using namespace std;

/* Utility function to print array arr[] */
void printArray(int arr[], int arr_size);

/* The function prints all combinations of numbers 1, 2, ...MAX_POINT
that sum up to n.
i is used in recursion keep track of index in arr[] where next
element is to be added. Initital value of i must be passed as 0 */
void printCompositions(int n, int i)
{

    /* array must be static as we want to keep track
    of values stored in arr[] using current calls of
    printCompositions() in function call stack*/
    static int arr[ARR_SIZE];

    if (n == 0)
    {
        printArray(arr, i);
    }
    else if(n > 0)
    {
        int k;
        for (k = 1; k <= MAX_POINT; k++)
        {
            arr[i]= k;
            printCompositions(n-k, i+1);
        }
    }
}

/* UTILITY FUNCTIONS */
/* Utility function to print array arr[] */
void printArray(int arr[], int arr_size)
{
    int i;
    for (i = 0; i < arr_size; i++)
        cout<<arr[i]<<" ";
    cout<<endl;
}

/* Driver code */
int main()
{
    int n = 5;

    cout<<"Different compositions formed by 1, 2 and 3 of "<<n<<" are\n";
    printCompositions(n, 0);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to Print all
// combinations of points that
// can compose a given number
#define MAX_POINT 3
#define ARR_SIZE 100
#include<stdio.h>

/* Utility function to print array arr[] */
void printArray(int arr[], int arr_size);

/* The function prints all combinations of numbers 1, 2, ...MAX_POINT
that sum up to n.
i is used in recursion keep track of index in arr[] where next
element is to be added. Initital value of i must be passed as 0 */
void printCompositions(int n, int i)
{

    /* array must be static as we want to keep track
    of values stored in arr[] using current calls of
    printCompositions() in function call stack*/
    static int arr[ARR_SIZE];

    if (n == 0)
    {
        printArray(arr, i);
    }
    else if(n > 0)
    {
        int k;
        for (k = 1; k <= MAX_POINT; k++)
        {
        arr[i]= k;
        printCompositions(n-k, i+1);
        }
    }
}

/* UTILITY FUNCTIONS */
/* Utility function to print array arr[] */
void printArray(int arr[], int arr_size)
{
    int i;
    for (i = 0; i < arr_size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

/* Driver function to test above functions */
int main()
{
    int n = 5;

    printf("Different compositions formed by 1, 2 and 3 of %d are\n", n);
    printCompositions(n, 0);

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Print all
// combinations of points that
// can compose a given number
import java.io.*;

class GFG
{
    // Function prints all combinations of numbers 1, 2, ...MAX_POINT
    // that sum up to n.
    // i is used in recursion keep track of index in arr[] where next
    // element is to be added. Initital value of i must be passed as 0
    static void printCompositions(int arr[], int n, int i)
    {
        int MAX_POINT = 3;
        if (n == 0)
        {
            printArray(arr, i);
        }
        else if(n > 0)
        {
            for (int k = 1; k <= MAX_POINT; k++)
            {
                arr[i]= k;
                printCompositions(arr, n-k, i+1);
            }
        }
    }

    // Utility function to print array arr[]
    static void printArray(int arr[], int m)
    {
        for (int i = 0; i < m; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 5;
        int size = 100;
        int[] arr = new int[size];
        System.out.println("Different compositions formed by 1, 2 and 3 of "+ n + " are");
        printCompositions(arr, n, 0);
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to Print all combinations
# of points that can compose a given number
MAX_POINT = 3;
ARR_SIZE = 100;

arr = [0] * ARR_SIZE;

# The function prints all combinations
# of numbers 1, 2, ...MAX_POINT that sum
# up to n. i is used in recursion keep
# track of index in arr[] where next
# element is to be added. Initital value
# of i must be passed as 0
def printCompositions(n, i):

    # array must be static as we
    # want to keep track of values
    # stored in arr[] using current
    # calls of printCompositions() in
    # function call stack*/
    if (n == 0):
        printArray(arr, i);
    elif(n > 0):
        for k in range(1,MAX_POINT + 1):
            arr[i] = k;
            printCompositions(n - k, i + 1);

# UTILITY FUNCTIONS */
# Utility function to print array arr[] */
def printArray(arr, arr_size):
    for i in range(arr_size):
        print(arr[i], end = " ");
    print();

# Driver Code
n = 5;
print("Different compositions formed " +
         "by 1, 2 and 3 of", n, " are");
printCompositions(n, 0);

# This code is contributed by mits
```

## C#

```
// C# program to Print all
// combinations of points that
// can compose a given number
using System;

class GFG {

    // Function prints all combinations of numbers
    // 1, 2, ...MAX_POINT that sum up to n. i is
    // used in recursion keep track of index in
    // arr[] where next element is to be added.
    // Initital value of i must be passed as 0
    static void printCompositions(int[] arr, int n, int i)
    {
        int MAX_POINT = 3;
        if (n == 0) {
            printArray(arr, i);
        }
        else if (n > 0) {
            for (int k = 1; k <= MAX_POINT; k++) {
                arr[i] = k;
                printCompositions(arr, n - k, i + 1);
            }
        }
    }

    // Utility function to print array arr[]
    static void printArray(int[] arr, int m)
    {
        for (int i = 0; i < m; i++)
            Console.Write(arr[i] + " ");
        Console.WriteLine();
    }

    // Driver program
    public static void Main()
    {
        int n = 5;
        int size = 100;
        int[] arr = new int[size];

        Console.WriteLine("Different compositions formed"
                    + " by 1, 2 and 3 of " + n + " are");
        printCompositions(arr, n, 0);
    }
}

// Contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Print all
// combinations of points that
// can compose a given number
$MAX_POINT = 3;
$ARR_SIZE = 100;

$arr = array($ARR_SIZE);

/* The function prints all combinations
of numbers 1, 2, ...MAX_POINT that sum
up to n. i is used in recursion keep
track of index in arr[] where next
element is to be added. Initital value
of i must be passed as 0 */
function printCompositions($n, $i)
{
    global $arr, $MAX_POINT, $ARR_SIZE;

    /* array must be static as we
    want to keep track of values
    stored in arr[] using current
    calls of printCompositions() in
    function call stack*/
    if ($n == 0)
    {
        printArray($arr, $i);
    }
    else if($n > 0)
    {
        for ($k = 1; $k <= $MAX_POINT; $k++)
        {
            $arr[$i] = $k;
            printCompositions($n - $k, $i + 1);
        }
    }
}

/* UTILITY FUNCTIONS */
/* Utility function to print array arr[] */
function printArray($arr, $arr_size)
{
    for ($i = 0; $i < $arr_size; $i++)
        echo $arr[$i]." ";
    echo "\n";
}

// Driver Code
$n = 5;

echo "Different compositions formed" .
     " by 1, 2 and 3 of ".$n." are\n";
printCompositions($n, 0);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print all
// combinations of points that
// can compose a given number

// Function prlets all combinations of numbers
// 1, 2, ...MAX_POlet that sum up to n.
// i is used in recursion keep track of index
// in arr[] where next element is to be added.
// Initital value of i must be passed as 0
function printCompositions(arr, n, i)
{
    let MAX_POINT = 3;
    if (n == 0)
    {
        printArray(arr, i);
    }
    else if(n > 0)
    {
        for(let k = 1; k <= MAX_POINT; k++)
        {
            arr[i] = k;
            printCompositions(arr, n - k, i + 1);
        }
    }
}

// Utility function to print array arr[]
function printArray(arr, m)
{
    for(let i = 0; i < m; i++)
        document.write(arr[i] + " ");

    document.write("<br/>");
}

// Driver code
let n = 5;
let size = 100;
let arr = new Array(size).fill(0);

document.write("Different compositions formed " +
               "by 1, 2 and 3 of "+ n + " are" + "<br/>");
printCompositions(arr, n, 0);

// This code is contributed by avijitmondal1998

</script>
```

**输出:**

```
Different compositions formed by 1, 2 and 3 of 5 are
1 1 1 1 1 
1 1 1 2 
1 1 2 1 
1 1 3 
1 2 1 1 
1 2 2 
1 3 1 
2 1 1 1 
2 1 2 
2 2 1 
2 3 
3 1 1 
3 2 
```

如果发现以上代码/算法有任何 bug，请写评论，或者找其他方法解决同样的问题。