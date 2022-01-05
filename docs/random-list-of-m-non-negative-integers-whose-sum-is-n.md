# 和为 N 的 M 个非负整数的随机列表

> 原文:[https://www . geesforgeks . org/random-list-m-非负整数-其和为-n/](https://www.geeksforgeeks.org/random-list-of-m-non-negative-integers-whose-sum-is-n/)

给定两个整数 **M** 和 **N** ，任务是创建一个 **M** 非负整数列表，其和为 **N** 。如果可能有多个列表，请找到任意一个。
**举例:**

> **输入:** M = 4，N = 8
> **输出:** 1 3 3 1
> 1 + 3 + 3 + 1 = 8
> **输入:** M = 5，N = 3
> **输出:**0 1 0 1 1

**方法:**要获得整数的完整随机列表，创建一个大小为 **M** 的数组，其中每个元素都用 **0** 初始化。现在运行从 **0** 到**N–1**的循环，并使用 [rand()](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/) 功能通过 **1** 增加数组中任意随机选择的元素。这样，结果列表的总和将为 **N** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the
// elements of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to generate a list of
// m random non-negative integers
// whose sum is n
void randomList(int m, int n)
{

    // Create an array of size m where
    // every element is initialized to 0
    int arr[m] = { 0 };
    srand(time(0));

    // To make the sum of the final list as n
    for (int i = 0; i < n; i++) {

        // Increment any random element
        // from the array by 1
        arr[rand() % m]++;
    }

    // Print the generated list
    printArr(arr, m);
}

// Driver code
int main()
{
    int m = 4, n = 8;

    randomList(m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Utility function to print the
// elements of an array
static void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Function to generate a list of
// m random non-negative integers
// whose sum is n
static void randomList(int m, int n)
{

    // Create an array of size m where
    // every element is initialized to 0
    int arr[] = new int[m];

    // To make the sum of the final list as n
    for (int i = 0; i < n; i++)
    {

        // Increment any random element
        // from the array by 1
        arr[(int)(Math.random() * m)]++;
    }

    // Print the generated list
    printArr(arr, m);
}

// Driver code
public static void main(String args[])
{
    int m = 4, n = 8;

    randomList(m, n);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from random import randint

# Utility function to print the
# elements of an array
def printArr(arr, n) :

    for i in range(n) :
        print(arr[i], end = " ");

# Function to generate a list of
# m random non-negative integers
# whose sum is n
def randomList(m, n):

    # Create an array of size m where
    # every element is initialized to 0
    arr = [0] * m;

    # To make the sum of the final list as n
    for i in range(n) :

        # Increment any random element
        # from the array by 1
        arr[randint(0, n) % m] += 1;

    # Print the generated list
    printArr(arr, m);

# Driver code
if __name__ == "__main__" :

    m = 4; n = 8;

    randomList(m, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Utility function to print the
// elements of an array
static void printArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function to generate a list of
// m random non-negative integers
// whose sum is n
static void randomList(int m, int n)
{

    // Create an array of size m where
    // every element is initialized to 0
    int [] arr = new int[m];

    // To make the sum of the final list as n
    for (int i = 0; i < n; i++)
    {

        // Increment any random element
        // from the array by 1
        Random rnd = new Random();

        arr[rnd.Next(0, n) % m]++;
    }

    // Print the generated list
    printArr(arr, m);
}

// Driver code
public static void Main()
{
    int m = 4, n = 8;

    randomList(m, n);
}
}

// This code is contributed by Mohit kumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    // Utility function to print the
// elements of an array
    function printArr(arr,n)
    {
        for (let i = 0; i < n; i++)
            document.write(arr[i] + " ");   
    }

    // Function to generate a list of
// m random non-negative integers
// whose sum is n
    function randomList(m,n)
    {
        // Create an array of size m where
    // every element is initialized to 0
    let arr = new Array(m);
    for(let i=0;i<arr.length;i++)
    {
        arr[i]=0;
    }

    // To make the sum of the final list as n
    for (let i = 0; i < n; i++)
    {

        // Increment any random element
        // from the array by 1
        arr[(Math.floor((Math.random() * n) )%m)]++;
    }

    // Print the generated list
    printArr(arr, m);
    }

    // Driver code
    let m = 4, n = 8;
    randomList(m, n);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
1 3 3 1
```

**时间复杂度:** O(max(M，N))